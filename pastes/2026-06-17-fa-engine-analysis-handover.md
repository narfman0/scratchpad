---
title: "FA Engine Analysis Handover"
date: 2026-06-17 18:03:42 +0000
author: pinky
---

# FA Engine Analysis — Handover Document

This document hands off ongoing work analyzing the Supreme Commander: Forged Alliance engine binary for FAF (Forged Alliance Forever) AI threading research.

## Context

The goal is to understand how SupCom distributes AI work across CPU cores — specifically whether FAF AI mods (M28AI, etc.) can be made to use multiple cores, and what the engine's threading limits are.

## What's Been Done

### Ghidra analysis of SupremeCommander.exe

- **Binary**: `SupremeCommander.exe` (13 MB, x86 PE, stripped — no PDB), MD5 `42e1f65f138f137c549c26cd587b350b`
- **Ghidra project**: `~/ghidra-supcom/` (SupCom.gpr) — fully analyzed, ~286s
- **Flatpak install**: `org.ghidra_sre.Ghidra` via system Flatpak
- **Extraction script**: `~/ExtractAllStrings.java` — dumps all thread/AI/sim symbols + strings to `~/fa-strings.txt`

### Key findings (full detail in README)

- **5–6 thread model**: sim thread, IssueThread, render/vsync thread, pathfinding background thread, prefetcher thread, CTaskThread worker pool
- **Beat-based lockstep**: `Sim_Sync` / `Sim_Dispatch` threads; `CClientBase` has `mQueuedBeat`, `mDispatchedBeat`, `mAvailableBeat`, etc. for netcode sync
- **CAiBrain**: C++ class at `0x00e69320`, loads `/lua/aibrain.lua`, exposes 30+ methods to Lua via `moho.aibrain_methods` metatable
- **ForkThread API**: Lua coroutines only — NOT OS threads. All FAF AI mods run as coroutines on the sim thread, which is why they can't use multiple cores today
- **`IAiCommandDispatch`** / `IAiCommandDispatchImpl`: decoupled command queue interface between AI and sim
- **Pathfinding**: `PathQueue` background thread with per-army tick budget (`path_BackgroundBudget`, `path_ArmyBudget`)

### Conclusion for multi-core AI

FAF AI mods (Lua) run entirely within the `ForkThread` coroutine scheduler on the **single sim thread**. The sim must be deterministic for netcode, so it cannot be parallelized. Multi-core gains are limited to offloading render/pathfind/prefetch — not AI logic itself.

## Project Location

```
/home/narfman0/.openclaw/workspace/faf-analysis/README.md
```

Full findings with addresses, string table, source file map, synthesis, and next steps.

## Files on Disk

| Path | Description |
|------|-------------|
| `~/.openclaw/workspace/faf/SupremeCommander.exe` | Binary being analyzed |
| `~/.openclaw/workspace/faf/MohoEngine.dll` | Engine DLL — **not yet analyzed** |
| `~/.openclaw/workspace/faf/faf-fa/` | FAF Lua source (reference) |
| `~/.openclaw/workspace/faf/M28AI/` | M28AI mod source (reference) |
| `~/ghidra-supcom/` | Ghidra project (SupCom.gpr + SupCom.rep) |
| `~/fa-strings.txt` | Raw extraction output (877 strings, 454 symbols) |
| `~/ExtractAllStrings.java` | Ghidra script for re-extraction |
| `~/.openclaw/workspace/faf-analysis/README.md` | Full analysis writeup |

## Pending / Next Steps

1. **Analyze MohoEngine.dll** — likely contains `CTaskThread` implementation, renderer, audio, and the actual affinity-setting code
2. **Cross-reference `__beginthreadex` callers** at `0x00ace3f3` to enumerate all spawned threads with names
3. **Decompile `Sim_Sync` / `Sim_Dispatch` entry points** — understand beat gate logic (find them via string xrefs to `0x00e4f9c8` / `0x00e4f9d4`)
4. **Map `SetThreadAffinityMask` callsites** — see which threads get pinned to which core masks
5. **Investigate `QueueUserAPC` callers** — likely the IssueThread→SimThread signaling path

## How to Re-run Extraction

```bash
# Project must be in home dir (Flatpak can't see /tmp)
cp -r /tmp/ghidra-supcom ~/ghidra-supcom   # already done

GHIDRA_MAXMEM=4G flatpak run --command=/app/lib/ghidra/support/analyzeHeadless \
  org.ghidra_sre.Ghidra \
  /home/narfman0/ghidra-supcom SupCom \
  -process SupremeCommander.exe \
  -noanalysis \
  -scriptPath /home/narfman0 \
  -postScript ExtractAllStrings.java
# Output: ~/fa-strings.txt
```

## How to Analyze MohoEngine.dll

```bash
GHIDRA_MAXMEM=6G flatpak run --command=/app/lib/ghidra/support/analyzeHeadless \
  org.ghidra_sre.Ghidra \
  /home/narfman0/ghidra-supcom SupCom \
  -import /home/narfman0/.openclaw/workspace/faf/MohoEngine.dll \
  -overwrite \
  2>&1 | tee ~/ghidra-moho-analysis.log
```

Then run `ExtractAllStrings.java` against it with `-process MohoEngine.dll -noanalysis`.