---
layout: default
title: XOr Gate
nav_order: 5
---

# xor Gate 

### 1. XOr Gate
The Xor gate, known as Exclusive-OR, returns true when the inputs are different (one is 0, the other is 1).

<img src="\images\xor.png" width="500" height="200px"/> 


### 2. Implementation (Logisim)
Representation of the xor gate in the logisim software using the Nxor xor the Not gates only.

<img src="\logisim\xor.png" width="500" height="200px"/> 


### 3. Implementation (HDL)
Representation of the xor gate in HDL using previous gates.


```hdl
CHIP Xor {
    IN a, b;
    OUT out;

    PARTS:
    Not(in=a, out=nota);
    Not(in=b, out=notb);
    And(a=a, b=notb, out=aAndNotb);
    And(a=nota, b=b, out=notaAndb);
    Or(a=aAndNotb, b=notaAndb, out=out);
}
 ```
#### Alternative solution
 ```hdl
 CHIP Xor {
    IN a, b;
    OUT out;

    PARTS:
    Nand(a=a, b=b, out=nandAB);       // (a NAND b)
    Nand(a=a, b=nandAB, out=nandA);   // (a NAND (a NAND b))
    Nand(a=b, b=nandAB, out=nandB);    // (b NAND (a NAND b))
    Nand(a=nandA, b=nandB, out=out);  // Final XOR
}
 ```
