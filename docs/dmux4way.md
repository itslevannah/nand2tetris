---
layout: default
title: DMux4Way Gate
nav_order : 15
---

# DMux4Way Chip 

### 1. DMux4Way Chip
An 4-way Demultiplexor chip outputs the given input to certain output pin, which is specified by selector bit.

<img src="\images\dmux4way.avif" width="500" height="200px"/> 

### 2. Truth Table

```markdown
| in  | sel[1] | sel[0] | a  | b  | c  | d  |
|-----|--------|--------|----|----|----|----|
|  0  |   0    |   0    |  0 |  0 |  0 |  0 |
|  0  |   0    |   1    |  0 |  0 |  0 |  0 |
|  0  |   1    |   0    |  0 |  0 |  0 |  0 |
|  0  |   1    |   1    |  0 |  0 |  0 |  0 |
|  1  |   0    |   0    |  1 |  0 |  0 |  0 |
|  1  |   0    |   1    |  0 |  1 |  0 |  0 |
|  1  |   1    |   0    |  0 |  0 |  1 |  0 |
|  1  |   1    |   1    |  0 |  0 |  0 |  1 |
```

### 3. Implementation (Logisim)
Representation of the DMux4Way Chip in the logisim software using the previous gates.

<img src="\logisim\dmux4way.png" width="500" height="200px"/> 


### 4. Implementation (HDL)
Representation of the DMux4Way Chip in HDL using previous gates.


```hdl
CHIP DMux4Way {
    IN in, sel[2];
    OUT a, b, c, d;

    PARTS:
    DMux(in=in, sel=sel[1], a=ab, b=cd);
    DMux(in=ab, sel=sel[0], a=a, b=b);
    DMux(in=cd, sel=sel[0], a=c, b=d);
}
 ```