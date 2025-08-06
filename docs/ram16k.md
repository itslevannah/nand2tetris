---
layout: default
title: RAM16K Chip
nav_order : 28
---

# RAM16K Chip

### 1. RAM16K Chip

RAM16K is a memory chip consisting of 16,384 (2¹⁴) 16-bit words. It is constructed from 4 RAM4K chips. The chip takes a 14-bit address (address[14]) to select one of its 16K memory locations.

    The top 2 address bits (address[12..13]) select which of the 4 RAM4K chips to use.

    The bottom 12 bits (address[0..11]) select the register within the chosen RAM4K.

### 2. Truth Table

| address (14-bit) | in (16-bit)         | load | out (16-bit)        | Notes                                  |
|------------------|---------------------|------|----------------------|----------------------------------------|
| 00000000000000   | 0000000000000000    | 0    | previous value       | Reads old value from address 0         |
| 00000000000001   | 0000000000001111    | 1    | 0000000000001111     | Writes to address 1                    |
| 00000000000001   | 0000000000000000    | 0    | 0000000000001111     | Reads value back from address 1        |
| 11111111111111   | 1010101010101010    | 1    | 1010101010101010     | Writes to last address (16383)         |
| 11111111111111   | 0000000000000000    | 0    | 1010101010101010     | Reads value from last address          |



### 3. Implementation (HDL)

RAM16K is built using 4 RAM4K chips. The upper 2 address bits (address[12..13]) select the chip, and the lower 12 bits (address[0..11]) index into it.

```hdl
CHIP RAM16K {
    IN in[16], load, address[14];
    OUT out[16];

    PARTS:
    DMux4Way(in=load, sel=address[12..13], a=la, b=lb, c=lc, d=ld);

    RAM4K(in=in, load=la, address=address[0..11], out=ra);
    RAM4K(in=in, load=lb, address=address[0..11], out=rb);
    RAM4K(in=in, load=lc, address=address[0..11], out=rc);
    RAM4K(in=in, load=ld, address=address[0..11], out=rd);

    Mux4Way16(a=ra, b=rb, c=rc, d=rd, sel=address[12..13], out=out);
}
```
### 4. Video Tutorial
<iframe width="560" height="315" src="https://www.youtube.com/embed/_sJkrndqIDw?si=39liIxk8YRbtRxSz" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>