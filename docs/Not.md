---
layout: default
title: Not Gate
nav_order: 2
---
# NOT Gate  

### 1. Nand Gate (Given)
The starting point of Hack computer architecture is Nand Gate, from which all other gates and chips are built. Nand Gate is considered as primitive gate in nand2tetris course. You don't have to worry about its implementation for now.

<img src="/images/nand.png" width="500" height="200px" />

### 2. Not Gate 
The single-input Not Gate, also referred as Inverter, inverts the value of input.

<img src="/images/not.png" width="500" height="200px" /> 

### 3. Implementation (Logisim)
Representation of the Not gate in the logisim software using the Nand gate only.

<img src="/logisim/not.png" width="500" height="200px"/> 


### 4. Implementation (HDL)
Representation of the Not gate in HDL using the Nand gate only.


```hdl
CHIP Not {
    IN in;
    OUT out;

    PARTS:
    Nand(a=in, b=in, out=out);
}
 ```
