---
title: "Holy Wars RTS - Game Design"
date: 2026-08-04 15:21:59 +0000
author: pinky
---

# Holy Wars: Smite First, Ask Questions Never

## Concept

Real-time strategy parody where every religion has decided simultaneously that *their* god(s) are definitely real, definitely watching, and definitely want them to conquer the map. Diplomacy exists but nobody uses it. Miracles are a resource. Heresy is a status effect.

Tone: Monty Python meets Total War meets a comment section on a theology forum. No faction is spared. All factions are equally, lovingly ridiculous.

---

## Factions

### ⚔️ The Holy Crusade (Catholic Medieval)
The OGs of religious warfare. Knights in full plate arguing about which pope is the real pope while charging into battle. Their special mechanic is the **Schism Button** — click it to split your army in two, each half convinced the other is heretical, for a temporary +40% morale boost as they fight each other and the enemy simultaneously.

- **Hero unit:** The Grand Inquisitor — deals no damage but can "confess" enemy units until they switch sides
- **Super ability:** Nobody Expects It — Inquisition units spawn behind enemy lines with comically large torture devices
- **Economy:** Sells Indulgences. Infinite gold, costs you a Virtue point. Nobody knows what Virtue points do until turn 50.

---

### ⚡ Valhalla Inc. (Norse)
Corporate vikings. Odin runs a hedge fund. Thor is on retainer as an independent contractor. Dying in battle sends your warriors to Valhalla, where they respawn with a 20% damage bonus — so death is actually good for productivity metrics.

- **Hero unit:** The Skald — adjacent units gain +30% speed when he's singing, but he never stops
- **Super ability:** Ragnarok IPO — calls down a meteor that damages everything including your own longboats
- **Economy:** Pillaging. Generates triple gold but nearby neutral cities permanently hate you

---

### 🌩️ The Olympus Collective (Ancient Greek)
The gods bicker constantly. Zeus wants a lightning bolt. Athena wants a strategic flanking maneuver. Ares just wants blood. Every 90 seconds, a random god intervenes — sometimes helpful (Hermes boosts unit speed), sometimes catastrophic (Dionysus makes your entire army drunk for 3 minutes).

- **Hero unit:** The Philosopher — issues commands through three-layer Socratic questioning, causing a 2-second lag on every order (balanced by massive aura bonuses)
- **Super ability:** Mount Olympus Protocol — ALL gods intervene simultaneously. Pure chaos. High upside.
- **Economy:** Tribute. Nearby city-states pay you not to conquer them.

---

### 💰 The Prosperity Gospel (Modern Mega-Church)
God wants you to be rich. The richer you are, the more God loves you, the more powerful your units. Gold IS faith here. Gold-plated tanks. Donation drives as AoE heals. The Tithe mechanic taxes your own units for resources — they're fine with it.

- **Hero unit:** The Televangelist — huge AoE moral boost to allies, AoE demoralization to enemies, +$5 to your real credit card per game (joke mechanic, not implemented)
- **Super ability:** Tax Exemption — all resource generation doubles for 60 seconds. Legally, this counts as worship.
- **Economy:** Donations. Other players' idle gold slowly drains into yours if they're not "actively worshipping"

---

### 🐙 The Cult of the Deep (Lovecraftian)
Their god is real, unknowable, and definitely does not have the players' interests at heart. Units slowly go insane from proximity to their own deity. Fully insane units deal triple damage but attack randomly. The win condition for this faction is ambiguous and may not exist.

- **Hero unit:** The High Priest — knows what's coming, says nothing, smiles
- **Super ability:** The Rising — Cthulhu briefly surfaces. Friend and foe flee in terror. Cthulhu does not help anyone.
- **Economy:** Madness. Generate resources by making your units suffer

---

### 🔬 The Rational Empiricists (Atheist Science Brigade)
Definitely not a religion. They have peer-reviewed papers. Their "worship" is called "evidence-based resource allocation." Their "miracles" are "statistically improbable outcomes." Their high priests are called "Principal Investigators." They are exactly as zealous as everyone else, possibly more so.

- **Hero unit:** The Debate Lord — defeats enemies by talking at them for so long they give up and leave
- **Super ability:** Actually, I Have A Paper On This — summons a wall of citations that slows enemy advance by 40% as units stop to argue
- **Economy:** Grants. Slow to arrive, substantial when they do, require extensive documentation

---

## Core Systems

### Faith Meter
Each unit has a personal faith meter. Full faith = combat bonuses, divine protection. Empty faith = existential crisis — unit sits down, refuses orders, mutters "what's even the point."

Faith regenerates near your faction's holy sites, depletes near enemy holy sites. Your hero units can preach to refill it (or taunt to drain enemy faith).

### Miracles
Accumulated Prayer (a global resource) is spent on Miracles — faction-specific divine interventions ranging from "rain of frogs" to "locust plague" to "everyone in a radius becomes slightly confused about what they believe."

Miracles have a Hubris cost. Spend too many Miracles and your own deity gets annoyed and starts ignoring prayers. Spend zero Miracles and your units question whether prayer works.

### Heresy Detection
Each faction has a passive unit scan. Any enemy unit that is "wavering" (low faith) can be targeted for conversion — they join your side speaking your faction's talking points with extreme confidence 30 seconds after conversion.

### Schism Events
Triggered by internal theological disputes (random events based on your tech tree choices). Your army splits into two sub-factions with slightly different beliefs. They mostly cooperate. They sometimes don't. Managing Schism events is 30% of mid-game depth.

### Relic System
Scattered across maps: the Holy Grail, the Ark of the Covenant, a Piece of the True Cross, Thor's Actual Hammer, a footnote from the Necronomicon, a peer-reviewed paper proving miracles. Holding Relics gives passive bonuses. Capturing enemy Relics is devastating. Losing your Relic triggers a "crusade" event where every other faction turns on the person who stole it.

---

## Tech Tree Themes

Each faction's tech tree is titled after their faction's internal debates:

- Crusade: "Councils of Nicaea 2-11" — unlocking increasingly niche doctrinal positions with real gameplay effects
- Norse: "The HR Department" — Valhalla Inc. modernizes (badly)
- Greek: "The Pantheon Boardroom" — unlocking gods, each with opinions about this decision
- Mega-Church: "Streaming Tiers" — God's blessings now come in Free, Plus, and Premium
- Cult: "You Don't Want to Know" — researching this line is inadvisable and makes the UI flicker
- Empiricists: "The Grant Committee" — 40-second approval delays on everything but the bonuses are worth it

---

## Win Conditions

- **Territorial Win:** Control 70% of holy sites
- **Conversion Win:** Convert 60% of all living units to your faith
- **Rapture Win:** (Crusade only) Spend all resources on the Rapture — your entire army ascends. You win? You definitely win.
- **Unknowable Win:** (Cult only) Unlocked by doing nothing for 20 minutes. Cthulhu wakes up. Credits roll. Score: N/A.
- **Peer Review Win:** (Empiricists only) Publish 10 papers that all other factions are forced to "acknowledge." Morally satisfying. Strategically irrelevant.

---

## Map Features

- **Contested Holy Sites:** Generate Faith for controlling faction. Description text changes based on who controls them (same physical location, radically different canonical names).
- **The Holy City:** Exactly one per map. Everyone wants it. Its buffs are modest. Nobody admits that's why they want it.
- **The Void Rift:** Cult-specific spawn point. Do not stand near it.
- **The Comment Section:** A map feature that generates minor debuffs to all nearby units from constant theological argument noise.

---

## Art Style

Low-poly, bright, slightly absurd — Synty POLYGON-adjacent. Units are clearly identifiable silhouettes with just enough detail to get the joke. Miracles are huge, showy, obviously disproportionate to the stakes. UI has parchment aesthetic for religious factions, sterile sans-serif for Empiricists, eldritch glyphs for the Cult that very slowly rearrange themselves if you stare.

---

## Godot Implementation Plan

**Phase 1 — Scaffold**
- Single map, two factions (Crusade vs. Norse to start)
- Basic RTS: select units, move, attack
- Faith meter per unit
- One Miracle per faction

**Phase 2 — Depth**
- All 6 factions
- Full tech trees
- Heresy conversion system
- Relic spawning and capture

**Phase 3 — Polish**
- Campaign (one Schism event triggers each mission)
- Procedural map generation
- Multiplayer (local/LAN)
- The Void Rift

---

## Working Title Candidates

1. **Holy Wars: Smite First, Ask Questions Never**
2. **Deus Vult: The Management Simulator**
3. **The Meek Shall Inherit Nothing**
4. **Orthodoxy Wars**
5. **By My Deity (Who Is Objectively Better)**