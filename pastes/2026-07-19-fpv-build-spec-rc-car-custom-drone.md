---
title: "FPV Build Spec — RC Car + Custom Drone"
date: 2026-07-19 21:34:57 +0000
author: pinky
---

# FPV Build Spec

## Shared Components

| Item | Model | Price |
|------|-------|-------|
| Goggles | Fatshark Recon HD (HDZero native) | ~$299 |
| Radio TX | RadioMaster Pocket (ELRS 2.4GHz) | ~$70 |
| LiPo Charger | ISDT Q6 Plus | ~$45 |
| **Shared subtotal** | | **~$414** |

---

## Section 1: Custom FPV Drone (5" Freestyle)

| Item | Model | Price |
|------|-------|-------|
| Frame | TBS Source One V5 (5") | ~$25 |
| FC + ESC Stack | SpeedyBee F405 V4 AIO | ~$65 |
| Motors (x4) | Emax Eco II 2306 2400KV | ~$60 |
| Props | HQProp 5x4.3x3 (pack) | ~$15 |
| FPV Camera + VTX | HDZero Nano Kit | ~$105 |
| Receiver | BetaFPV SuperP ELRS | ~$15 |
| Battery (x2) | 4S 1500mAh LiPo (CNHL/Tattu) | ~$55 |
| Misc (hardware, connectors) | — | ~$20 |
| **Drone subtotal** | | **~$360** |

**Firmware:** Betaflight (free, open source)
**Notes:** HDZero Nano feeds directly to Fatshark Recon HD goggles. Same RadioMaster Pocket controls both drone and car.

---

## Section 2: FPV RC Car (Phone Carrier, ~400m road use)

| Item | Model | Price |
|------|-------|-------|
| Chassis | Traxxas Rustler 4x4 BL-2S (RTR) | ~$380 |
| FPV Camera + VTX | HDZero Nano Kit (second unit) | ~$105 |
| Receiver | BetaFPV SuperP ELRS (replaces stock RX) | ~$15 |
| Power for FPV | 5V BEC tapped from main battery | ~$10 |
| Phone cradle/mount | Universal adjustable mount | ~$15 |
| Camera tilt mount | 3D printed or universal (~30° tilt) | ~$10 |
| **Car subtotal** | | **~$535** |

**Notes:** Traxxas stock radio replaced by ELRS receiver, controlled via same RadioMaster Pocket as drone. HDZero camera matches goggles ecosystem — no extra hardware needed. Phone rides in the cradle; car is road-going at low speed so securing it casually is fine.

---

## Grand Total

| Section | Cost |
|---------|------|
| Shared components | ~$414 |
| Custom FPV drone | ~$360 |
| FPV RC car | ~$535 |
| **Total** | **~$1,309** |

---

## Notes & Next Steps

- Fatshark Recon HD supports HDZero natively — no adapter needed
- Both vehicles share the same RadioMaster Pocket transmitter and same FPV goggles
- Build drone first to learn Betaflight + ELRS; RC car is simpler to wire
- HDZero latency: ~8-14ms — noticeably sharper to fly than DJI O3 at ~25ms
- For the car: no FAA registration needed, no drone regs, just drive