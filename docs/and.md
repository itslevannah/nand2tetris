---
layout: default
title: And Gate
nav_order: 3
---
# And Gate 

### 1. And Gate
The And gate returns true, only when both of the inputs are true.

<img src="/nand2tetris/images/and.jpg" width="500" height="200px"/> 


### 2. Implementation (Logisim)
Representation of the And gate in the logisim software using the Nand and the Not gates only.

<img src="/nand2tetris/logisim/and.png" width="500" height="200px"/> 


### 3. Implementation (HDL)
Representation of the And gate in HDL using previous gates.


```hdl
CHIP And {
    IN a, b;
    OUT out;

    PARTS:
    Nand(a=a, b=b, c=notout);
    Not(in=notout, out=out);
}
 ```