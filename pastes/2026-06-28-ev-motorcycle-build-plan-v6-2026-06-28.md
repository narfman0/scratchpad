---
title: "EV Motorcycle Build Plan v6 — 2026-06-28"
date: 2026-06-28 17:38:43 +0000
author: pinky
---

# 1994 Kawasaki VN750 Vulcan — EV Conversion Plan

*Updated: 2026-06-28 — v6: shaft drive discovery, revised option analysis*

## Vehicle Specs

- **Frame:** 1994 Kawasaki VN750 Vulcan
- **Swingarm width (OLD):** 260mm (measured bolt-to-spacer-end, includes drum brake)
- **Engine cavity:** 220mm wide x 500mm tall x 300mm deep
- **Final drive:** **Shaft drive** (engine → gearbox → driveshaft through swingarm → bevel gear → rear wheel)
- **Stock rear tire:** ~150mm width, ~25mm gap to right swingarm wall
- **System voltage:** 96V (committed)

> **Key discovery (2026-06-28):** The VN750 is shaft-driven, not chain-driven. This significantly affects mid-drive planning. Hub drive (Option A) is unaffected — it replaces the rear wheel entirely and bypasses the original drivetrain. Mid-drive options require either converting to chain drive or coupling the motor to the shaft drive input via a custom spline coupler.

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

## Drivetrain Architecture — VN750 Shaft Drive

```
Original: Engine → 5-speed gearbox → driveshaft (through swingarm) → bevel gear → rear wheel

EV Option A (Hub):
  QS273 hub motor laced into new rear wheel → rear wheel (shaft drive removed entirely)

EV Option B (Spline coupler mid-drive):
  Electric motor → custom spline coupler → shaft drive input → existing driveshaft → existing bevel gear → rear wheel
  (gearbox removed with engine; bevel gear final reduction preserved)

EV Option C (Chain conversion mid-drive):
  Electric motor → output sprocket → new chain → new rear sprocket bolted to rear wheel
  (entire shaft drive system removed)
```

## Drivetrain Options — All 96V

### Option A — Hub Drive (QS273) — **Recommended: Cleanest Path**

| Component | Spec | Notes |
| --- | --- | --- |
| Motor | QS273 V3 hub motor | ~12kW rated |
| Controller | Fardriver ND961800 | 96V, 1800A peak |
| Wheel | 17 inch laced by Damon | Only size offered |
| OLD | 230mm | Fits 260mm swingarm with 15mm spacers each side |
| Tire width | 180mm recommended | 190mm marginal — needs physical check |
| Display | SCJ5066-1 | Confirmed available |
| DC-DC | Included | Per Damon email |
| Source | SiAECOSYS / damon@siaecosys.com | |
| Est. price | ~$1,490 | |

**Pros:** Highest power (~12kW), no chain, DC-DC included, packaged kit, bypasses shaft drive entirely — no coupler or conversion needed

**Cons:** Most expensive, tire clearance TBD (hold ~190mm object in swingarm to check), swingarm spacers needed

---

### Option B — Mid-Drive via Spline Coupler (QS165 or ME1302)

Remove the engine and gearbox. Keep the existing shaft drive system. Couple the electric motor directly to the shaft drive input using a custom-fabricated spline coupler.

**How it works:**
- Machine shop fabricates an adapter: motor output shaft → VN750 driveshaft input spline
- Motor replaces the engine output; driveshaft and bevel gear remain in place
- No chain, no chain maintenance — fully shaft-driven EV
- Only gear reduction is the rear bevel gear ratio (~3:1)

**Fabrication needed:**
- Disassemble driveshaft input to measure spline specs
- Machine shop makes spline coupler (~$300–600 for the part)
- Motor mounting plate in engine bay (~$200–400)
- One fitting iteration likely needed for alignment

**Timeline/cost:** ~$500–1,000 total fab cost; not a single afternoon, but not impossibly expensive. Legitimate approach used by other shaft-drive EV conversions.

| Motor candidate | Power | Price | Notes |
| --- | --- | --- | --- |
| QS165 V3 | 5kW / 10kW peak | $797 (kit) | Air-cooled, AliExpress |
| ME1302 | ~12.5kW | $799 (motor only) | Water-cooled, US-sourced, Kelly |

**Pros:** Chainless drivetrain preserved, no chain maintenance ever, uses existing swingarm/bevel gear

**Cons:** Custom spline coupler required (machine shop), no gearbox (single fixed ratio), motor RPM range must pair well with final drive ratio

---

### Option C — Mid-Drive with Chain Conversion (QS165 / QS138)

Remove the shaft drive system entirely. Add a chain drive: motor output sprocket → chain → rear wheel sprocket.

#### Option C1 — QS165 (Recommended if chain conversion chosen)

| Component | Spec | Notes |
| --- | --- | --- |
| Motor | QS165 V3 | 5kW rated / 10kW peak |
| Controller | Fardriver ND96680 | 96V, 680A peak |
| Display | DKD display | Included |
| Throttle | T08 | Included |
| Output sprocket | 428-pitch | Switch full drivetrain to 428 |
| Rear wheel | Stock retained | No tire clearance issue |
| Source | AliExpress item 3256809152484076 | Verify harness included |
| Price | $797 | Complete kit |

#### Option C2 — QS138 (Budget fallback)

| Component | Spec | Notes |
| --- | --- | --- |
| Motor | QS138 V3 | 4kW rated / 7.5kW peak |
| Controller | Fardriver ND96530 | 96V, 530A peak |
| Source A | AliExpress item 3256811876286767 | $717 |
| Source B | AliExpress item 3256812196354498 | $659 |

**Cons for C1/C2:** Shaft drive must be removed and replaced — most fabrication of any option. Chain adds ongoing maintenance. QS138 is the least powerful; QS165 only $80 more.

---

### Option D — US-Sourced: Motenergy ME1302 + Kelly KLS96601

Can be paired with either spline coupler (Option B) or chain conversion (Option C).

| Component | Spec | Price |
| --- | --- | --- |
| Motor: ME1302 | 96V, ~12.5kW, water-cooled | $799 |
| Controller: KLS96601-8080NPS | 96V, 600A peak | ~$400–500 |
| Water cooling kit | Pump + radiator + hoses | ~$100–150 |
| Display: Kelly TFT 750C | 24-120V | $99–119 |
| Custom mount + coupler/sprocket | Fab required | ~$300–600 |
| **Est. total** | | **~$1,700–2,100+** |

**Pros:** US-sourced (fast shipping, English support), power matches QS273, works with either drivetrain path

**Cons:** Water cooling required, most expensive, custom mounting always needed

**Note:** Most Motenergy motors cap at 48–72V. ME1302 is the only one rated to 96V.

## Power Comparison

| Option | Motor | Continuous | Peak | Cooling | Drivetrain path |
| --- | --- | --- | --- | --- | --- |
| A | QS273 hub | ~12kW+ | Higher | Air | Hub (bypasses shaft drive) |
| B | QS165 mid | ~5kW | ~10kW | Air | Spline coupler or chain |
| B | QS138 mid | ~4kW | ~7.5kW | Air | Spline coupler or chain |
| D | ME1302 mid | ~12.5kW | Higher | Water req'd | Spline coupler or chain |

**Note:** Gear ratios multiply torque but not power. Watt ceiling is set by motor rating, not ratio.

## Chain and Sprocket (Chain Conversion Only — Options C/D chain path)

Only relevant if the shaft drive is removed and chain drive is added. QS mid-drive kits ship with 428-pitch output sprockets; VN750 stock uses 530.

**Recommended if converting:** Switch full drivetrain to 428 — replace rear wheel sprocket with 428-pitch unit. Adequate for 5–10kW.

## Option Ranking by Simplicity

| Rank | Option | Why |
| --- | --- | --- |
| 1 | Hub drive (A) | No coupler, no chain, packaged kit — shaft drive discovery makes this even cleaner |
| 2 | Mid-drive + spline coupler (B) | Preserves shaft drive elegantly, chainless result, but requires custom fab |
| 3 | Mid-drive + chain conversion (C/D) | Most fabrication; shaft drive removal adds work vs. just adding chain to a chain-drive bike |

## Other Components Needed

| Component | Option A (Hub) | Options B/C (Mid) | Option D (US) | Est. cost |
| --- | --- | --- | --- | --- |
| DC-DC 12V | Included (Damon) | Source separately | Source separately | ~$30–50 |
| 96V charger | Source separately | Source separately | Source separately | ~$150–300 |
| Throttle | Verify | Included (QS165) | Included | ~$25 if separate |
| Brake cutoff switches | Source | Source | Source | ~$15–25 |
| Wiring harness | Included (Damon) | Verify (QS165) | Custom | ~$40–80 if separate |
| Display | SCJ5066-1 (Damon) | Included (QS165) | Kelly TFT 750C | ~$30–119 if separate |

## Open Questions

| Question | Affects |
| --- | --- |
| Does 180mm tire clear swingarm with 17 inch hub wheel? | Option A go/no-go |
| AliExpress QS165 — harness included? | Option C1 true cost |
| VN750 driveshaft input spline specs (count, diameter, pitch) | Option B feasibility |
| QS165 frame mount fitment in VN750 engine bay | Options B/C go/no-go |
| VN750 rear bevel gear ratio — compatible with motor RPM range? | Option B speed calculation |
| Kelly KLS96601 exact price | Option D cost |

## Pending Actions

- [ ] Eyeball tire clearance: hold ~190mm-wide object in swingarm (Option A check)
- [ ] Disassemble driveshaft input and measure spline specs if pursuing Option B
- [ ] Email Damon: 96V mid-drive price with harness + throttle; confirm SCJ5066-1 + DC-DC in hub kit
- [ ] Check AliExpress QS165 listing for harness inclusion (item 3256809152484076)
- [x] Order battery — done 2026-06-28
- [x] Mail DMV packet — done 2026-06-27

## DMV and Registration Status

- **Goal:** Virginia antique plates (qualifies: 25+ years old)
- **Completed:** Title filled out, insurance obtained, packet mailed 2026-06-27
- **Pending:** Await DMV response
- **Note:** 4.15% SUT applies, $75 minimum, $140 total check sent
- **Strategy:** Registered before conversion while bike is ridable