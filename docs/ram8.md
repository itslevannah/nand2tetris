---
layout: default
title: RAM8 Chip
nav_order : 24
---

# RAM8 Chip

### 1. RAM8 Chip

RAM8 is a memory chip that consists of 8 registers, each capable of holding a 16-bit value. It provides read/write access to one of these registers, based on a 3-bit address input. If load is 1, the value at in is stored in the selected register; otherwise, the stored value is retained..

<img src="\images\ram8.png" width="500" height="200px"/>


### 2. Truth Table

| address (3-bit) | in (16-bit)         | load | out (16-bit)        | Notes                                |
|-----------------|---------------------|------|----------------------|--------------------------------------|
| 000             | 0000000000000000    | 0    | previous value @ 000 | Holds old value at address 000       |
| 011             | 1111111111111111    | 1    | 1111111111111111     | Updates register 011 with new input |
| 011             | 0000000000000000    | 0    | 1111111111111111     | Reads updated value at address 011  |
| 100             | 1010101010101010    | 1    | 1010101010101010     | Updates register 100 with new input |
| 100             | 0000000000000000    | 0    | 1010101010101010     | Reads updated value at address 100  |

### 3. Implementation (Logisim)

Representation of the RAM8 in the logisim software

<img src="\logisim\ram8.png" width="500" height="200px"/>


### 4. Implementation (HDL)

RAM8 is built using 8 Register chips and a multiplexer/demultiplexer setup to route inputs and outputs based on the address.

```hdl
CHIP RAM8 {
    IN in[16], load, address[3];
    OUT out[16];

    PARTS:
    DMux8Way(in=load, sel=address, a=la, b=lb, c=lc, d=ld, e=le, f=lf, g=lg, h=lh);

    Register(in=in, load=la, out=ra);
    Register(in=in, load=lb, out=rb);
    Register(in=in, load=lc, out=rc);
    Register(in=in, load=ld, out=rd);
    Register(in=in, load=le, out=re);
    Register(in=in, load=lf, out=rf);
    Register(in=in, load=lg, out=rg);
    Register(in=in, load=lh, out=rh);

    Mux8Way16(a=ra, b=rb, c=rc, d=rd, e=re, f=rf, g=rg, h=rh, sel=address, out=out);
}

 ```