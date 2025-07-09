---
layout: default
title: DMux Chip
nav_order : 7
---

# DMux Chip 

### 1. DMux Chip
A Demultiplexer (DMux) performs the inverse function of a Multiplexer (Mux). It takes a single input (in) and routes it to one of two outputs (a or b), depending on the value of a selector bit (sel).

    If sel = 0, the input is directed to output a.

    If sel = 1, the input is directed to output b.

<img src="/nand2tetris/images/dmux.png" width="500" height="200px"/> 


### 2. Implementation (Logisim)
Representation of the DMux Chip in the logisim software using the previous gates.

<img src="/nand2tetris/logisim/dmux.png" width="500" height="200px"/> 


### 3. Implementation (HDL)
Representation of the DMux Chip in HDL using previous gates.


```hdl
CHIP DMux {
    IN in, sel;
    OUT a, b;

    PARTS:
    Not(in=sel, out=notsel);      // Invert the selector bit
    And(a=in, b=notsel, out=a);    // Output 'in' to 'a' if sel=0
    And(a=sel, b=in, out=b);       // Output 'in' to 'b' if sel=1
}
 ```