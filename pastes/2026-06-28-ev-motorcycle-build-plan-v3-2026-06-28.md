---
title: "EV Motorcycle Build Plan v3 — 2026-06-28"
date: 2026-06-28 14:21:52 +0000
author: pinky
---

# 1994 Kawasaki VN750 Vulcan — EV Conversion Plan

*Updated: 2026-06-28*

## Vehicle Specs

- **Frame:** 1994 Kawasaki VN750 Vulcan
- **Swingarm width (OLD):** 260mm (measured bolt-to-spacer-end, includes drum brake)
- **Engine cavity:** 220mm wide × 500mm tall × 300mm deep
- **Stock chain pitch:** 530
- **Stock rear tire:** ~150mm width, ~25mm gap to right swingarm wall

## Battery — Decided

| Spec | Value |
| --- | --- |
| Chemistry | NMC Li-ion Ternary (not LiFePO4) |
| Capacity | 40Ah |
| Voltage | 96V nominal |
| BMS | 300A continuous |
| Dimensions | 165 × 240 × 270mm |
| Cavity fit | ~55mm width margin, ~30mm depth margin |
| Source | AliExpress item 3256804576924652 |
| Price | ~$731 |

Seller confirmed dimensions 165x240x270mm. Engine cavity 220x500x300mm — comfortable fit on all axes.

## Drivetrain Options

Three options remain under consideration. All 96V nominal.

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

**Pros:** Highest power, no chain, simpler drivetrain, DC-DC included

**Cons:** Most expensive, 17 inch custom wheel, tire clearance TBD, needs swingarm spacers

### Option B — Mid-Drive QS165 (Recommended mid-drive)

| Component | Spec | Notes |
| --- | --- | --- |
| Motor | QS165 V3 | 5kW rated / 10kW peak |
| Controller | Fardriver ND96680 | 96V, 680A peak |
| Display | DKD display | Included in kit |
| Throttle | T08 | Included in kit |
| Output sprocket | 428-pitch | Chain switch likely needed |
| Rear wheel | Stock retained | No tire clearance issue |
| Source | AliExpress | Item TBD — verify harness included |
| Price | $797 | Complete kit with display + throttle |

**Pros:** $700 cheaper than hub kit, keeps stock wheel, 10kW peak, full kit

**Cons:** Less power than QS273, chain/sprocket work needed, frame mount TBD

### Option C — Mid-Drive QS138 (Budget)

| Component | Spec | Notes |
| --- | --- | --- |
| Motor | QS138 V3 | 4kW rated / 7.5kW peak |
| Controller | Fardriver ND96530 | 96V, 530A peak |
| Display | Not confirmed | ~$30-50 standalone |
| Throttle | Not confirmed | Verify with seller |
| Output sprocket | 428-14T | Same chain concern as Option B |
| Rear wheel | Stock retained | No tire clearance issue |
| Source | AliExpress item 3256811876286767 | |
| Price | $717 | Harness inclusion TBD |

**Pros:** Cheapest option, keeps stock wheel

**Cons:** Least power, harness likely not included, QS165 only $80 more with full kit

## Power Comparison

| Motor | Continuous power | Peak | Best use |
| --- | --- | --- | --- |
| QS138 mid-drive | ~4kW | ~7.5kW | Light street |
| QS165 mid-drive | ~5kW | ~10kW | Street + hills |
| QS273 hub | ~12kW+ | Higher | Strong highway, loaded |

**Important:** Gear ratios multiply wheel torque but not power. A 3:1 chain reduction triples low-speed pulling force but the watt ceiling is the motor rating regardless of sprocket choice.

## Chain and Sprocket Notes (Mid-Drive)

Mid-drive kits ship with 428-pitch output sprockets. VN750 stock uses 530 chain. Two options:

1. **Switch full drivetrain to 428** — replace rear wheel sprocket with 428-pitch unit. 428 is adequate for 5-10kW. Recommended since drivetrain is being rebuilt anyway.

2. **Source 530 output sprocket for motor** — fit motor output shaft bore. Keeps stock rear sprocket. More complex to source.

## Other Components Needed

| Component | Option A (Hub) | Option B/C (Mid) | Est. cost |
| --- | --- | --- | --- |
| DC-DC 12V converter | Included (Damon) | Source separately | ~$30-50 |
| 96V charger | Source separately | Source separately | ~$150-300 |
| Throttle | Verify | Included (QS165) | ~$15-30 if separate |
| Brake cutoff switches | Source | Source | ~$15-25 |
| Wiring harness | Included (Damon) | Verify (QS165) | ~$40-80 if separate |
| Display | SCJ5066-1 (Damon) | Included (QS165) | ~$30-50 if separate |

## Open Questions

| Question | Affects |
| --- | --- |
| Does 180mm tire clear swingarm with 17 inch hub wheel? | Option A decision |
| AliExpress QS165 listing — harness included? | Option B true cost |
| Damon price for 96V mid-drive with harness and throttle | Option B vs Damon |
| Chain pitch: full 428 switch vs 530 output sprocket? | Option B/C |
| QS165/QS138 frame mount fitment in VN750 engine bay | Option B/C go/no-go |

## Pending Actions

- [ ] Eyeball tire clearance: hold ~190mm-wide object in swingarm
- [ ] Email Damon: 96V mid-drive price with harness + throttle; 530 sprocket availability; confirm SCJ5066-1 + DC-DC in hub kit
- [ ] Check AliExpress QS165 listing for harness inclusion (item 3256809152484076)
- [ ] Order battery (AliExpress item 3256804576924652)
- [ ] Mail DMV packet: VSA 14 + VSA 10B + signed title + proof of insurance + $140 check to DMV

## DMV and Registration Status

- **Goal:** Virginia antique plates (qualifies: 25+ years old)
- **Completed:** Title filled out, insurance obtained
- **Pending:** Mail the full packet above
- **Note:** 4.15% SUT applies, $75 minimum included in the $140 total
- **Strategy:** Register before conversion while bike is still ridable