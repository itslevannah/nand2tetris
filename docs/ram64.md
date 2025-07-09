---
layout: default
title: RAM64 Chip
nav_order : 25
---

# RAM64 Chip

### 1. RAM64 Chip

RAM64 is a memory chip composed of 64 registers (from address 000000 to 111111), each capable of holding a 16-bit value. It allows read and write access to one of the 64 registers based on a 6-bit address input.

Internally, RAM64 is built using 8 RAM8 chips and a tree of multiplexers/demultiplexers.


### 2. Truth Table

| address (6-bit) | in (16-bit)         | load | out (16-bit)        | Notes                                 |
|------------------|---------------------|------|----------------------|---------------------------------------|
| 000000           | 0000000000000000    | 0    | previous value @ 000000 | No update, reads old value         |
| 000011           | 1111111111111111    | 1    | 1111111111111111     | Writes to address 000011             |
| 000011           | 0000000000000000    | 0    | 1111111111111111     | Reads the stored value at 000011     |
| 101010           | 1010101010101010    | 1    | 1010101010101010     | Writes to address 101010             |
| 101010           | 0000000000000000    | 0    | 1010101010101010     | Reads updated value from 101010      |




### 3. Implementation (Logisim)

Representation of the RAM8 in the logisim software

<img src="\logisim\ram64.png" width="500" height="200px"/>

### 4. Implementation (HDL)

RAM64 is composed of 8 RAM8 chips. The top 3 bits of the address (address[3..5]) select which RAM8 chip to activate, while the bottom 3 bits (address[0..2]) select the register within that RAM8.

```hdl
CHIP RAM64 {
    IN in[16], load, address[6];
    OUT out[16];

    PARTS:
    DMux8Way(in=load, sel=address[3..5], a=la, b=lb, c=lc, d=ld, e=le, f=lf, g=lg, h=lh);

    RAM8(in=in, load=la, address=address[0..2], out=ra);
    RAM8(in=in, load=lb, address=address[0..2], out=rb);
    RAM8(in=in, load=lc, address=address[0..2], out=rc);
    RAM8(in=in, load=ld, address=address[0..2], out=rd);
    RAM8(in=in, load=le, address=address[0..2], out=re);
    RAM8(in=in, load=lf, address=address[0..2], out=rf);
    RAM8(in=in, load=lg, address=address[0..2], out=rg);
    RAM8(in=in, load=lh, address=address[0..2], out=rh);

    Mux8Way16(a=ra, b=rb, c=rc, d=rd, e=re, f=rf, g=rg, h=rh, sel=address[3..5], out=out);
}
 ``` 