---
layout: default
title: Register Chip
nav_order : 23
---

# Register Chip

### 1. Register Chip

The Register is a 16-bit storage unit. It stores a 16-bit value and either maintains the stored value or updates it based on the load control bit.

<img src="\images\register.png" width="500" height="200px"/> 


### 2. Truth Table

| in (16-bit)         | load | out (16-bit)        | Notes                            |
|---------------------|------|---------------------|----------------------------------|
| 0000000000000000    | 0    | previous value      | Holds previous 16-bit value     |
| 1111111111111111    | 0    | previous value      | No update, holds previous value |
| 1010101010101010    | 1    | 1010101010101010    | Updates with new input value    |
| 0000000000000000    | 1    | 0000000000000000    | Updates with all 0s             |



### 3. Implementation (HDL)

The Register chip is built using 16 Bit chips — one for each bit of the 16-bit value.

```hdl
CHIP Register {
    IN in[16], load;
    OUT out[16];

    PARTS:
    Bit(in=in[0], load=load, out=out[0]);
    Bit(in=in[1], load=load, out=out[1]);
    Bit(in=in[2], load=load, out=out[2]);
    Bit(in=in[3], load=load, out=out[3]);
    Bit(in=in[4], load=load, out=out[4]);
    Bit(in=in[5], load=load, out=out[5]);
    Bit(in=in[6], load=load, out=out[6]);
    Bit(in=in[7], load=load, out=out[7]);
    Bit(in=in[8], load=load, out=out[8]);
    Bit(in=in[9], load=load, out=out[9]);
    Bit(in=in[10], load=load, out=out[10]);
    Bit(in=in[11], load=load, out=out[11]);
    Bit(in=in[12], load=load, out=out[12]);
    Bit(in=in[13], load=load, out=out[13]);
    Bit(in=in[14], load=load, out=out[14]);
    Bit(in=in[15], load=load, out=out[15]);
}

 ```