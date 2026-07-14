---
title: "EV Motorcycle Build Plan v9 - 2026-07-14"
date: 2026-07-14 04:05:03 +0000
author: pinky
---

# VN750 EV Conversion Build Plan — v9 (2026-07-14)

> **Status:** Battery ordered. Hub motor eliminated. Mid-drive via spline coupler is the primary path.

---

## Key Facts

- **Bike:** Kawasaki VN750 (shaft drive — no chain/sprocket on rear wheel)
- **Battery:** 96V 40Ah NMC, 300A BMS, 165×240×270mm — **ORDERED ~$731**
- **Engine cavity:** 220mm wide × 500mm tall × 300mm deep — battery fits with margin
- **Swingarm OLD:** ~260mm measured
- **DMV packet:** Mailed (VSA 14 + VSA 10B + signed title + insurance + $140 check)

---

## Tire Clearance — Hub Motor ELIMINATED

Cardboard test (190–195mm wide mock-up placed on stock tire) confirmed the 190mm tire **will not clear the right swingarm arm**. Approximately 25mm short. No viable workaround without major swingarm fabrication.

**Hub motor option is closed.**

---

## Primary Path: Option B — Mid-Drive via Spline Coupler

Keep the shaft drive. Mount a mid-drive motor in the engine bay, couple it to the driveshaft input via a custom spline coupler.

### Why this works
- Stock rear wheel stays — no tire fitment issue
- Keeps the shaft drive's bevel gear final reduction (~3:1 estimated) — chainless, beltless, low maintenance
- Mid-drive motor sits where the engine was — natural mounting location

### Motor Options

| Motor | Power | Cooling | Source | Price |
|---|---|---|---|---|
| QS165 96V kit | 5kW / 10kW peak | Air | AliExpress | $797 |
| QS138 96V kit | 4kW / 7.5kW peak | Air | AliExpress | $659–717 |
| ME1302 + Kelly KLS96601 | ~12.5kW | Water required | Kelly (US) | ~$1,500+ |

**QS165 recommended** — complete kit (motor + ND96680 controller + display + throttle), air-cooled, motorcycle-designed output shaft, best power/price balance.

Links:
- QS165 96V kit: search AliExpress for "QS165 5KW 96V ND96680"
- ME1302: https://kellycontroller.com/shop/me1302/
- Kelly KLS-8080N: https://kellycontroller.com/shop/kls-8080n-nps/

### Custom Parts Required

| Part | Description | Est. Cost |
|---|---|---|
| Spline coupler | Mates QS165 output shaft to VN750 driveshaft input spline | $300–600 fab |
| Motor mount plate | Locates motor in frame, aligned with driveshaft input | $200–400 fab |

### Open Questions — Option B

| Question | Action |
|---|---|
| VN750 driveshaft input spline spec (count, diameter, pitch) | Pull driveshaft, measure — machine shop needs this |
| Rear bevel gear ratio | Determines top speed; check service manual or measure |
| QS165 output shaft diameter | Confirm from listing or email seller — machine shop needs this |
| Does QS165 physically align with driveshaft input in engine bay? | Trial fit after motor arrives |

---

## Option A — Hub Drive (ELIMINATED)

~~QS273 V4 70H, 17×6" wheel, ND961800 controller~~ — eliminated by tire clearance. 190mm tire confirmed not fitting swingarm via cardboard test 2026-07-13.

---

## Option C — Mid-Drive + Chain Conversion (NOT PURSUED)

Would require adding a chain sprocket to the rear wheel hub and removing shaft drive. More fabrication than Option B with no benefit. Not pursuing.

---

## Component Checklist

| Item | Status | Cost |
|---|---|---|
| 96V 40Ah NMC battery | **ORDERED** | $731 |
| Motor + controller (QS165 kit) | Pending decision | ~$797 |
| Custom spline coupler | Pending spline measurement | $300–600 |
| Motor mount plate | Pending motor choice | $200–400 |
| Charger (96V compatible) | Not yet sourced | ~$100–150 |
| Brake switches (cutoff) | Not yet sourced | ~$20–40 |
| Contactor + pre-charge | Check if included in kit | ~$50–80 |
| DC-DC converter (96V→12V) | Check if included in kit | ~$30–50 |
| Misc wiring, connectors, hardware | — | ~$50–100 |

**Estimated total (Option B):** ~$2,300–2,900 depending on fab costs

---

## Next Steps

1. **Pull driveshaft** — measure input spline (count, diameter, pitch)
2. **Find local machine shop** — get coupler quote with spline + QS165 shaft specs
3. **Confirm bevel gear ratio** — VN750 service manual or measure
4. **Order QS165 96V kit** — once spline fab path is confirmed viable
5. **Source charger** — 96V compatible, ~10A minimum

---

## DMV / Title

- Virginia "specially constructed vehicle" registration
- VSA 14 + VSA 10B + signed title + insurance card + $140 check mailed
- Awaiting response