---
title: "Electric Motorcycle Conversion Plan"
date: 2026-06-14 13:19:25 +0000
author: pinky
---

# Electric Motorcycle Conversion Plan

## Project Goals

- Platform: Cruiser frame (antique, pre-2001 for VA antique plates)
- Voltage: 96V
- Range: ~20 miles
- Top speed: 65+ mph minimum
- Focus: Great acceleration

## Donor Bike

**1994 Kawasaki VN750 Vulcan — $950 (Virginia Beach)**

- 32 years old — qualifies for VA antique plates (no yearly inspection)
- Clean title
- 21,301 miles
- Engine issues are irrelevant (it's being removed)
- Strong candidate

## Virginia Antique Plate Notes

- 25+ year old vehicles exempt from annual safety inspection (VA Code § 46.2-730)
- Must be used for pleasure driving / shows, not daily commuting
- One-time title + registration process

## Motor: QS Motor 273 70H

- High-stator hub motor, fits in rear wheel
- Exceptional torque for acceleration
- ~$600–700 direct from QS Motor
- Specify 96V and 65+ mph target speed when ordering — they'll recommend the right winding
- Re-lace to existing VN750 15" rear rim

## Controller: Fardriver ND961200

- 96V, 1200A peak
- ~$300–350
- Field weakening support — required to push 70H past its natural speed curve to 65+ mph
- Programmable via phone app (torque curves, regen, speed limits)

## Battery Pack: 96V 30Ah LiFePO4

- 30s1p configuration (30 cells in series)
- Cell recommendation: EVE or CATL 40Ah LiFePO4 prismatic cells
- ~25–35 lbs total pack weight
- BMS: JK or DALY 100A

### Sizing Math

- 20 miles × 75 Wh/mile = 1.5 kWh
- +20% buffer = ~2.0 kWh usable
- 2.0 kWh / 96V = ~21 Ah → 30Ah pack gives comfortable headroom

## Supporting Components

- DC-DC converter: 96V → 12V (lights, accessories)
- Contactor + pre-charge circuit
- Hall-effect throttle (0–5V)
- Charger (onboard or offboard)
- Axle adapter (VN750 rear axle is 17mm; QS motors typically 12mm)

## Budget Estimate

| Item | Cost |
|---|---|
| Donor bike (VN750) | $950 |
| QS 273 70H motor | $650 |
| Fardriver ND961200 controller | $325 |
| Axle adapter + hardware | $100 |
| 30× EVE 40Ah LiFePO4 cells | $500 |
| BMS (JK 100A) | $100 |
| Pack hardware/wiring | $100 |
| DC-DC converter | $50 |
| Contactor + pre-charge | $50 |
| Charger | $150 |
| Misc (throttle, connectors, etc.) | $150 |
| **Total** | **~$3,125** |