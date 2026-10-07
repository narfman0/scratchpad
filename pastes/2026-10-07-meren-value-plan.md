---
title: "Meren value plan"
date: 2026-10-07 21:18:34 +0000
author: hermes
---

# Meren: move from Hulk combo to a value deck

## Why

In practice the deck rarely plays through Meren; most games become Protean Hulk lines. While Hulk is in the 99, every tutor's best target is Hulk (or Entomb to set it up), so playing around it means deliberately making worse plays. Moving the Hulk package to the sideboard makes Meren the engine again, and the package can be swapped back in when I want to combo.

The aim: Meren returns a creature from the graveyard at every end step, so each slot should be a creature worth getting back every turn (edicts, drain, removal, tutoring).

## Out (to sideboard: the Hulk package)

- **Protean Hulk**
- **Natural Order**: Hulk is the only reason it's in the deck.
- **Footsteps of the Goryo**: the creature is sacrificed at end step, so it's only good with Hulk.
- **Apprentice Necromancer**: same problem, the creature it returns is sacrificed at end step.
- **Melira, Sylvok Outcast**: Hulk fetch target.
- **Lesser Masticore**: Hulk fetch target.
- **Disciple of the Vault**: Hulk fetch target.

To combo again, swap these 7 back in for the 7 below.

## In (about $13 total)

- **Plaguecrafter** ($0.40): each player sacrifices a creature or planeswalker. Sacrifice it to an outlet and Meren returns it, so it's an edict every turn.
- **Fleshbag Marauder** ($0.28): a second repeatable edict.
- **Pitiless Plunderer** ($4.62): a Treasure whenever another creature of yours dies, so every sacrifice gives mana back.
- **Gray Merchant of Asphodel** ($3.97): drains each opponent for your devotion to black. Meren returns it every turn once you have 5 experience. A finisher that doesn't need Hulk.
- **Grave Titan** ($0.34): a 6/6 with deathtouch that makes two Zombies when it enters and whenever it attacks, which is more sacrifice fodder and experience. Buy a second copy; the current one is in Satoru.
- **Massacre Wurm** ($1.94): opponents' creatures get -2/-2 when it enters, and each opponent loses 2 life whenever one of their creatures dies. A repeatable board wipe and drain.
- **Rune-Scarred Demon** ($1.07): a 6/6 flier that tutors any card when it enters. It's also a second turn-1 Entomb + Animate Dead target alongside Archon.

## Experience and big targets

- Without Hulk, **Archon of Cruelty** (8 mana value) is the only creature that needs 8 experience. Everything else in the list costs 6 or less.
- Experience counters are on the player, not on Meren. If she's killed you keep the count, and when you recast her she returns big creatures right away.
- When a creature costs more than your experience count, Meren still puts it back in your hand, so Archon returns every turn before you reach 8.
- **Phyrexian Delver** is a strong repeat target: it returns a creature from the graveyard to the battlefield when it enters (you lose life equal to that creature's mana value).

## Turn-1 Animate Dead

Tutor for **Entomb** (instant, B), Entomb Archon or Rune-Scarred Demon, then cast Animate Dead (1B). With the Hulk package swapped in and a free sac outlet available, Entomb Hulk instead: it fetches Viscera Seer + Melira + Lesser Masticore + Disciple and the loop kills the table.

## Bracket

Still Bracket 4: 5 Game Changers remain, and Mikaeus + Walking Ballista and Mikaeus + Yawgmoth are still two-card combos. Keep those as backup wins, or move Ballista to the sideboard too if you want the deck fully fair.

## Later swaps

- Growing Rites of Itlimoc, out for **Noxious Gearhulk** ($0.39): repeatable creature removal.
- Phyrexian Arena, out for **Sheoldred, Whispering One** (proxy; about $21 real): returns a creature at each of your upkeeps and makes each opponent sacrifice one at theirs.

## To do

- Make the swaps on Moxfield, with the Hulk package on the sideboard.
- `sync_decks.py` only reads the main deck, commander and maybeboard. Add sideboard support so the Hulk package is tracked.
- Update `descriptions/meren.md` with the new gameplan.
