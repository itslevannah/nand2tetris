---
layout: default
title: Or8Way Chip
nav_order : 12
---

# Or8Way Chip 

### 1. Or8Way Chip
An 8-way Or gate outputs 1 when at least one bit of its 16-bit input is 1.

Unlike n-bit input logic gates, n-way logic gates use the same output iteratively over the boolean operation, which means, it uses the previous output as input for the next similar boolean operation.

### 2.Truth Table

```markdown
| in[0] | in[1] | in[2] | in[3] | in[4] | in[5] | in[6] | in[7] | out |
|-------|-------|-------|-------|-------|-------|-------|-------|-----|
|   0   |   0   |   0   |   0   |   0   |   0   |   0   |   0   |  0  |
|   0   |   0   |   0   |   0   |   0   |   0   |   0   |   1   |  1  |
|   0   |   0   |   0   |   0   |   0   |   0   |   1   |   0   |  1  |
|   0   |   0   |   0   |   0   |   0   |   1   |   0   |   0   |  1  |
|   0   |   0   |   0   |   0   |   1   |   0   |   0   |   0   |  1  |
|   0   |   0   |   0   |   1   |   0   |   0   |   0   |   0   |  1  |
|   0   |   0   |   1   |   0   |   0   |   0   |   0   |   0   |  1  |
|   0   |   1   |   0   |   0   |   0   |   0   |   0   |   0   |  1  |
|   1   |   0   |   0   |   0   |   0   |   0   |   0   |   0   |  1  |
|   1   |   1   |   1   |   1   |   1   |   1   |   1   |   1   |  1  |
```

### 3. Implementation (Logisim)
Representation of the Or8Way Chip in the logisim software using the previous gates.

<img src="/nand2tetris/logisim/or8way.png" width="500" height="200px"/> 


### 4. Implementation (HDL)
Representation of the Mux16 Chip in HDL using previous gates..


```hdl
CHIP Or8Way {
    IN in[8];
    OUT out;

    PARTS:
    Or(a=in[0], b=in[1], out=o1);
    Or(a=o1, b=in[2], out=o2);
    Or(a=o2, b=in[3], out=o3);
    Or(a=o3, b=in[4], out=o4);
    Or(a=o4, b=in[5], out=o5);
    Or(a=o5, b=in[6], out=o6);
    Or(a=o6, b=in[7], out=out);
}
 ```
### 5. Video Tutorial
<iframe width="560" height="315" src="https://www.youtube.com/embed/xnyV7mmg_HI?si=Djh3uKI4ZbBWrKk6" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>