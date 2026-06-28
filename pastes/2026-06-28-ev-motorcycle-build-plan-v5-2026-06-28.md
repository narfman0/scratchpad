---
title: "EV Motorcycle Build Plan v5 — 2026-06-28"
date: 2026-06-28 16:26:32 +0000
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

## Drivetrain Options — All 96V

### Option A — Hub Drive (QS273) — Highest Power

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

**Pros:** Highest power (~12kW), no chain, DC-DC included, packaged kit

**Cons:** Most expensive, tire clearance TBD, swingarm spacers needed

### Option B — Mid-Drive QS165 (Recommended mid-drive)

| Component | Spec | Notes |
| --- | --- | --- |
| Motor | QS165 V3 | 5kW rated / 10kW peak |
| Controller | Fardriver ND96680 | 96V, 680A peak |
| Display | DKD display | Included |
| Throttle | T08 | Included |
| Output sprocket | 428-pitch | Switch full drivetrain to 428 recommended |
| Rear wheel | Stock retained | No tire clearance issue |
| Source | AliExpress item 3256809152484076 | Verify harness included |
| Price | $797 | Complete kit |

**Pros:** $700 cheaper than hub, keeps stock wheel, full kit

**Cons:** Less power than QS273 or ME1302, chain work needed, frame mount TBD

### Option C — Mid-Drive QS138 (Budget fallback)

| Component | Spec | Notes |
| --- | --- | --- |
| Motor | QS138 V3 | 4kW rated / 7.5kW peak |
| Controller | Fardriver ND96530 | 96V, 530A peak |
| Rear wheel | Stock retained | No tire clearance issue |
| Source A | AliExpress item 3256811876286767 | $717, harness TBD |
| Source B | AliExpress item 3256812196354498 | $659, different seller |

**Cons:** Least power; QS165 only $80 more with full kit — hard to justify

### Option D — US-Sourced: Motenergy ME1302 + Kelly KLS96601

Mid-drive configuration using US-available components.

| Component | Spec | Price | Link |
| --- | --- | --- | --- |
| Motor: ME1302 | 96V, 130A cont / 450A peak (~12.5kW), water-cooled | $799 | kellycontroller.com/shop/me1302/ |
| Controller: KLS96601-8080NPS | 96V, 600A peak, sinusoidal BLDC | ~$400-500 est. | kellycontroller.com/shop/kls-8080n-nps/ |
| Water cooling kit | Pump + radiator + hoses | ~$100-150 | Various |
| Display: Kelly TFT 750C | 24-120V speedometer | $99-119 | kellycontroller.com |
| Throttle | Hall effect | ~$25 | Various |
| Custom motor mount + output sprocket | Fab work required | ~$100-300 est. | Local machine shop |
| **Est. total** | | **~$1,600-1,900+** | |

**Pros:** US-sourced (fast shipping, English support, easy returns), power matches QS273, mid-drive keeps stock wheel

**Cons:** Water cooling required, custom mounting fabrication needed, most expensive option, sin/cosine sensor (not hall) limits controller options

**Note:** Most Motenergy motors cap at 48-72V. ME1302 is the only one rated to 96V.

## Power Comparison

| Motor | Continuous | Peak | Cooling | Source |
| --- | --- | --- | --- | --- |
| QS138 mid | ~4kW | ~7.5kW | Air | AliExpress |
| QS165 mid | ~5kW | ~10kW | Air | AliExpress |
| QS273 hub | ~12kW+ | Higher | Air | SiAECOSYS |
| ME1302 mid | ~12.5kW | Higher | Water req'd | Kelly (US) |

**Note:** Gear ratios multiply torque but not power. The watt ceiling is determined by the motor rating, not the sprocket ratio.

## Chain and Sprocket (Mid-Drive Options B/C/D)

QS mid-drive kits ship with 428-pitch output sprockets. VN750 stock uses 530 chain.

**Recommended:** Switch full drivetrain to 428 — replace rear wheel sprocket with 428-pitch unit. 428 is adequate for 5-10kW, cleaner since drivetrain is being rebuilt anyway.

Alternative: have a machine shop bore a 530-pitch sprocket to fit the motor output shaft.

## Other Components Needed

| Component | Option A (Hub) | Options B/C (Mid) | Option D (US) | Est. cost |
| --- | --- | --- | --- | --- |
| DC-DC 12V | Included (Damon) | Source separately | Source separately | ~$30-50 |
| 96V charger | Source separately | Source separately | Source separately | ~$150-300 |
| Throttle | Verify | Included (QS165) | Included | ~$25 if separate |
| Brake cutoff switches | Source | Source | Source | ~$15-25 |
| Wiring harness | Included (Damon) | Verify (QS165) | Custom | ~$40-80 if separate |
| Display | SCJ5066-1 (Damon) | Included (QS165) | Kelly TFT 750C | ~$30-119 if separate |

## Open Questions

| Question | Affects |
| --- | --- |
| Does 180mm tire clear swingarm with 17 inch hub wheel? | Option A go/no-go |
| AliExpress QS165 — harness included? | Option B true cost |
| Damon's 96V mid-drive price with harness + throttle | Option B Damon comparison |
| Chain pitch: full 428 switch vs 530 output sprocket? | Options B/C/D |
| QS165/QS138 frame mount fitment in VN750 engine bay | Options B/C go/no-go |
| Kelly KLS96601 exact price | Option D cost |

## Pending Actions

- [ ] Eyeball tire clearance: hold ~190mm-wide object in swingarm
- [ ] Email Damon: 96V mid-drive price with harness + throttle; 530 sprocket option; confirm SCJ5066-1 + DC-DC in hub kit
- [ ] Check AliExpress QS165 listing for harness inclusion (item 3256809152484076)
- [x] Order battery — done 2026-06-28
- [x] Mail DMV packet — done 2026-06-27

## DMV and Registration Status

- **Goal:** Virginia antique plates (qualifies: 25+ years old)
- **Completed:** Title filled out, insurance obtained, packet mailed 2026-06-27
- **Pending:** Await DMV response
- **Note:** 4.15% SUT applies, $75 minimum, $140 total check sent
- **Strategy:** Registered before conversion while bike is ridable