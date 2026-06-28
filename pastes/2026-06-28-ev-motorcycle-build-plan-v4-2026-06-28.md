---
title: "EV Motorcycle Build Plan v4 — 2026-06-28"
date: 2026-06-28 15:41:04 +0000
author: pinky
---

# 1994 Kawasaki VN750 Vulcan — EV Conversion Plan

*Updated: 2026-06-28*

## Vehicle Specs

- **Frame:** 1994 Kawasaki VN750 Vulcan
- **Swingarm width (OLD):** 260mm (measured bolt-to-spacer-end, includes drum brake)
- **Engine cavity:** 220mm wide x 500mm tall x 300mm deep
- **Stock chain pitch:** 530
- **Stock rear tire:** ~150mm width, ~25mm gap to right swingarm wall
- **System voltage:** 96V (committed)

## Battery — ORDERED

| Spec | Value |
| --- | --- |
| Chemistry | NMC Li-ion Ternary (not LiFePO4) |
| Capacity | 40Ah |
| Voltage | 96V nominal |
| BMS | 300A continuous |
| Dimensions | 165 x 240 x 270mm |
| Cavity fit | ~55mm width margin, ~30mm depth margin |
| Source | AliExpress item 3256804576924652 |
| Price | ~$731 |
| Status | **Ordered 2026-06-28** |

Dimensions confirmed by seller. Engine cavity 220x500x300mm — comfortable fit on all axes. 96V is now the fixed system voltage.

## Drivetrain Options

All options 96V. Motor/controller decision still open.

### Option A — Hub Drive (QS273) — Highest Power

| Component | Spec | Notes |
| --- | --- | --- |
| Motor | QS273 V3 hub motor | ~12kW rated |
| Controller | Fardriver ND961800 | 96V, 1800A peak |
| Wheel | 17 inch laced by Damon | Only size offered |
| OLD | 230mm | Fits 260mm swingarm with 15mm spacers each side |
| Tire width | 180mm recommended | 190mm marginal — needs physical check |
| Display | SCJ5066-1 | Confirmed available |
| DC-DC converter | Included | Per Damon email |
| Chain | N/A | Direct hub drive |
| Source | SiAECOSYS / damon@siaecosys.com | |
| Est. drivetrain price | ~$1,490 | |

**Pros:** Highest power (~12kW), no chain, simpler drivetrain, DC-DC included

**Cons:** Most expensive, 17 inch custom wheel, tire clearance TBD, needs swingarm spacers

### Option B — Mid-Drive QS165 (Recommended mid-drive)

| Component | Spec | Notes |
| --- | --- | --- |
| Motor | QS165 V3 | 5kW rated / 10kW peak |
| Controller | Fardriver ND96680 | 96V, 680A peak |
| Display | DKD display | Included in kit |
| Throttle | T08 | Included in kit |
| Output sprocket | 428-pitch | Full drivetrain switch to 428 recommended |
| Rear wheel | Stock retained | No tire clearance issue |
| Source | AliExpress item 3256809152484076 | Verify harness included |
| Price | $797 | Complete kit with display + throttle |

**Pros:** $700 cheaper than hub kit, keeps stock wheel, 10kW peak, full kit

**Cons:** Less power than QS273, chain/sprocket work needed, frame mount TBD

### Option C — Mid-Drive QS138 (Budget fallback)

| Component | Spec | Notes |
| --- | --- | --- |
| Motor | QS138 V3 | 4kW rated / 7.5kW peak |
| Controller | Fardriver ND96530 | 96V, 530A peak |
| Output sprocket | 428-14T | Same chain concern as Option B |
| Rear wheel | Stock retained | No tire clearance issue |
| Source | AliExpress item 3256811876286767 | |
| Price | $717 | Harness likely not included |

**Pros:** Cheapest drivetrain

**Cons:** Least power, harness not confirmed; QS165 is only $80 more with full kit

## Power Comparison

| Motor | Continuous | Peak | Notes |
| --- | --- | --- | --- |
| QS138 mid-drive | ~4kW | ~7.5kW | Budget fallback only |
| QS165 mid-drive | ~5kW | ~10kW | Recommended mid-drive |
| QS273 hub | ~12kW+ | Higher | Highest power option |

**Note:** Gear ratios multiply wheel torque but not power. The watt ceiling stays at the motor rating regardless of sprocket choice.

## Chain and Sprocket Notes (Mid-Drive)

Mid-drive kits ship with 428-pitch output sprockets. VN750 stock uses 530 chain.

**Recommended:** Switch full drivetrain to 428 — replace rear wheel sprocket with 428-pitch unit. 428 is adequate for 5-10kW and results in cheaper chain/sprockets going forward. Clean solution since drivetrain is being rebuilt anyway.

Alternative: ask Damon or a machine shop to bore a 530-pitch sprocket to fit the motor output shaft.

## Other Components Needed

| Component | Option A (Hub) | Option B/C (Mid) | Est. cost |
| --- | --- | --- | --- |
| DC-DC 12V converter | Included (Damon) | Source separately | ~$30-50 |
| 96V charger | Source separately | Source separately | ~$150-300 |
| Throttle | Verify with kit | Included (QS165) | ~$15-30 if separate |
| Brake cutoff switches | Source | Source | ~$15-25 |
| Wiring harness | Included (Damon) | Verify (QS165) | ~$40-80 if separate |
| Display | SCJ5066-1 (Damon) | Included (QS165) | ~$30-50 if separate |

## Open Questions

| Question | Affects |
| --- | --- |
| Does 180mm tire clear swingarm with 17 inch hub wheel? | Option A go/no-go |
| AliExpress QS165 — harness included? | Option B true cost |
| Damon price for 96V mid-drive with harness + throttle | Option A vs B comparison |
| Chain pitch: full 428 switch vs 530 output sprocket? | Option B/C |
| QS165/QS138 frame mount fitment in VN750 engine bay | Option B/C go/no-go |

## Pending Actions

- [ ] Eyeball tire clearance: hold ~190mm-wide object in swingarm
- [ ] Email Damon: 96V mid-drive price with harness + throttle; 530 sprocket option; confirm SCJ5066-1 + DC-DC in hub kit
- [ ] Check AliExpress QS165 listing for harness inclusion (item 3256809152484076)
- [x] Order battery — done 2026-06-28
- [ ] Mail DMV packet: VSA 14 + VSA 10B + signed title + proof of insurance + $140 check to DMV

## DMV and Registration Status

- **Goal:** Virginia antique plates (qualifies: 25+ years old)
- **Completed:** Title filled out, insurance obtained
- **Pending:** Mail the full packet above
- **Note:** 4.15% SUT applies, $75 minimum included in $140 total
- **Strategy:** Register before conversion while bike is still ridable