---
layout: default
title: Bit Chip
nav_order : 22
---

# Bit Chip

### 1. Bit Chip

The Bit chip stores a single bit of data. It acts like a 1-bit register that can either maintain its previous state or update based on the load input signal.

<img src="\images\bit.png" width="500" height="200px"/> 

### 2. Truth Table

| in | load | out | Notes                            |
|----|------|-----|----------------------------------|
|  0 |   0  |  ?  | Keeps previous value (no update) |
|  1 |   0  |  ?  | Keeps previous value (no update) |
|  0 |   1  |  0  | Updates stored value to 0        |
|  1 |   1  |  1  | Updates stored value to 1        |


### 3. Implementation (Logisim)

Representation of the Bit Chip using a DFF and Mux to control updating.

<img src="\logisim\bit.png" width="500" height="200px"/> 


### 4. Implementation (HDL)

The Bit chip uses a D flip-flop to store state, and a Mux to decide whether to load a new input or keep the current one.


```hdl
CHIP Bit {
    IN in, load;
    OUT out;

    PARTS:
    Mux(a=out, b=in, sel=load, out=muxOut);
    DFF(in=muxOut, out=out);
}
 ```