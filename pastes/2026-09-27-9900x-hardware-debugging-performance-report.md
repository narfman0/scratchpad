---
title: "9900x Hardware Debugging & Performance Report"
date: 2026-09-27 02:02:40 +0000
author: pinky
---

# 9900x Desktop — Hardware Debugging & Performance Report

**Machine:** Ryzen 9 9900X · ASUS TUF GAMING X870-PLUS WIFI · RTX 5070 Ti · 2×16 GB G.Skill F5-5600J2834F16G · WD Blue SN570 (root) · Fedora 44, kernel 7.2.7

**Period covered:** 2026-07-03 → 2026-09-26 (50+ boots of journal history)

**Status as of 2026-09-26:** all five hardware issues resolved and verified. A sixth
investigation (storage / boot / launch latency) was run on 2026-09-26 and closed with a
*do-not-buy* finding — see §6.

---

## Summary

| # | Issue | Fixed | Headline result |
|---|---|---|---|
| 1 | Keyboard dropouts needing unplug/replug | pre-Aug 2026 | Moved to CPU-direct USB controller; dropouts stopped |
| 2 | BIOS 16 months out of date | 2026-08-11 | 1006 (Feb 2025) → 1681 (Jun 2026) |
| 3 | Post-resume hard freeze | 2026-09-15 | 10 crashes → **0 in 24 suspend cycles** |
| 4 | RAM running below spec | 2026-09-25 | 4800 → **5600 MT/s** (+16.7%) |
| 5 | CPU thermally throttled to half speed | 2026-09-25 | 2.78 → **5.28 GHz all-core** (+90%) |
| 6 | "Still feels slow" — SSD upgrade worth it? | investigated 2026-09-26 | **No.** Disk is at the latency floor; 71 s of the 100 s boot is BIOS memory training |

The single largest win was #5: the CPU had been silently delivering roughly half its multicore throughput.

---

## 1. Keyboard dropouts — USB topology

**Symptom.** Keyboard would stop responding; recovery required physically unplugging and replugging it.

**Diagnosis.** The keyboard was enumerated on a USB controller that reaches the CPU only through the chipset's PCIe switch, rather than on one of the CPU's own USB controllers.

**Fix.** Moved the keyboard to a CPU-direct port.

**Verified current topology (2026-09-25).** Das Keyboard 4 (`24f0:0140`) sits at `usb 7-2.4` on controller `0000:73:00.4` — *AMD Raphael/Granite Ridge USB 3.1 xHCI* — which hangs directly off `00:08.1`, the CPU's internal GPP bridge. That is **one hop from the CPU die**.

For contrast, the chipset USB controller `09:00.0` (*800 Series Chipset USB 3.x xHCI*, buses 1–2) is reached via `00:02.1 → 03:00.0 → 04:0c.0 → 09:00.0` — **four hops** through the Promontory PCIe switch. That is almost certainly where the keyboard used to live.

> Note: the keyboard is behind a VIA Labs VL812 hub, but the *hub itself* is plugged into the CPU-direct controller, so the fix holds. Hub presence is not the relevant variable; which controller the chain roots at is.

**Caveat.** This predates the retained session transcripts, so the original diagnosis is reconstructed from the surviving hardware state plus the user's recollection. The topology evidence above is current and directly measured.

---

## 2. BIOS update — 1006 → 1681

**Evidence (kernel DMI line, per boot):**

- boots through 2026-08-10 → `BIOS 1006 02/10/2025`
- boot of 2026-08-11 onward → `BIOS 1681 06/18/2026`

The board had been running a **launch-era BIOS from February 2025 — roughly 16 months of AGESA and firmware updates skipped.** Flashed manually from within the BIOS (EZ Flash), so it left no `fwupd` history record.

**Confirmed benefit:** BIOS UI rendering improved.

**Not the sleep fix.** This was applied partly as a speculative fix for the resume freezes, but unclean shutdowns continued afterward (Aug 19, Aug 29, Sep 4, Sep 10, Sep 12, Sep 14). It did not resolve issue #3.

**But it was an enabler.** AGESA 1006 predates mature Zen 5 memory training. The later jump to 5600 MT/s (#4) and the PBO behavior seen in (#5) depend on firmware this recent, so the update was a prerequisite for the performance work even though it fixed no bug on its own.

---

## 3. Post-resume hard freeze — the long one

**Symptom.** Machine hard-froze roughly 6–7 minutes after resuming from suspend. Journal stopped mid-stream with no oops, no MCE, no pstore entry — a true hard hang with nothing written to disk.

**Scale of the problem.** 10 unclean shutdowns recorded:

> 2026-07-21 · 07-31 · 08-03 · 08-10 · 08-19 · 08-29 · 09-04 · 09-10 · 09-12 · 09-14

Against **133 suspend cycles** in that window — roughly a **7.5% failure rate per suspend**.

**Attempt 1 (~2026-07-05).** Changed the sleep profile to keep the fan running. Did not hold. (Predates retained transcripts; details not captured.)

**Attempt 2 (2026-09-12) — instrumentation, not a fix.** With no evidence surviving the hang, the session installed capture infrastructure instead of guessing:

- `kernel.sysrq=1`, `hardlockup_panic=1`, all-CPU backtraces on hard and soft lockup
- `crashkernel=2G-64G:256M,64G-:512M` reserved, `kdump` enabled
- Manual escape hatches: `Alt+SysRq+C` to force a vmcore, `Alt+SysRq+R-E-I-S-U-B` for a clean reboot
- Sleep mode switched `deep` → `s2idle` as a probe
- Live diagnostic: during a freeze, check whether Caps Lock still toggles its LED and whether SSH responds — this separates a dead kernel from a dead display path

**Root cause (2026-09-15).** The **WD Blue SN570 root drive was failing to wake from NVMe APST** (Autonomous Power State Transition). The drive entered a deep power state on suspend and never came back; the system ran until it next needed to touch the root filesystem, then hung — which explains the consistent 6–7 minute delay.

**Fix.** `nvme_core.default_ps_max_latency_us=0` — caps NVMe autonomous power-state latency, preventing entry into the unreachable state.

Applied via `grubby` to all BLS entries plus `/etc/default/grub` and `/etc/kernel/cmdline`, so it survives kernel updates. Sleep mode was deliberately reverted `s2idle` → `deep` at the same time, so the NVMe argument was the *only* changed variable — a deliberate choice by the user to keep the fix tightly scoped and falsifiable.

**Result.** **24 suspend cycles since the fix, zero freezes, zero unclean shutdowns, zero MCE/EDAC/NVMe errors.**

| | Before fix | After fix |
|---|---|---|
| Suspend cycles | 133 | 24 |
| Hard freezes | 10 | **0** |
| Failure rate | ~7.5% | **0%** |

---

## 4. Memory — 4800 → 5600 MT/s

The DIMMs are rated 5600 (XMP 3.0 profile; the kit exposes no EXPO profile) but were running at the JEDEC fallback of 4800 — **14% below their rated speed.**

Raised in two deliberate steps, each stress-verified before the next:

| Date | Speed | Verification |
|---|---|---|
| 2026-09-24 | 4800 → 5200 | `stress-ng --vm 6 --vm-bytes 20G --vm-method all --verify`, 4 min — passed |
| 2026-09-25 | 5200 → **5600** | same test — passed, 0 errors, 116.9M bogo-ops |

Running at 1.1 V. No EDAC or MCE events at any step. Net gain: **+16.7% memory clock** over the starting state.

---

## 5. CPU cooling — the largest win

**Symptom.** None visible to the user. The machine simply ran slow under load, with no error, warning, or log entry.

**Measurement (2026-09-25, before).** 24-thread `stress-ng --matrix`:

- Idle: Tctl **78.5 °C**, Tccd 63–65 °C at 38 W package
- Load: Tctl pinned at **95.4 °C** (Tjmax), throttling to **2.78 GHz at only 60 W**

A healthy 9900X sustains ~5.0–5.2 GHz at ~160 W PPT. The chip was delivering **roughly half its multicore throughput on under 40% of its power budget.**

**Ruling out the easy answer.** The obvious suspect was a bad fan curve. It was not: `nct6799` reported `pwm1..7 = 255` — 100% duty — at idle *and* under load, while fans turned only 1337 / 1909 / 1356 RPM and no channel showed a pump-like RPM signature. **The fans were already flat out and the heat still was not leaving.** That isolated the fault as mechanical — mount pressure, dried paste, or a dead pump — rather than anything configurable in software or BIOS.

**After cooler service:**

| Metric | Before | After | Change |
|---|---|---|---|
| Idle Tctl | 78.5 °C | 50–59 °C | **−20 to −28 °C** |
| Idle Tccd | 63–65 °C | 33–38 °C | **−27 °C** |
| All-core clock | 2.78 GHz | **5.24–5.32 GHz** | **+90%** |
| Package power | 60 W | 177–181 W | **+197%** |
| Load Tctl | 95.4 °C (Tjmax) | 77–79 °C | **−17 °C** |
| Throttling | Continuous | **None** | — |

Clocks held rock-steady across the full 75-second run with no thermal sag, and the package returned to 56 °C within 20 seconds of load ending.

This beat the target set before the work (5.0 GHz / 140–160 W / under 85 °C) on all three axes. Package power of 177–181 W exceeds the 9900X's 162 W stock PPT, indicating PBO or the board's enhanced power mode is active — sustainable at 79 °C with headroom remaining.

---

## 6. Storage, boot time and launch latency — measured 2026-09-26

This was not a fix but a **buy-or-not investigation**: with the CPU, RAM and sleep all healthy, the remaining complaint was that the machine still *felt* slow to boot and to open apps. The question was whether an SSD upgrade would help.

**Answer: no. Do not buy an SSD.** The conclusion below is measured, not estimated.

### Root drive is already at the NAND latency floor

Root is the WD Blue SN570 2 TB, sitting on the **chipset** M.2 slot (`00:02.1 → 03:00.0 → 04:00.0 → 05:00.0`, PCIe 3.0 x4 / 8 GT/s), btrfs with `compress=zstd:1,ssd,discard=async`.

| Measurement | Result | What it means |
|---|---|---|
| Sequential read, uncached (`dd iflag=direct`) | **3.5 GB/s** | Saturating the Gen3 x4 link |
| 4K random read, QD1, uncached | **40,279 IOPS / 25 µs** | At the NAND latency floor |
| io PSI some-stall over 23.6 h uptime | 5.5 s total (**0.006 %**) | Storage is not making anything wait |
| Drive busy time over same window | 112.6 s (**0.13 %**) | Idle 99.87 % of the time |
| Total read in 23.6 h | 15.3 GiB | 16 GiB already resident in page cache |

QD1 4K latency is what app launch actually touches, and 25 µs is essentially the floor for this NAND. A Gen5 drive would sell sequential bandwidth that nothing on this machine consumes.

### The faster drive is the one doing nothing

| Drive | Slot / link | Role | 24 h I/O |
|---|---|---|---|
| WD Blue SN570 2 TB | Chipset, PCIe 3.0 x4 (8 GT/s) | **Root filesystem** | 15.3 GiB read |
| WD_BLACK SN770 2 TB | **CPU-direct**, PCIe 4.0 (16 GT/s), `00:01.2 → 02:00.0` | Idle — 1.8 TB of NTFS (old Windows install + Recovery) | **0 bytes** |

The faster drive is on the faster slot doing nothing, while the slower drive on the slower slot is root. Any future storage change here is a **free swap of hardware already owned**, not a purchase.

### CPU is not the bottleneck either

A 150 ms single-thread burst reaches **5.54 GHz on the first burst** under `powersave` + `balance_performance`. There is no ramp-up penalty to eliminate, which independently confirms §5's note that switching EPP to `performance` would gain nothing.

### The real measured slowness is firmware POST

`systemd-analyze` on the current boot:

```
1min 11.088s (firmware) + 3.739s (loader) + 1.701s (kernel)
  + 2.550s (initrd) + 20.722s (userspace) = 1min 39.802s
```

**71.1 s of a 99.8 s boot is firmware POST** — DDR5 memory training at 5600 MT/s, re-run on every cold boot. That is 71 % of boot time spent before the kernel exists.

**Untried lever:** BIOS **Memory Context Restore = Enabled** (with **Power Down Enable = Disabled**). This caches the training result and typically cuts AM5 POST to ~15–20 s. It affects the cold-boot training path only — not S3 resume — and reverts by simply re-disabling it. Some AM5 boards trade a small amount of cold-boot reliability for it, which is why it is flagged as untried rather than recommended outright.

Userspace's largest single item is `plymouth-quit-wait.service` at 10.7 s of the 20.7 s. Note that `dnf5-automatic.service` showing 66 s in `systemd-analyze blame` is a **red herring** — its `WantedBy=` is empty and it is timer-triggered, so it never blocks boot. Confirmed via `systemd-analyze critical-chain`.

### Why app launches still feel slow

The heavy apps are all Electron/Chromium — Discord (607 MB flatpak), Spotify, Element, Steam, plus a 1.6 GB Python RSS process. Their launch cost is V8 parse plus Chromium init: **single-thread bound at clocks that are already maxed**, with the disk idle. No hardware purchase addresses this.

The two levers that would actually help:

1. **Keep them resident** rather than relaunching them.
2. **Protect page cache** — 30 GiB total with 9.2 GiB in use and 1.6 GiB already in zram (lzo-rle, swappiness 60).

---

## Cumulative effect

- **Stability:** a hard freeze roughly every 13 suspends → none in 24 cycles
- **Multicore CPU:** ~1.9× throughput, from a half-speed thermally-capped state to full boost
- **Memory:** +16.7% clock, at rated spec for the first time
- **Firmware:** 16 months of skipped updates closed
- **Storage:** confirmed *not* a bottleneck — and the idle SN770 found sitting on the faster slot

Three of the five issues — the keyboard, the BIOS, and the cooler — were **silent failures**. Nothing logged an error. The keyboard looked like a flaky cable, the BIOS looked fine because the machine booted, and the CPU simply ran slow with no indication anything was wrong. They were found by measuring against what the hardware *should* do rather than by chasing error messages.

---

## Remaining opportunities

Both were blocked by the thermal cap and are now unblocked:

1. **PBO Curve Optimizer undervolt** — highest-value remaining knob, with ~16 °C of thermal headroom to work with.
2. **Memory beyond 6000 MT/s** — past the XMP profile, so it requires manual timings.

Added by the 2026-09-26 investigation:

3. **BIOS Memory Context Restore = Enabled** — the single largest remaining wall-clock win: potentially ~50 s off every cold boot. Cold-boot path only; trivially reversible.
4. **Swap root onto the idle SN770** — the CPU-direct Gen4 drive is doing nothing. Won't speed up app launches (§6), but it is free and it puts the better drive to work. Requires dealing with the 1.8 TB of old Windows/Recovery NTFS still on it.
5. **Reduce `plymouth-quit-wait`** — 10.7 s of the 20.7 s userspace boot.

Explicitly ruled out by measurement: **buying any SSD** (§6).

Not worth pursuing: switching the `amd-pstate-epp` driver from `balance_performance` to `performance`. The current `powersave` governor already reaches full 5.3 GHz boost, so there is no headroom being left on the table.

## Cleanup completed

The debug instrumentation from the 2026-09-12 investigation was removed on 2026-09-25, the root cause having been found three days later:

- `/etc/sysctl.d/99-freeze-debug.conf` renamed to `.disabled` (sysctls revert to vendor defaults at next boot)
- `kdump.service` disabled and stopped
- `crashkernel=2G-64G:256M,64G-:512M` removed from all 4 BLS entries, reclaiming 256 MB of boot-reserved RAM at next reboot

Verified after the change that both production boot arguments survived on all four entries: `nvme_core.default_ps_max_latency_us=0` and `mem_sleep_default=deep`. `crashkernel` was only ever present in the BLS entries (not `/etc/default/grub` or `/etc/kernel/cmdline`), so newly installed kernels will not reintroduce it.

## Method note

Figures in this report come from direct measurement on 2026-09-25 and 2026-09-26 (`stress-ng`, `turbostat`, `sensors`, `dmidecode`, `lspci`, `lsusb`, `dd`, `systemd-analyze`, `/proc/pressure/io`) and from the systemd journal spanning 2026-07-03 to 2026-09-25. BIOS versions are from the kernel DMI line recorded at each boot. Freeze counts are boots that terminated with no clean-shutdown record.

Two items are partly reconstructed rather than fully evidenced: the keyboard fix and the ~2026-07-05 sleep-profile attempt both predate the retained session transcripts. The keyboard topology described above is current and directly measured; the original diagnosis is inferred from that state plus the user's recollection.

---

## State re-verified 2026-09-26

Spot-checked live on the running system while writing this copy of the report:

| Check | Value |
|---|---|
| BIOS | `1681`, dated `06/18/2026` — the update from §2 is live |
| Sleep mode | `s2idle [deep]` — `deep` selected, as intended by §3 |
| Kernel cmdline | `mem_sleep_default=deep nvme_core.default_ps_max_latency_us=0` both present |
| Keyboard | `Bus 007 Device 004: 24f0:0140 Metadot Das Keyboard 4` — still on the CPU-direct controller (§1) |
| Idle temps | Tctl **49.9 °C**, Tccd1 36.2 °C, Tccd2 34.5 °C — matches the post-service numbers in §5 |
| kdump | `disabled` / `inactive`; `99-freeze-debug.conf.disabled` — cleanup held |
| Uptime | 1 day 3 h, booted 2026-09-25 18:34 |

One loose end: `crashkernel=2G-64G:256M,64G-:512M` is **still present in `/proc/cmdline`**. This is expected and not a regression — it was removed from the BLS entries on 2026-09-25, but the machine has not cold-booted since (current boot predates the edit by minutes). The 256 MB will be reclaimed on the next reboot. Worth re-checking `cat /proc/cmdline` after the next boot to confirm it is gone.