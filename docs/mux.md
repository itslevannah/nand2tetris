---
layout: default
title: Mux Chip
nav_order: 6
---

# Mux Chip 

### 1. Mux Chip
A Multiplexer, is a three-input bit chip that uses one of the inputs, called the "selection bit" (sel), to select and output one of the other two inputs (a or b).

    When sel = 0, the output is a.

    When sel = 1, the output is b.

<img src="\images\mux.png" width="500" height="200px"/> 


### 2. Implementation (Logisim)
Representation of the Mux Chip in the logisim software using the previous gates.

<img src="\logisim\mux.png" width="500" height="200px"/> 


### 3. Implementation (HDL)
Representation of the Mux Chip in HDL using previous gates.


```hdl
CHIP Mux {
    IN a, b, sel;
    OUT out;

    PARTS:
    Not(in=sel, out=notsel);     // Invert the selection bit
    And(a=a, b=notsel, out=aAndNotSel);  // If sel=0, pass 'a'
    And(a=sel, b=b, out=bAndSel);        // If sel=1, pass 'b'
    Or(a=aAndNotSel, b=bAndSel, out=out); // Output the selected value
}
 ```