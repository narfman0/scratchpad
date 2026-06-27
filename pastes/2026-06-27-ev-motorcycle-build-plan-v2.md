---
title: "EV Motorcycle Build - Plan v2"
date: 2026-06-27 13:14:05 +0000
author: pinky
---

# EV Motorcycle Conversion — Updated Plan

Build: 1994 Kawasaki VN750 Vulcan → 96V Electric
Goal: Great acceleration, 65+ mph capable, ~25 mile range, VA antique plates

## Donor Bike

| Item | Status | Cost |
| --- | --- | --- |
| 1994 Kawasaki VN750 Vulcan | Purchased | $950 |

## Options Considered

### Motor + Controller

**Frontrunner: SiAECOSYS 17x6.0inch 70H 12000W V4 96V kit — Combo 2 (ND961800)**

- QS 273 70H 12000W V4 hub motor
- Fardriver ND961800 controller (96V, 1800A peak)
- Kit price: $1,490.39
- Contact: damon@siaecosys.com
- Note: 17 inch rim only — 15 inch lacing not available. Motor OLD (dropout width): 230mm.

### Battery

| Option | Specs | Cost | Notes |
| --- | --- | --- | --- |
| **Frontrunner: 40Ah 300A BMS** | 26s NMC, 96V, 40Ah, 300A BMS, charger included | $731 | 165x240x270mm; NMC confirmed |
| Backup: 30Ah 100A BMS | 26s NMC, 96V, 30Ah, 100A BMS, charger included | $379 | 100A BMS likely undersized for motor |

AliExpress item: 3256804576924652

Battery notes:

- Chemistry: NMC (Li-ion Ternary), not LiFePO4
- Higher energy density than LiFePO4; ~500-1000 cycle life
- Store at ~80% charge if sitting for extended periods
- 300A BMS x 96V = 28.8kW peak — matches motor well

## Selected Parts List

### Drivetrain (pending confirmation)

| Item | Notes |
| --- | --- |
| QS 273 70H 12000W V4 hub motor | 17 inch lacing |
| Fardriver ND961800 controller | 96V, 1800A peak |
| SCJ5066-1 TFT display | 5 inch, Lin communication (LCD not compatible with 96V) |
| YY V3 throttle + combination switch | ~$60 |
| Vehicle wiring harness | Includes 96V to 12V DC-DC converter |

### Battery (pending fitment confirmation)

| Item | Notes |
| --- | --- |
| 40Ah 300A BMS NMC pack | 165x240x270mm, charger included |

### Wheel and Brake

| Item | Est. Cost |
| --- | --- |
| 17 inch motorcycle rim (match motor spoke count) | $60 |
| 190/50-17 tire | $80 |
| Wheel lacing (bike shop) | $80 |
| Rear disc rotor (6-bolt ISO, 160mm) | $35 |
| Rear caliper + bracket | $70 |
| Hydraulic brake line | $25 |

### Mechanical

| Item | Notes | Est. Cost |
| --- | --- | --- |
| Axle spacers | Machine shop — measure OLD first (17mm axle confirmed) | $75 |

### Electrical

| Item | Est. Cost |
| --- | --- |
| Main contactor | $45 |
| Pre-charge resistor + relay | $20 |
| Main fuse + disconnect switch (emergency kill) | $30 |
| Misc wire, connectors, terminals | $80 |

## Open Measurements Needed (Blockers)

1. **Swingarm OLD** — motor dropout is 230mm; measure inner dropout width with rear axle removed. Determines if motor fits without swingarm modification.
2. **Engine cavity LxWxH** — battery is 165x240x270mm; confirm fit before ordering.
3. **Swingarm clearance for 190mm tire** — stock is 140mm wide; confirm 190mm tire clears swingarm.

## Open Questions / Next Actions

- [ ] Get updated quote from Damon — with SCJ5066-1 display + throttle + harness added to kit
- [ ] Measure swingarm OLD
- [ ] Measure engine cavity
- [ ] Confirm 190mm tire swingarm clearance
- [ ] Determine charger plug type (included with battery)
- [ ] Register for antique plates (VA) once build is complete

## Budget Summary

| Category | Cost |
| --- | --- |
| Donor bike | $950 |
| Drivetrain kit (ND961800) | $1,490 |
| Display + throttle + harness | ~$210 |
| Battery (40Ah 300A NMC) | $731 |
| Wheel + brake | $350 |
| Mechanical + electrical misc | $250 |
| **Total** | **~$3,981** |

## Key Specs Reference

- Voltage: 96V nominal (109.2V peak charge)
- Motor: QS 273 70H, 12000W, hub drive, 17 inch wheel
- Controller: Fardriver ND961800, 1800A peak
- Battery: 26s NMC, 40Ah, 300A BMS — effective peak ~28.8kW (300A x 96V)
- Rear wheel: 17 inch, 190/50-17 tire
- Rear brake: disc (upgrade from stock drum)
- Motor dropout (OLD): 230mm
- Battery dimensions: 165x240x270mm
- Weight: ~70-100 lbs lighter than stock VN750