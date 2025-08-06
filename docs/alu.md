---
layout: default
title: ALU
nav_order : 21
---

# ALU Arithmetic Logic Unit

### 1. ALU

The Hack ALU computes 18 possible functions on two 16-bit inputs (x, y), selected by 6 control bits. It outputs:

    A 16-bit result (out).

    Two status flags:

        zr (Zero): 1 if out == 0, else 0.

        ng (Negative): 1 if out < 0 (MSB = 1), else 0.


<img src="/nand2tetris/images/alu.avif" width="500" height="200px"/> 

### 2. Truth Table
<img src="/nand2tetris/images/alutt.avif" width="500" height="200px"/> 


### 3. Implementation (Logisim)

Representation of the ALU in the logisim software using the previous gates.
The ALU is built using:

    Multiplexers (Mux16) for zeroing/negating inputs.

    Add16 and And16 for arithmetic/logic operations.

    Not16 for conditional negation.

    Or16Way + Not for zero detection.



<img src="/nand2tetris/logisim/alu.png" width="500" height="200px"/> 

#### **3.1 Control bits:**

zx -- essentially named as zerox -- states whether x is 0 or not -- if zx = true, then x = 0.

nx -- essentially named as negationx -- states whether x will undergo negation or not -- if nx = true, then x will undergo negation.

zy -- essentially named as zeroy -- states whether y is 0 or not -- if zy = true, then y = 0.

ny -- essentially named as negationy -- states whether y will undergo negation or not -- if ny = true, then y will undergo negation.

f -- essentially named as function -- states whether addition or and function is selected -- if f = true, then execute function x + y ; else x & y

no -- essentially named as negationout -- states whether output will undergo negaton or not -- if no = true, then out will undergo negation.

#### **3.2 Output bits:**

While output bits other than out is not shown in the truth table, there are two output bits -- zr & ng -- other than out.

zr -- essentially named as zero -- states whether the final output is zero or not. -- if out = 0; zr = true

ng -- essentially named as negative -- states whether the final output is negative or not. -- if out = negative; ng = true

### 4. Implementation (HDL)

The ALU can be implemented using some of the gates we've learnt earlier.


```hdl
CHIP ALU {
    IN  
        x[16], y[16],      // 16-bit inputs  
        zx, nx, zy, ny,    // Input modifiers  
        f, no;             // Function/Output modifiers  

    OUT  
        out[16],           // 16-bit result  
        zr, ng;            // Flags: zero/negative  

    PARTS:  
    // Preprocess X (zx, nx)  
    Mux16(a=x, b=false, sel=zx, out=zerox);  
    Not16(in=zerox, out=notx);  
    Mux16(a=zerox, b=notx, sel=nx, out=prex);  

    // Preprocess Y (zy, ny)  
    Mux16(a=y, b=false, sel=zy, out=zeroy);  
    Not16(in=zeroy, out=noty);  
    Mux16(a=zeroy, b=noty, sel=ny, out=prey);  

    // Compute f(x,y)  
    Add16(a=prex, b=prey, out=addxy);      // x + y  
    And16(a=prex, b=prey, out=andxy);      // x & y  
    Mux16(a=andxy, b=addxy, sel=f, out=fxy);  

    // Postprocess output (no)  
    Not16(in=fxy, out=notfxy);  
    Mux16(a=fxy, b=notfxy, sel=no, out=out, out[15]=ng, out[0..7]=zr1 , out[8..15]=zr2);  

    // Zero/negative flags  
    Or8Way(in=zr1, out=or1)
    Or8Way(in=zr, out=or2)
    Or(a=zr1 , b=zr2 , out=prezr)
    Not(in=prezr, out=zr);                 // zr = 1 iff out == 0  
}
 ```
### 5. Video Tutorial
<iframe width="560" height="315" src="https://www.youtube.com/embed/fOo2wle4uKY?si=LJHyn_AgoMXPcUcH" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>