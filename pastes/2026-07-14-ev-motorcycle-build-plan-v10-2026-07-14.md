---
title: "EV Motorcycle Build Plan v10 - 2026-07-14"
date: 2026-07-14 11:32:40 +0000
author: pinky
---

# VN750 EV Conversion Build Plan — v10 (2026-07-14)

> **Status:** Battery ordered. Motor kit ordered. Mid-drive via spline coupler is the primary path.

---

## Key Facts

- **Bike:** Kawasaki VN750 (shaft drive — no chain/sprocket on rear wheel)
- **Battery:** 96V 40Ah NMC, 300A BMS, 165×240×270mm — **ORDERED ~$731**
- **Motor kit:** QS165 10kW V3 60H PMSM + 1:2.37 gearbox + ND961000 controller + DKD display — **ORDERED $1,217 delivered**
- **Engine cavity:** 220mm wide × 500mm tall × 300mm deep — battery fits with margin
- **Swingarm OLD:** ~260mm measured
- **DMV packet:** Mailed (VSA 14 + VSA 10B + signed title + insurance + $140 check)

---

## Tire Clearance — Hub Motor ELIMINATED

Cardboard test (190-195mm wide mock-up placed on stock tire) confirmed the 190mm tire **will not clear the right swingarm arm**. Approximately 25mm short. No viable workaround without major swingarm fabrication.

**Hub motor option is closed.**

---

## Primary Path: Mid-Drive via Spline Coupler

Keep the shaft drive. Mount the QS165 + gearbox in the engine bay, couple the gearbox output shaft to the VN750 driveshaft input via a custom spline coupler.

### Why this works
- Stock rear wheel stays — no tire fitment issue
- Built-in 2.37:1 gearbox + VN750 bevel gear (~3:1 est.) = strong low-speed torque, two reduction stages
- Chainless, beltless, low maintenance — keeps the shaft drive character of the bike
- Motor sits where the engine was — natural mounting location

### Motor Kit — ORDERED

**QS165 10kW V3 60H PMSM + 1:2.37 Gearbox**
- Motor: QS165, 10kW rated, 60H high-torque stator
- Gearbox: integrated 1:2.37 reduction
- Controller: Fardriver ND961000 (96V, 1000A peak)
- Display: DKD speedometer included
- Source: AliExpress — https://a.aliexpress.com/_m0lBCOr
- Price: $867 + $350 shipping = **$1,217**

### Custom Parts Required

| Part | Description | Est. Cost |
|---|---|---|
| Spline coupler | Mates gearbox output shaft to VN750 driveshaft input spline | $300-600 fab |
| Motor mount plate | Locates motor+gearbox in frame, aligned with driveshaft input | $200-400 fab |

### Open Questions

| Question | Action |
|---|---|
| Gearbox output shaft spec (diameter, interface: keyed/splined/flanged) | Ask seller now; verify when motor arrives |
| VN750 driveshaft input spline spec (count, diameter, pitch) | Pull driveshaft, measure — machine shop needs this |
| Rear bevel gear ratio | Check service manual or measure — affects top speed calc |
| Does motor+gearbox physically fit and align in engine bay? | Trial fit when motor arrives |

---

## Component Checklist

| Item | Status | Cost |
|---|---|---|
| 96V 40Ah NMC battery | **ORDERED** | $731 |
| QS165 + gearbox + ND961000 + display | **ORDERED** | $1,217 |
| Custom spline coupler | Pending shaft measurements | $300-600 |
| Motor mount plate | Pending motor arrival | $200-400 |
| Charger (96V compatible) | Not yet sourced | ~$100-150 |
| Brake switches (cutoff) | Not yet sourced | ~$20-40 |
| Contactor + pre-charge | Check if included in kit | ~$50-80 |
| DC-DC converter (96V to 12V) | Check if included in kit | ~$30-50 |
| Misc wiring, connectors, hardware | — | ~$50-100 |

**Spent so far:** $1,948
**Estimated remaining:** $700-1,400 (fab + accessories)
**Estimated total:** ~$2,650-3,350

---

## Next Steps

1. **Ask AliExpress seller** — gearbox output shaft diameter and interface type (keyed/splined/flanged)
2. **Pull VN750 driveshaft** — measure input spline (count, diameter, pitch)
3. **Find local machine shop** — get coupler quote once you have both shaft specs
4. **Confirm bevel gear ratio** — service manual or measure at the rear axle
5. **Source charger** — 96V compatible, ~10A minimum
6. **Trial fit motor** when it arrives — confirm alignment with driveshaft input

---

## Eliminated Options

- **Option A (Hub drive — QS273):** Eliminated 2026-07-13. 190mm tire confirmed not clearing swingarm via cardboard test.
- **Option C (Mid-drive + chain conversion):** Not pursuing — more fab than spline coupler with no benefit.

---

## DMV / Title

- Virginia specially constructed vehicle registration
- VSA 14 + VSA 10B + signed title + insurance card + $140 check mailed
- Awaiting response