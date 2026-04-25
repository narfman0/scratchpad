---
title: "fellytip Portal Preview Rendering Plan"
date: 2026-04-25 17:11:42 +0000
author: pinky
---

## Portal Preview Rendering Plan

### Core concept

The game already prefetches 1-hop neighbor zone tiles on every transition (`send_zone_tiles` sends destination + all neighbors). The tile data is already on the client. The portal preview is just **rendering that cached data to a texture and displaying it on the portal shape**.

---

### The Bevy technique: Render-to-Texture + Secondary Camera

```
Main Camera (RenderLayers::layer(0))
  └── renders current zone tiles + entities

Portal Camera (RenderLayers::layer(1))  ← one per visible portal
  └── renders destination zone tiles + entities
  └── target: RenderTarget image (e.g. 256×256 texture)

Portal Mesh (at portal world position)
  └── sprite/quad using the RenderTarget as its material
  └── on layer(0) so main camera sees it
```

For top-down 2.5D the portal camera orientation is identical to the main camera — just repositioned. The "looking through" illusion comes from offsetting the portal camera by how far the player is from the portal center:

```
portal_cam_pos = destination_anchor + (player_pos - portal_pos)
```

This gives true parallax — as you approach and angle around the portal, the view through it shifts.

---

### What changes per layer

| Thing | Current | With portal preview |
|---|---|---|
| Current zone tiles | spawned on default layer | move to `RenderLayers::layer(0)` explicitly |
| Neighbor zone tiles | cached but not rendered | spawn on `RenderLayers::layer(1)`, centered on their anchor |
| Portal trigger entity | invisible ECS entity | gains a portal-preview mesh using RenderTarget texture |
| World-style shader | not implemented | applied to portal *camera* — Sunken Realm pixelation appears inside portal frame before crossing |

---

### The seamless transition

```
Player approaches portal
  → portal preview mesh is visible (seeing other side)
  → portal camera tracks player offset (parallax)

Player crosses trigger radius
  → ZoneMembership swaps
  → Main camera smoothly lerps position to player's new location
  → World-style transition shader fires (pixelate, ink-bleed, etc.)
  → Old zone tiles fade/despawn
  → New zone's portal camera is now the main view
```

Because the portal preview was already showing the destination, the transition isn't a hard cut.

---

### Per-world style in the portal frame

| World | Portal camera post-process |
|---|---|
| **Surface → Sunken Realm** | Render at 320×180, nearest-neighbor upscale — pixelation visible *inside* the portal while standing in the realistic Surface world |
| **Surface → Mycelium** | Vertex displacement + chromatic aberration — view through portal is already wobbly and wrong before you step in |
| **Within Surface** | No post-process on portal camera, seamless |

---

### Implementation phases

**Phase 1 — Static tile preview (no entities, fixed camera)**
1. In `ZoneRendererPlugin`, tag neighbor zone tiles `RenderLayers::layer(1)`
2. For each `PortalTrigger` in range: spawn `PortalCamera` + `RenderTarget` image
3. Portal trigger entity gets a quad mesh using that `RenderTarget` as material
4. Portal camera positioned at `to_anchor`, same rotation as main camera

**Phase 2 — Live parallax + entities**
5. Portal camera tracks `to_anchor + (player_pos - portal_pos)` each frame
6. Destination zone entities get `RenderLayers::layer(1)` added when in range

**Phase 3 — World-style shaders in portal**
7. Portal camera gets `PostProcessSettings` keyed to destination `WorldId`
8. During transition: main camera adopts those settings, crossfade

---

### Open questions before coding

- **Portal shape**: rectangular (doors/arches) or oval? Shape clips the RenderTarget.
- **Portal camera count**: only spawn for portals within current zone + screen-distance threshold.
- **Entities in preview**: Phase 2 requires Lightyear per-zone interest management to be wired (currently not).

---

### Verdict

Phase 1 is buildable now — all tile data is already prefetched, purely a renderer change. Phase 2 requires no data model changes. Phase 3 depends on art style work.