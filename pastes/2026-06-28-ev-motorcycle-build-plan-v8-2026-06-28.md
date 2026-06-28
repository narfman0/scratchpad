---
title: "EV Motorcycle Build Plan v8 — 2026-06-28"
date: 2026-06-28 18:24:43 +0000
author: pinky
---

# 1994 Kawasaki VN750 Vulcan — EV Conversion Plan

*Updated: 2026-06-28 — v8: harness and DC-DC confirmed included in Option A*

## Vehicle Specs

- **Frame:** 1994 Kawasaki VN750 Vulcan
- **Swingarm width (OLD):** 260mm (measured bolt-to-spacer-end, includes drum brake)
- **Engine cavity:** 220mm wide x 500mm tall x 300mm deep
- **Final drive:** **Shaft drive** (engine → gearbox → driveshaft through swingarm → bevel gear → rear wheel)
- **Stock rear tire:** ~150mm width, ~25mm gap to right swingarm wall
- **System voltage:** 96V (committed)

> **Key discovery (2026-06-28):** The VN750 is shaft-driven, not chain-driven. Hub drive (Option A) is unaffected — it replaces the rear wheel entirely and bypasses the original drivetrain. Mid-drive (Option B) requires a custom spline coupler to the shaft drive input.

## Battery — ORDERED

| Spec | Value |
| --- | --- |
| Chemistry | NMC Li-ion Ternary (not LiFePO4) |
| Capacity | 40Ah |
| Voltage | 96V nominal |
| BMS | 300A continuous |
| Dimensions | 165 x 240 x 270mm |
| Source | AliExpress item 3256804576924652 |
| Price | ~$731 |
| Status | **Ordered 2026-06-28** |

## Drivetrain Architecture — VN750 Shaft Drive

```
Original: Engine → 5-speed gearbox → driveshaft (through swingarm) → bevel gear → rear wheel

EV Option A (Hub):
  QS273 hub motor laced into new rear wheel (shaft drive removed entirely)

EV Option B (Spline coupler mid-drive):
  Electric motor → custom spline coupler → shaft drive input → existing driveshaft → bevel gear → rear wheel
```

## Drivetrain Options — All 96V

### Option A — Hub Drive (QS273 V4 70H + ND961800) — **Recommended**

| Component | Spec | Notes |
| --- | --- | --- |
| Motor | QS273 V4 **70H** hub motor | 12kW, larger stator |
| Controller | **Fardriver ND961800** | 96V, **1800A peak** |
| Wheel | 17x6" laced | Tire 190/50-17 |
| OLD | 230mm | Fits 260mm swingarm with 15mm spacers each side |
| Tire width | 190mm | Physical clearance check needed |
| Top speed | 157 km/h (97 mph) @ 96V | |
| Bluetooth | Included | |
| Wiring harness | **Included** | With relay, flasher, start button |
| DC-DC converter | **Included** | 96V → 12V |
| Display | Not included | Source separately ~$30–119 |
| Throttle | Not included | Source separately ~$25 |
| Source | cnqsmotor.com (Damon / SiAECOSYS) | Select **Combo 2** for 96V/ND961800 |
| **Price** | **$1,490** | Sale from $1,694 |
| Link | [cnqsmotor.com product page](https://www.cnqsmotor.com/product/siaecosys-17x6-0inch-70h-12000w-v4-96v-157kph-hub-motor-with-nd721800-nd961800-controller-powertrain-kits-for-high-power-electric-motorcycle/) | |

> **Important:** Select **Combo 2** on the product page to get the ND961800 (96V) controller. Combo 1 is the ND721800 (72V).

**Pros:** Highest power, 1800A peak, harness + DC-DC included, bypasses shaft drive entirely, cleanest path

**Cons:** Display and throttle are add-ons; tire clearance TBD; swingarm spacers needed

---

### Option B — Mid-Drive via Spline Coupler

Remove engine and gearbox. Keep shaft drive. Couple motor to shaft drive input via custom spline coupler.

- Machine shop makes coupler: motor output shaft → VN750 driveshaft input spline (~$300–600)
- Motor mounting plate in engine bay (~$200–400)
- No chain — fully shaft-driven EV; only reduction is rear bevel gear (~3:1)

| Motor candidate | Power | Price | Notes |
| --- | --- | --- | --- |
| QS165 V3 | 5kW / 10kW peak | $797 (kit) | Air-cooled, AliExpress |
| ME1302 | ~12.5kW | $799 (motor only) | Water-cooled, US-sourced |

**Cons:** Custom coupler required, more total cost and work than Option A, single fixed ratio

## All-In Cost Estimate

| Item | Option A | Notes |
| --- | --- | --- |
| Motor + controller kit | $1,490 | Combo 2, ND961800 |
| Battery | $731 | Ordered |
| Display | ~$30–119 | SCJ5066-1 or similar |
| Throttle | ~$25 | Hall effect |
| Brake cutoff switches | ~$15–25 | |
| 96V charger | ~$150–300 | |
| Swingarm spacers | ~$20–40 | 15mm each side |
| Misc wiring/connectors | ~$30–50 | |
| **Total estimate** | **~$2,490–2,780** | Before labor/fab |

## Open Questions

| Question | Affects |
| --- | --- |
| Does 190mm tire clear swingarm? | Option A go/no-go — hold ~190mm object in swingarm |
| Confirm Combo 2 = ND961800 96V with Damon | Option A ordering |
| VN750 driveshaft input spline specs | Option B feasibility |
| VN750 rear bevel gear ratio | Option B speed calculation |

## Pending Actions

- [ ] Physical check: hold ~190mm-wide object in swingarm (Option A tire clearance)
- [ ] Email Damon: confirm Combo 2 is ND961800 96V; confirm harness + DC-DC included
- [x] Order battery — done 2026-06-28
- [x] Mail DMV packet — done 2026-06-27

## DMV and Registration Status

- **Goal:** Virginia antique plates (qualifies: 25+ years old)
- **Completed:** Title filled out, insurance obtained, packet mailed 2026-06-27
- **Pending:** Await DMV response
- **Note:** 4.15% SUT applies, $75 minimum, $140 total check sent
- **Strategy:** Registered before conversion while bike is ridable