# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a tutorial repository for learning **Amos Pro 2.x** programming on the **Commodore Amiga**. It contains 14 progressive code snippets demonstrating graphics, audio, and hardware techniques, targeting a vanilla Amiga 500 (OCS/ECS chipset, 512KB chip RAM + 512KB RAM).

Amos Pro is a BASIC dialect for the Amiga. The code requires the **AMCAF** and **Amos Turbo** extensions (bundled in the community edition).

## Repository Structure

Each snippet lives in `snippet-NNN_description/` with:
- `src/*.amos` — Binary Amos Pro format (contains embedded data banks)
- `src/*.amo` — Plain text version (readable, no banks)
- `src/assets/` — IFF graphics and MOD music files (when needed)
- `README.md` — Detailed explanation of the snippet's techniques
- `readImg/` — Screenshots and diagrams

The `releases/` directory contains Amiga disk images (`.adf` files).

## Development Environment

There is no build system. Source files are loaded directly into Amos Pro 2.x Community Edition (2020.1), which runs on an Amiga or Amiga emulator (e.g., WinUAE). Download link in the main README.md.

## Architecture and Key Concepts

The snippets follow a progression through Amiga programming topics:

- **3D wireframes and solids** (snippets 1, 8, 9): rotation matrices, projection, backface culling — all using integer-only arithmetic for 50 FPS on 7MHz 68000
- **2D scrolling and playfields** (snippets 3, 4, 6): dual/triple playfield modes, hardware scrolling, sinusoidal animation
- **Sprites and bobs** (snippets 5, 10, 14): hardware sprites (max 8), blitter objects, AMAL animation language for parallel sprite control
- **Copper list programming** (snippet 11): direct manipulation of Amiga copper coprocessor for color gradient effects
- **Audio** (snippet 7): Protracker MOD playback via Amos tracker commands
- **Hardware I/O** (snippet 12): joystick multi-button reading via hardware registers (Peek/Poke/Deek/Doke)

**Common pattern across snippets:**
```
Main Loop (VBL synchronized)
  ├── Input reading (joystick/keyboard)
  ├── Computation (integer math, transformations)
  ├── Rendering (blitter ops, screen drawing)
  ├── AMAL channel updates (parallel animation)
  └── Screen Swap / Wait VBL
```

## Working with the Code

- `.amo` files are the human-readable source — use these for code review and analysis
- `.amos` files are the runnable binaries with embedded asset banks — these cannot be meaningfully diffed
- All math is integer-only (no floating point) to maintain 50 FPS on the target hardware
- Programs are synchronized to the PAL vertical blank (50Hz)
- Double buffering is used throughout for flicker-free animation
