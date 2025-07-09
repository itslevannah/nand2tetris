---
layout: default
title: Mux8Way16
nav_order : 14
---

# Mux8Way16 Chip 

### 1. Mux8Way16 Chip
An 8-way 16-bit Multiplexor chip outputs one of the given eight 16-bit inputs, which is specified by selector bit.

<img src="/nand2tetris/images/mux8way16.jpg" width="500" height="200px"/> 

### 2. Truth Table

```markdown
| a[0] | b[0] | c[0] | d[0] | e[0] | f[0] | g[0] | h[0] | sel[0] | sel[1] | sel[2] | out[0] | ... | a[15] | b[15] | ... | h[15] | sel[0] | sel[1] | sel[2] | out[15] |
|------|------|------|------|------|------|------|------|--------|--------|--------|--------|-----|-------|-------|-----|-------|--------|--------|--------|---------|
|   0  |   0  |   0  |   0  |   0  |   0  |   0  |   0  |    0   |    0   |    0   |    0   | ... |   0   |   0   | ... |   0   |    0   |    0   |    0   |    0    |
|   1  |   0  |   0  |   0  |   0  |   0  |   0  |   0  |    0   |    0   |    0   |    1   | ... |   1   |   0   | ... |   0   |    0   |    0   |    0   |    1    |
|   0  |   1  |   0  |   0  |   0  |   0  |   0  |   0  |    0   |    0   |    1   |    1   | ... |   0   |   1   | ... |   0   |    0   |    0   |    1   |    1    |
|   0  |   0  |   1  |   0  |   0  |   0  |   0  |   0  |    0   |    1   |    0   |    1   | ... |   0   |   0   | ... |   0   |    0   |    1   |    0   |    1    |
|   0  |   0  |   0  |   1  |   0  |   0  |   0  |   0  |    0   |    1   |    1   |    1   | ... |   0   |   0   | ... |   0   |    0   |    1   |    1   |    1    |
|   0  |   0  |   0  |   0  |   1  |   0  |   0  |   0  |    1   |    0   |    0   |    1   | ... |   0   |   0   | ... |   0   |    1   |    0   |    0   |    1    |
|   0  |   0  |   0  |   0  |   0  |   1  |   0  |   0  |    1   |    0   |    1   |    1   | ... |   0   |   0   | ... |   0   |    1   |    0   |    1   |    1    |
|   0  |   0  |   0  |   0  |   0  |   0  |   1  |   0  |    1   |    1   |    0   |    1   | ... |   0   |   0   | ... |   0   |    1   |    1   |    0   |    1    |
|   0  |   0  |   0  |   0  |   0  |   0  |   0  |   1  |    1   |    1   |    1   |    1   | ... |   0   |   0   | ... |   0   |    1   |    1   |    1   |    1    |
```

### 3. Implementation (Logisim)
Representation of the Mux8Way16 Chip in the logisim software using the previous gates.

<img src="/nand2tetris/logisim/mux8way16.png" width="500" height="200px"/> 


### 4. Implementation (HDL)
Representation of the Mux8Way16 Chip in HDL using previous gates.


```hdl
CHIP Mux8Way16 {
    IN a[16], b[16], c[16], d[16],
       e[16], f[16], g[16], h[16],
       sel[3];
    OUT out[16];

    PARTS:
    Mux4Way16(a=a, b=b, c=c, d=d, sel=sel[0..1], out=abcd);
    Mux4Way16(a=e, b=f, c=g, d=h, sel=sel[0..1], out=efgh);
    
    Mux16(a=abcd, b=efgh, sel=sel[2], out=out);
}
 ```