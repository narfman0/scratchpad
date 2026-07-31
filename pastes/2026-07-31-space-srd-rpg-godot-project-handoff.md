---
title: "Space SRD RPG — Godot Project Handoff"
date: 2026-07-31 01:03:21 +0000
author: pinky
---

# Space SRD RPG — Godot Project Handoff

## Vision

A **Baldur's Gate 3 in space** — a narrative 3D RPG using a custom SRD-compatible ruleset set in a near-future sci-fi universe. Small handcrafted area slices (not open world), deep dialogue and roleplay, tactical combat, and a broader faction-driven narrative context.

Reference touchstones: Baldur's Gate 3, Mass Effect, Pillars of Eternity.

---

## Key Decisions Made

- **Engine**: Godot 4 (latest stable)
- **Perspective**: 3D, small area slices (not open world, not seamless planets)
- **Combat**: Turn-based tactical (BG3-style), not real-time action
- **Rules**: Custom SRD-compatible space ruleset (own setting, own nouns — legally distinct from D&D 5e but mechanically compatible)
- **Assets**: Synty Studios packs (modular, low-poly) served from local asset server
- **Dialogue**: Dialogic plugin (free, widely used for Godot narrative games)
- **Architecture**: Reusable addon (`addons/space_srd/`) so the engine can power future games

---

## Space SRD Ruleset Outline

Keep D&D 5e SRD math exactly. Reskin all nouns:

| D&D 5e SRD | Space SRD |
|---|---|
| Strength | Might |
| Dexterity | Reflex |
| Constitution | Endurance |
| Intelligence | Logic |
| Wisdom | Intuition |
| Charisma | Presence |
| Fighter | Soldier |
| Rogue | Ghost |
| Wizard/Sorcerer | Psion |
| Cleric | Warden |
| Spells | Abilities (tagged: psionic / tech / combat / support) |
| Spell slots | Energy slots (same math) |
| Monster CR | Threat Rating |

Core mechanics retained: d20 + modifier vs DC, advantage/disadvantage, action economy (Action + Bonus Action + Movement + Reaction), conditions (prone, stunned, etc.), short/long rest, proficiency bonus by level.

---

## Project Structure

```
res://
  addons/
    space_srd/              ← reusable engine addon (no game content here)
      rules/
        rules_engine.gd     ← Autoload: roll_d20(), ability_check(), attack_roll(), saving_throw()
        combat_manager.gd   ← Autoload: turn order, action economy, end-of-turn logic
      resources/
        character_data.gd   ← Resource: ability scores, HP, proficiency, spell slots, conditions
        ability_data.gd     ← Resource: ability name, tags, range, damage, save type, description
        item_data.gd        ← Resource: weight, cost, equip slot, stat modifiers
        encounter_data.gd   ← Resource: participants list, initiative, grid/free position
      systems/
        inventory_manager.gd
        condition_tracker.gd
        experience_manager.gd
      ui/
        character_sheet.tscn
        action_bar.tscn
        dice_roller.tscn    ← animated d20 roll UI
  game/                     ← THIS game's content (swap out for future games)
    areas/                  ← handcrafted level slices
    characters/             ← NPCs, party members, enemies
    quests/
    dialogue/               ← Dialogic trees
    ui/                     ← game-specific HUD
```

---

## Build Order (Recommended)

### Phase 1 — Rules Core (no graphics)
1. `CharacterData` Resource with ability scores, HP, proficiency bonus, spell/energy slots
2. `RulesEngine` autoload: `roll_d20()`, `ability_modifier(score)`, `ability_check(char, ability, dc)`, `attack_roll(attacker, target)`, `saving_throw(char, ability, dc)`
3. Console test: two characters, one combat encounter, all rolls logged — prove the math

### Phase 2 — Combat Loop
4. `CombatManager` autoload: initiative order, current-turn tracking, action economy flags
5. Basic 3D scene: flat plane, two `CharacterBody3D` nodes using `CharacterData`
6. UI: action bar (Attack, Ability, Item, End Turn), HP bars, turn indicator
7. Enemy AI: simple aggro → move toward player → attack on turn

### Phase 3 — Dialogue & Narrative
8. Install Dialogic plugin
9. One NPC with a branching conversation (skill check gated option using RulesEngine)
10. Quest flag system (simple Dictionary in a `QuestManager` autoload)

### Phase 4 — First Area
11. Import first Synty asset pack into Godot
12. Block out one small area (a space station corridor or planetary outpost)
13. Place NPCs, one encounter, one quest start-to-finish

### Phase 5 — Iteration
14. Add classes (Soldier, Ghost, Psion, Warden) with unique ability lists
15. Add second area / second planet slice
16. Companion system (party of up to 4)

---

## Plugins to Install

- **Dialogic** — dialogue trees, character portraits, branching narrative
  - https://github.com/dialogic-godot/dialogic
- **Phantom Camera** (optional) — smooth camera rigs for third-person view

---

## Assets

- Source: Synty Studios packs (owner has license)
- Served from local asset server (HTTP or SMB mount — clarify with owner)
- Import format: FBX via Godot's built-in importer
- Synty kits snap to 1-unit grid — use GridSnap in Godot editor
- Recommended packs for this genre: POLYGON Sci-Fi Space, POLYGON City, POLYGON Sci-Fi Worlds

---

## What NOT to Build Yet

- Seamless planet-to-planet travel (out of scope for v1)
- Civilization/faction simulation (narrative context only, not simulated)
- Spaceship ownership/piloting (nice to have, not core)
- Multiplayer/MMO elements

---

## Owner Context

- Godot experience: ~0 (tried it ~10 years ago)
- Strong programming background (see other projects in workspace)
- Wants a reusable framework for multiple games, not just one
- Setting and IP are original (not D&D, just SRD-compatible mechanics)
- Prefers to use existing Synty assets rather than commissioning new art
