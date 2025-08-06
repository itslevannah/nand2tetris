---
layout: default
title: Mux4Way16
nav_order : 13
---

# Mux4Way16 Chip 

### 1. Mux4Way16 Chip
An 4-way 16-bit Multiplexor chip outputs one of the given four 16-bit inputs, which is specified by selector bit.

Unlike n-bit input logic gates, n-way logic gates use the same output iteratively over the boolean operation, which means, it uses the previous output as input for the next similar boolean operation.

<img src="/nand2tetris/images/mux4way16.png" width="500" height="200px"/> 

### 2. Truth Table

```markdown
| a[0] | b[0] | c[0] | d[0] | sel[0] | sel[1] | out[0] | ... | a[15] | b[15] | c[15] | d[15] | sel[0] | sel[1] | out[15] |
|------|------|------|------|--------|--------|--------|-----|-------|-------|-------|-------|--------|--------|---------|
|   0  |   0  |   0  |   0  |    0   |    0   |    0   | ... |   0   |   0   |   0   |   0   |    0   |    0   |    0    |
|   1  |   0  |   0  |   0  |    0   |    0   |    1   | ... |   1   |   0   |   0   |   0   |    0   |    0   |    1    |
|   0  |   1  |   0  |   0  |    0   |    1   |    1   | ... |   0   |   1   |   0   |   0   |    0   |    1   |    1    |
|   0  |   0  |   1  |   0  |    1   |    0   |    1   | ... |   0   |   0   |   1   |   0   |    1   |    0   |    1    |
|   0  |   0  |   0  |   1  |    1   |    1   |    1   | ... |   0   |   0   |   0   |   1   |    1   |    1   |    1    |
```

### 3. Implementation (Logisim)
Representation of the Mux4Way16 Chip in the logisim software using the previous gates.

<img src="/nand2tetris/logisim/mux4way16.png" width="500" height="200px"/> 


### 4. Implementation (HDL)
Representation of the Mux4Way16 Chip in HDL using previous gates.


```hdl
CHIP Mux4Way16 {
    IN a[16], b[16], c[16], d[16], sel[2];
    OUT out[16];

    PARTS:
    Mux16(a=a, b=b, sel=sel[0], out=ab);
    Mux16(a=c, b=d, sel=sel[0], out=cd);
    Mux16(a=ab, b=cd, sel=sel[1], out=out);
}
 ```
### 5. Video Tutorial
<iframe width="560" height="315" src="https://www.youtube.com/embed/Y9aiaY3iK7k?si=lLy9Dso9fskKCFFZ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>