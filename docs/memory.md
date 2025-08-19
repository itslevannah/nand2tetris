---
layout: default
title: Memory Chip
nav_order : 32
---

# Memory Chip

### 1. Memory Chip

The Memory chip is the top-level abstraction of the Hack computer's general-purpose memory. It integrates:

    RAM16K – the main user-accessible memory

    Screen – mapped to memory addresses 16384 to 24575

    Keyboard – mapped to memory address 24576

It receives a 16-bit address, a 16-bit in, a load signal, and produces a 16-bit out. Depending on the address:

    address[14..] == 0 → RAM16K (0–16383)

    address[14..] == 1 and address < 24576 → Screen (16384–24575)

    address == 24576 → Keyboard

<img src="/nand2tetris/images/memory.avif" width="500" height="200px"/>


### 2. Truth Table

| address (15-bit) | in (16-bit)         | load | out (16-bit)        | Memory Target | Notes                                 |
|------------------|---------------------|------|----------------------|----------------|---------------------------------------|
| 000000000000000  | 0000000000000001    | 1    | 0000000000000001     | RAM16K         | Writes to general memory (RAM[0])     |
| 001111111111111  | 1111111111111111    | 1    | 1111111111111111     | RAM16K         | Writes to RAM[8191]                   |
| 010000000000000  | 1010101010101010    | 1    | 1010101010101010     | Screen         | Writes to Screen[0] (address 16384)   |
| 010011111111111  | 0000000000000000    | 0    | current screen value | Screen         | Reads from Screen[8191]               |
| 011000000000000  | x                   | 0    | 0000000000000001     | Keyboard       | Reads key input                       |



### 3. Implementation (HDL)

Memory uses 1 RAM16K, 1 Screen chip, and 1 Keyboard chip. Routing is based on the upper bits of the address.

```hdl
CHIP Memory {
    IN in[16], load, address[15];
    OUT out[16];

    PARTS:
    // ---------------------------------------------------------
    // Address ranges:
    //   0–16383   : RAM16K
    //   16384–24575 : Screen
    //   24576     : Keyboard
    // ---------------------------------------------------------

    // RAM select: address[14] = 0
    Not(in=address[14], out=ramSel);
    And(a=ramSel, b=load, out=loadRam);

    // Screen select: address[14] = 1 AND address[13] = 0
    Not(in=address[13], out=notA13);
    And(a=address[14], b=notA13, out=screenSel);
    And(a=screenSel, b=load, out=loadScreen);

    // RAM16K block
    RAM16K(in=in, load=loadRam, address=address[0..13], out=ramOut);

    // Screen block
    Screen(in=in, load=loadScreen, address=address[0..12], out=screenOut);

    // Keyboard block
    Keyboard(out=keyOut);

    // Output selection:
    // First choose between RAM and Screen (based on address[14])
    Mux16(a=ramOut, b=screenOut, sel=address[14], out=ramOrScreen);

    // Then choose between (RAM/Screen) vs Keyboard
    And(a=address[14], b=address[13], out=keySel);
    Mux16(a=ramOrScreen, b=keyOut, sel=keySel, out=out);
}

 ```
