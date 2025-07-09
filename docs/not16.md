---
layout: default
title: Not16 Chip
nav_order : 8
---

# Not16 Chip 

### 1. Not16 Chip
Unlike a single Not gate, the Not16 chip takes a 16-bit input bus and applies a bitwise NOT operation to each bit, producing a 16-bit output.
In other words:

    If input bit in[i] = 0, then out[i] = 1.

    If input bit in[i] = 1, then out[i] = 0.


### 2. Truth Table

```markdown
| in[0] | out[0] | in[1] | out[1] | ... | in[15] | out[15] |
|-------|--------|-------|--------|-----|--------|---------|
|   0   |   1    |   0   |   1    | ... |   0    |    1    |
|   1   |   0    |   1   |   0    | ... |   1    |    0    |
```

### 3. Implementation (Logisim)
Representation of the Not16 Chip in the logisim software using the previous gates.

<img src="\logisim\not16.png" width="500" height="200px"/> 


### 4. Implementation (HDL)
Representation of the Not16 Chip in HDL using previous gates.


```hdl
CHIP Not16 {
    IN in[16];
    OUT out[16];

    PARTS:
    Not(in=in[0], out=out[0]);
    Not(in=in[1], out=out[1]);
    Not(in=in[2], out=out[2]);
    Not(in=in[3], out=out[3]);
    Not(in=in[4], out=out[4]);
    Not(in=in[5], out=out[5]);
    Not(in=in[6], out=out[6]);
    Not(in=in[7], out=out[7]);
    Not(in=in[8], out=out[8]);
    Not(in=in[9], out=out[9]);
    Not(in=in[10], out=out[10]);
    Not(in=in[11], out=out[11]);
    Not(in=in[12], out=out[12]);
    Not(in=in[13], out=out[13]);
    Not(in=in[14], out=out[14]);
    Not(in=in[15], out=out[15]);
}
 ```