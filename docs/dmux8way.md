---
layout: default
title: DMux8Way Gate
nav_order : 16
---

# DMux8Way Chip 

### 1. DMux8Way Chip

An 8-way Demultiplexor chip outputs the given input to certain output pin, which is specified by selector bit.

<img src="/nand2tetris/images/dmux8way.jpg" width="500" height="200px"/> 

### 2. Truth Table

```markdown
| in  | sel[2] | sel[1] | sel[0] | a  | b  | c  | d  | e  | f  | g  | h  |
|-----|--------|--------|--------|----|----|----|----|----|----|----|----|
|  0  |   0    |   0    |   0    |  0 |  0 |  0 |  0 |  0 |  0 |  0 |  0 |
|  0  |   0    |   0    |   1    |  0 |  0 |  0 |  0 |  0 |  0 |  0 |  0 |
|  0  |   0    |   1    |   0    |  0 |  0 |  0 |  0 |  0 |  0 |  0 |  0 |
|  0  |   0    |   1    |   1    |  0 |  0 |  0 |  0 |  0 |  0 |  0 |  0 |
|  0  |   1    |   0    |   0    |  0 |  0 |  0 |  0 |  0 |  0 |  0 |  0 |
|  0  |   1    |   0    |   1    |  0 |  0 |  0 |  0 |  0 |  0 |  0 |  0 |
|  0  |   1    |   1    |   0    |  0 |  0 |  0 |  0 |  0 |  0 |  0 |  0 |
|  0  |   1    |   1    |   1    |  0 |  0 |  0 |  0 |  0 |  0 |  0 |  0 |
|  1  |   0    |   0    |   0    |  1 |  0 |  0 |  0 |  0 |  0 |  0 |  0 |
|  1  |   0    |   0    |   1    |  0 |  1 |  0 |  0 |  0 |  0 |  0 |  0 |
|  1  |   0    |   1    |   0    |  0 |  0 |  1 |  0 |  0 |  0 |  0 |  0 |
|  1  |   0    |   1    |   1    |  0 |  0 |  0 |  1 |  0 |  0 |  0 |  0 |
|  1  |   1    |   0    |   0    |  0 |  0 |  0 |  0 |  1 |  0 |  0 |  0 |
|  1  |   1    |   0    |   1    |  0 |  0 |  0 |  0 |  0 |  1 |  0 |  0 |
|  1  |   1    |   1    |   0    |  0 |  0 |  0 |  0 |  0 |  0 |  1 |  0 |
|  1  |   1    |   1    |   1    |  0 |  0 |  0 |  0 |  0 |  0 |  0 |  1 |
```

### 3. Implementation (Logisim)
Representation of the DMux8Way Chip in the logisim software using the previous gates.

<img src="/nand2tetris/logisim/dmux8way.png" width="500" height="200px"/> 


### 4. Implementation (HDL)
Representation of the DMux8Way Chip in HDL using previous gates.


```hdl
CHIP DMux8Way {
    IN in, sel[3];
    OUT a, b, c, d, e, f, g, h;

    PARTS:
    DMux(in=in, sel=sel[2], a=abcd, b=efgh);
    DMux4Way(in=abcd, sel=sel[0..1], a=a, b=b, c=c, d=d);
    DMux4Way(in=efgh, sel=sel[0..1], a=e, b=f, c=g, d=h);
}
 ```
### 5. Video Tutorial
<iframe width="560" height="315" src="https://www.youtube.com/embed/sbDKBzMAiDU?si=tFDOU7Xo9PX7hVO6" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>