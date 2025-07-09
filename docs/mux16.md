---
layout: default
title: Mux16 Chip
nav_order : 11
---

# Mux16 Chip 

### 1. Mux16 Chip
An 16-bit multiplexor is almost similar to the Multiplexor Chip described previously, except that both inputs are each 16-bit wide, while the selector is a single bit.



### 2. Truth Table

```markdown
| a[0] | b[0] | sel | out[0] | a[1] | b[1] | sel | out[1] | ... | a[15] | b[15] | sel | out[15] |
|------|------|-----|--------|------|------|-----|--------|-----|-------|-------|-----|---------|
|  0   |  0   |  0  |   0    |  0   |  0   |  0  |   0    | ... |   0   |   0   |  0  |    0    |
|  0   |  1   |  0  |   0    |  0   |  1   |  0  |   0    | ... |   0   |   1   |  0  |    0    |
|  1   |  0   |  0  |   1    |  1   |  0   |  0  |   1    | ... |   1   |   0   |  0  |    1    |
|  1   |  1   |  0  |   1    |  1   |  1   |  0  |   1    | ... |   1   |   1   |  0  |    1    |
|  0   |  0   |  1  |   0    |  0   |  0   |  1  |   0    | ... |   0   |   0   |  1  |    0    |
|  0   |  1   |  1  |   1    |  0   |  1   |  1  |   1    | ... |   0   |   1   |  1  |    1    |
|  1   |  0   |  1  |   0    |  1   |  0   |  1  |   0    | ... |   1   |   0   |  1  |    0    |
|  1   |  1   |  1  |   1    |  1   |  1   |  1  |   1    | ... |   1   |   1   |  1  |    1    |
```

### 3. Implementation (Logisim)
Representation of the Mux16 Chip in the logisim software using the previous Chips.

<img src="/nand2tetris/logisim/mux16.png" width="500" height="200px"/> 


### 4. Implementation (HDL)
Representation of the Mux16 Chip in HDL using previous Chips.


```hdl
CHIP Mux16 {
    IN a[16], b[16], sel;
    OUT out[16];

    PARTS:
    Mux(a=a[0], b=b[0], sel=sel, out=out[0]);
    Mux(a=a[1], b=b[1], sel=sel, out=out[1]);
    Mux(a=a[2], b=b[2], sel=sel, out=out[2]);
    Mux(a=a[3], b=b[3], sel=sel, out=out[3]);
    Mux(a=a[4], b=b[4], sel=sel, out=out[4]);
    Mux(a=a[5], b=b[5], sel=sel, out=out[5]);
    Mux(a=a[6], b=b[6], sel=sel, out=out[6]);
    Mux(a=a[7], b=b[7], sel=sel, out=out[7]);
    Mux(a=a[8], b=b[8], sel=sel, out=out[8]);
    Mux(a=a[9], b=b[9], sel=sel, out=out[9]);
    Mux(a=a[10], b=b[10], sel=sel, out=out[10]);
    Mux(a=a[11], b=b[11], sel=sel, out=out[11]);
    Mux(a=a[12], b=b[12], sel=sel, out=out[12]);
    Mux(a=a[13], b=b[13], sel=sel, out=out[13]);
    Mux(a=a[14], b=b[14], sel=sel, out=out[14]);
    Mux(a=a[15], b=b[15], sel=sel, out=out[15]);
}
 ```