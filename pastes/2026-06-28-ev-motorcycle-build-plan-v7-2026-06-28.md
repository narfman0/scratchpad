---
title: "EV Motorcycle Build Plan v7 — 2026-06-28"
date: 2026-06-28 18:15:46 +0000
author: pinky
---

# 1994 Kawasaki VN750 Vulcan — EV Conversion Plan

*Updated: 2026-06-28 — v7: Option A corrected to ND961800 kit with direct link*

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
```

## Drivetrain Options — All 96V

### Option A — Hub Drive (QS273 V4 70H + ND961800) — **Recommended**

| Component | Spec | Notes |
| --- | --- | --- |
| Motor | QS273 V4 **70H** hub motor | 12kW, larger stator than standard |
| Controller | **Fardriver ND961800** | 96V, **1800A peak** |
| Wheel | 17x6" laced | Tire 190/50-17 |
| OLD | 230mm | Fits 260mm swingarm with 15mm spacers each side |
| Tire width | 190mm | Physical clearance check needed |
| Top speed | 157 km/h (97 mph) @ 96V | |
| Bluetooth | Included | |
| DC-DC | Not included | Source separately ~$30–50 |
| Display | Not included | Source separately ~$30–119 |
| Throttle | Not included | Source separately ~$25 |
| Harness | Not included | Source separately ~$40–80 |
| Source | cnqsmotor.com (Damon / SiAECOSYS) | Select **Combo 2** for 96V/ND961800 |
| **Price** | **$1,490** | Sale from $1,694 |
| Link | [cnqsmotor.com product page](https://www.cnqsmotor.com/product/siaecosys-17x6-0inch-70h-12000w-v4-96v-157kph-hub-motor-with-nd721800-nd961800-controller-powertrain-kits-for-high-power-electric-motorcycle/) | |

> **Important:** Select **Combo 2** on the product page to get the ND961800 (96V) controller. Combo 1 is the ND721800 (72V).

**Pros:** Highest power, 1800A peak controller, bypasses shaft drive entirely, no chain, packaged kit — cheaper than the ND96850 kit

**Cons:** DC-DC/display/throttle/harness are add-ons; tire clearance TBD; swingarm spacers needed

---

### Option B — Mid-Drive via Spline Coupler

Remove the engine and gearbox. Keep the existing shaft drive system. Couple the electric motor directly to the shaft drive input using a custom-fabricated spline coupler.

**How it works:**
- Machine shop fabricates an adapter: motor output shaft → VN750 driveshaft input spline
- Motor replaces the engine output; driveshaft and bevel gear remain in place
- No chain — fully shaft-driven EV
- Only gear reduction is the rear bevel gear ratio (~3:1)

**Fabrication needed:**
- Disassemble driveshaft input to measure spline specs
- Machine shop makes spline coupler (~$300–600 for the part)
- Motor mounting plate in engine bay (~$200–400)
- One fitting iteration likely needed for alignment

**Timeline/cost:** ~$500–1,000 total fab cost on top of motor/controller

| Motor candidate | Power | Price | Notes |
| --- | --- | --- | --- |
| QS165 V3 | 5kW / 10kW peak | $797 (kit) | Air-cooled, AliExpress |
| ME1302 | ~12.5kW | $799 (motor only) | Water-cooled, US-sourced, Kelly |

**Pros:** Chainless drivetrain, no chain maintenance, uses existing swingarm/bevel gear

**Cons:** Custom spline coupler required, no gearbox (single fixed ratio), more total cost and work than Option A

## Power Comparison

| Option | Motor | Controller | Peak current | Top speed | Price |
| --- | --- | --- | --- | --- | --- |
| A | QS273 V4 70H hub | ND961800 | **1800A** | 157 km/h | $1,490 + accessories |
| B | QS165 mid | ND96680 | 680A | TBD (ratio-dependent) | $797 + $500–1k fab |
| B | ME1302 mid | Kelly KLS96601 | 600A | TBD | $799 motor + controller + fab |

**Note:** Gear ratios multiply torque but not power. Watt ceiling is set by motor rating.

## Add-ons Needed for Option A

| Component | Est. cost | Notes |
| --- | --- | --- |
| DC-DC 12V converter | ~$30–50 | Powers lights/accessories from 96V pack |
| 96V charger | ~$150–300 | Source separately |
| Throttle | ~$25 | Hall effect |
| Brake cutoff switches | ~$15–25 | Safety cutoff |
| Wiring harness | ~$40–80 | Can ask Damon if he sells separately |
| Display | ~$30–119 | SCJ5066-1 or similar |
| **Accessories subtotal** | **~$290–595** | |
| **Option A all-in estimate** | **~$1,780–2,085** | Including battery |

## Open Questions

| Question | Affects |
| --- | --- |
| Does 190mm tire clear swingarm? | Option A go/no-go — hold ~190mm object in swingarm to check |
| Can Damon sell harness + display separately? | Option A accessories cost |
| VN750 driveshaft input spline specs | Option B feasibility |
| VN750 rear bevel gear ratio | Option B speed calculation |

## Pending Actions

- [ ] Physical check: hold ~190mm-wide object in swingarm (Option A tire clearance)
- [ ] Email Damon: confirm Combo 2 is ND961800 96V; ask about harness + display add-ons
- [ ] Check AliExpress QS165 listing for harness inclusion if pursuing Option B (item 3256809152484076)
- [x] Order battery — done 2026-06-28
- [x] Mail DMV packet — done 2026-06-27

## DMV and Registration Status

- **Goal:** Virginia antique plates (qualifies: 25+ years old)
- **Completed:** Title filled out, insurance obtained, packet mailed 2026-06-27
- **Pending:** Await DMV response
- **Note:** 4.15% SUT applies, $75 minimum, $140 total check sent
- **Strategy:** Registered before conversion while bike is ridable