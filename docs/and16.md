---
layout: default
title: And16 Chip
nav_order : 9
---

# And16 Chip 

### 1. And16 Chip
The And16 chip performs a bitwise AND operation on two 16-bit inputs (a and b), producing a 16-bit output (out).

    Each output bit out[i] is the result of a[i] AND b[i] (for i = 0..15).

    This is a parallel operation—all 16 bits are processed simultaneously.

### 2. Truth Table

```markdown
| a[0] | b[0] | out[0] | a[1] | b[1] | out[1] | ... | a[15] | b[15] | out[15] |
|------|------|--------|------|------|--------|-----|-------|-------|---------|
|  0   |  0   |   0    |  0   |  0   |   0    | ... |   0   |   0   |    0    |
|  0   |  1   |   0    |  0   |  1   |   0    | ... |   0   |   1   |    0    |
|  1   |  0   |   0    |  1   |  0   |   0    | ... |   1   |   0   |    0    |
|  1   |  1   |   1    |  1   |  1   |   1    | ... |   1   |   1   |    1    |
```
Example:

    If a = 0b1100 and b = 0b1010 (4-bit simplification), then out = 0b1000.

    Extend this logic to 16 bits.

### 2. Implementation (Logisim)
Representation of the And16 Chip in the logisim software using the previous gates.

    Built using 16 individual AND gates, each processing one bit of the input buses.

<img src="\logisim\and16.png" width="500" height="200px"/> 


### 3. Implementation (HDL)
Representation of the And16 Chip in HDL using previous gates.


```hdl
CHIP And16 {
    IN a[16], b[16];
    OUT out[16];

    PARTS:
    And(a=a[0], b=b[0], out=out[0]);
    And(a=a[1], b=b[1], out=out[1]);
    And(a=a[2], b=b[2], out=out[2]);
    And(a=a[3], b=b[3], out=out[3]);
    And(a=a[4], b=b[4], out=out[4]);
    And(a=a[5], b=b[5], out=out[5]);
    And(a=a[6], b=b[6], out=out[6]);
    And(a=a[7], b=b[7], out=out[7]);
    And(a=a[8], b=b[8], out=out[8]);
    And(a=a[9], b=b[9], out=out[9]);
    And(a=a[10], b=b[10], out=out[10]);
    And(a=a[11], b=b[11], out=out[11]);
    And(a=a[12], b=b[12], out=out[12]);
    And(a=a[13], b=b[13], out=out[13]);
    And(a=a[14], b=b[14], out=out[14]);
    And(a=a[15], b=b[15], out=out[15]);
}
 ```