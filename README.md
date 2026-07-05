# After Burner Climax — PC Recompilation

> Mach-speed, missile-locked, sun-flared arcade dogfighting — running natively on your PC.

A static recompilation of **After Burner Climax** (Sega, Xbox 360 / XBLA, 2010) to a
native x86-64 executable. No emulator, no interpreter — the game's PowerPC code is
translated to C++ ahead of time with the [ReXGlue SDK](https://github.com/rexglue/rexglue-sdk)
and compiled to run directly on your machine.

## Why this game

After Burner Climax is Sega AM2's gorgeous, ridiculous love letter to the 1987
arcade classic — lock on to a dozen jets, hold the trigger, weave through a wall of
missiles, and slam into Climax Mode as the screen melts into bloom and afterburner
trails. It is pure arcade adrenaline.

And it's **gone.** Sega pulled it from Xbox Live and PSN in **2015** when the
licensing lapsed. It never came to PC. If you didn't buy it in that five-year
window, there has been no legal way to play it since — no Steam release, no
collection, nothing. That's exactly the kind of game static recompilation exists to
rescue: the recompiled executable *is* the preservation.

## Status

🚧 **Scaffolded — recompiled to C++, build up next.** The Xbox 360 binary
recompiles cleanly (base `0x82000000`, a hefty 43.6 MB image) via ReXGlue v0.8.0's
codegen with 4 function-entry hints (baked into the manifest). Next is building and
first boot; then the real work — GPU/shader bring-up, audio, and input. Being a
3D/VMX-heavy arcade title, it'll exercise more of the runtime than the 2D catalog.

| Stage | State |
|---|---|
| Extract (STFS → XEX) | ✅ |
| Codegen (PPC → C++) | ✅ (4 function hints) |
| Build / link | ⏳ |
| Boot / render / play | ⏳ |

## Building

You bring your own legally-dumped copy of the game — **no game data is included in
this repo** (and never will be).

```bash
# 1. Build the ReXGlue SDK (see its repo) and have Clang 20+, CMake 3.25+, Ninja.
# 2. Drop your dumped package in and extract the XEX + assets to extracted/.
# 3. Recompile and build:
rexglue codegen
cmake --preset win-amd64-release
cmake --build out/build/win-amd64-release
# 4. Run:
./out/build/win-amd64-release/afterburner.exe --game_data_root=extracted
```

Tooling and the full workflow live in [360tools](https://github.com/sp00nznet/360tools).

## Legal

This repository contains only original recompilation scaffolding and code. It
includes **no** game assets, executables, or copyrighted Sega material. After Burner
Climax is © Sega. Supply your own legally-obtained copy.
