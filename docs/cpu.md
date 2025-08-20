---
layout: default
title: CPU Chip
nav_order : 33
---

# CPU Chip

### 1. CPU Chip

The CPU (Central Processing Unit) is the brain of the Hack computer. It:

    Executes instructions received from memory.

    Handles both A-instructions (addressing) and C-instructions (computation).

    Controls the Program Counter (PC).

    Interfaces with Memory, ALU, and A/D registers.

It receives a 16-bit instruction and computes the next values for the outM, writeM, addressM, and pc outputs.

<img src="/nand2tetris/images/cpu.png" width="500" height="200px"/>


### 2. Truth Table

| instruction[15] | Type         | Operation                                     |
|------------------|--------------|-----------------------------------------------|
| 0                | A-instruction| Set A register to instruction[0..14]          |
| 1                | C-instruction| Perform ALU operation and control flow        |

#### Key outputs and behaviors:

| input              | output                 | Description                                              |
|--------------------|------------------------|----------------------------------------------------------|
| instruction        | outM                   | ALU result, to be written to memory (if writeM = 1)     |
| instruction[3]     | writeM                 | Set to 1 if result is to be written to memory            |
| instruction[0..2]  | jump bits              | Determine whether to jump based on ALU output            |
| ALU out == 0       | Jump if j1 or j2 is set| Conditional jump logic                                   |
| instruction[10..6] | comp bits              | Determines ALU computation                               |
| instruction[5..3]  | dest bits              | Where to store ALU result (A, D, or M)                   |
| reset == 1         | pc = 0                 | Forces PC to reset                                       |

### 3. Implementation (HDL)

The CPU combines the ALU, Register, and Program Counter (PC), and routes control based on instruction bits.

```hdl
CHIP CPU {
    IN  inM[16],          // M value input  (from memory)
        instruction[16],  // current instruction
        reset;            // reset signal
    OUT outM[16],         // M value output (to memory)
        writeM,           // write M? (to memory)
        addressM[15],     // address (of memory)
        pc[15];           // program counter

    PARTS:
    // Decode type of instruction
    Not(in=instruction[15], out=isAInstruction);   // 0 = A-instruction, 1 = C-instruction

    // ALU input selection (a bit of C-instruction)
    Mux16(a=aOut, b=inM, sel=instruction[12], out=aluY);

    // ALU
    ALU(x=dOut, y=aluY,
        zx=instruction[11], nx=instruction[10],
        zy=instruction[9],  ny=instruction[8],
        f=instruction[7],   no=instruction[6],
        out=aluOut, zr=zr, ng=ng);

    // ----- Registers -----

    // A register input: if A-instruction → instruction[0..14]; if C-instruction → ALU output
    Mux16(a=instruction, b=aluOut, sel=instruction[15], out=aIn);

    // Load A if: A-instruction OR (C-instruction with dest[2] = 1)
    Or(a=isAInstruction, b=instruction[5], out=loadA);
    Register(in=aIn, load=loadA, out=aOut);

    // D register (C-instruction with dest[1] = 1)
    And(a=instruction[15], b=instruction[4], out=loadD);
    Register(in=aluOut, load=loadD, out=dOut);

    // ----- Memory interface -----

    // OutM = ALU output
    Assign(outM = aluOut);

    // AddressM = A register
    Assign(addressM = aOut[0..14]);

    // WriteM = C-instruction with dest[0] = 1
    And(a=instruction[15], b=instruction[3], out=writeM);

    // ----- Program Counter -----

    // Jump condition evaluation
    Not(in=zr, out=notZr);
    Not(in=ng, out=notNg);

    // Compute >0, ==0, <0
    And(a=notNg, b=notZr, out=pos);  // >0
    And(a=zr, b=true, out=zero);     // ==0
    And(a=ng, b=true, out=neg);      // <0

    // Instruction[2:0] = jump bits (JGT, JEQ, JLT)
    And(a=instruction[2], b=pos,  out=jgt);
    And(a=instruction[1], b=zero, out=jeq);
    And(a=instruction[0], b=neg,  out=jlt);

    Or(a=jgt, b=jeq, out=tmp1);
    Or(a=tmp1, b=jlt, out=jump);

    // Only allow jump if it’s a C-instruction
    And(a=instruction[15], b=jump, out=pcLoad);

    // Program Counter
    PC(in=aOut, load=pcLoad, inc=true, reset=reset, out=pc);
}


 ```
