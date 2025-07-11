---
layout: default
title: RAM4K Chip
nav_order : 27
---

# RAM4K Chip

### 1. RAM4K Chip

RAM4K is a memory chip that stores 4,096 (2¹²) 16-bit words. It is built using 8 RAM512 chips. The input address[12] selects one of the 4,096 registers for read or write. The upper 3 bits (address[9..11]) choose which RAM512 chip to access, while the lower 9 bits (address[0..8]) specify the register inside that chip.



### 2. Truth Table

| address (12-bit) | in (16-bit)         | load | out (16-bit)        | Notes                                |
|-------------------|---------------------|------|----------------------|--------------------------------------|
| 000000000000      | 0000000000000000    | 0    | previous value       | No update, reads old value           |
| 000000000101      | 0000000000001111    | 1    | 0000000000001111     | Writes to address 000000000101       |
| 000000000101      | 0000000000000000    | 0    | 0000000000001111     | Reads stored value from that address |
| 110101011010      | 1010101010101010    | 1    | 1010101010101010     | Writes to address 110101011010       |
| 110101011010      | 0000000000000000    | 0    | 1010101010101010     | Reads stored value                   |



### 3. Implementation (HDL)

RAM4K uses 8 RAM512 chips. The top 3 address bits select the RAM512, and the lower 9 bits are passed to the selected chip.

```hdl
CHIP RAM4K {
    IN in[16], load, address[12];
    OUT out[16];

    PARTS:
    DMux8Way(in=load, sel=address[9..11], a=la, b=lb, c=lc, d=ld, e=le, f=lf, g=lg, h=lh);

    RAM512(in=in, load=la, address=address[0..8], out=ra);
    RAM512(in=in, load=lb, address=address[0..8], out=rb);
    RAM512(in=in, load=lc, address=address[0..8], out=rc);
    RAM512(in=in, load=ld, address=address[0..8], out=rd);
    RAM512(in=in, load=le, address=address[0..8], out=re);
    RAM512(in=in, load=lf, address=address[0..8], out=rf);
    RAM512(in=in, load=lg, address=address[0..8], out=rg);
    RAM512(in=in, load=lh, address=address[0..8], out=rh);

    Mux8Way16(a=ra, b=rb, c=rc, d=rd, e=re, f=rf, g=rg, h=rh, sel=address[9..11], out=out);
}
```