# tetris_asm

**Tetris written in MIT Beta assembly**, targeting a custom 32-bit Beta CPU running on an FPGA. This repository contains the **software** half of the project: the game logic, rendering routines, and data, all written directly in Beta assembly.

> **This is 1 of 2 repositories.** This code doesn't run on a normal computer — it runs on a custom-built processor. The CPU (and the FPGA hardware it lives on) is in a separate repo:
> **➡️ [niclukman/tetris-cpu](https://github.com/niclukman/tetris-cpu)** — the 32-bit Beta CPU that executes this program.
>
> You need both halves for the full project: this repo is the program, the other repo is the machine it runs on.

## Overview

The entire game is implemented in [MIT Beta](https://en.wikipedia.org/wiki/Beta_(instruction_set_architecture)) assembly — no compiler, no high-level language. It covers the full Tetris loop: piece spawning and movement, collision detection, line-clearing, and writing to a framebuffer that the CPU's VGA controller draws to a **640×480 display at 60 Hz**.

## Repository structure

The assembler keeps instruction and data memory in **separate files**, matching the two sources here:

| File | Description |
|------|-------------|
| `tetris.uasm` | Instruction memory: game logic, input handling, rendering routines |
| `tetris_data.uasm` | Data memory: piece/sprite definitions, board layout, lookup tables |

## Assembling

These `.uasm` files are assembled with the Python **[natalieagus/beta-assembler](https://github.com/natalieagus/beta-assembler)** (32-bit MIT Beta ISA, built for the 50.002 1D project on the Alchitry Au). The assembler picks up `tetris.uasm` as instruction memory and `tetris_data.uasm` as data memory automatically from the shared base name.

This produces `files/tetris.hex` (instruction memory) and `files/tetris_data.hex` (data memory) alongside the sources.

## Running

This program only runs on the accompanying CPU. To actually play:

1. Assemble the sources here into `.hex` memory images 
2. Load those images into the CPU design and flash it to the FPGA — see **[niclukman/tetris-cpu](https://github.com/niclukman/tetris-cpu)** for build & flash instructions


## Related

- **CPU / hardware:** [niclukman/tetris-cpu](https://github.com/niclukman/tetris-cpu)
