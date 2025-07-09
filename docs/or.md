---
layout: default
title: Or Gate
nav_order: 4
---
# Or Gate 

### 1. Or Gate
The Or gate returns true, when either of the inputs are true.

<img src="\images\or.jpg" width="500" height="200px"/> 


### 2. Implementation (Logisim)
Representation of the Or gate in the logisim software using the Nand and the Not gates only.
We can represent the Or gate in both ways circuits in the image!
<img src="\logisim\or.png" width="500" height="200px"/> 


### 3. Implementation (HDL)
Representation of the Or gate in HDL using previous gates.


```hdl
CHIP Or {
    IN a, b;
    OUT out;

    PARTS:
    Not(in=a, out=nota);
    Not(in=b, out=notb);
    Nand(a=nota, b=notb, out=out);
}
 ```