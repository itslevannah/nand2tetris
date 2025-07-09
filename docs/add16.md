---
layout: default
title: Add16
nav_order : 19
---

# Add16 Chip

### 1. Add16 Chip

16-bit Adder chip is used to add two 16-bit numbers.

    Performs 16-bit binary addition of two inputs: a[16] and b[16].

    Outputs a 16-bit sum (out[16]) and discards the final carry (no 17th bit).

    Built using a chain of 1 Half Adder (for LSB) + 15 Full Adders for ripple-carry addition.

<img src="/nand2tetris/images/16add.png" width="500" height="200px"/> 

### 2. Truth Table

| a (16-bit)          | b (16-bit)          | out (16-bit)       | Notes                     |
|---------------------|---------------------|--------------------|---------------------------|
| `0000000000000000`  | `0000000000000000`  | `0000000000000000` | 0 + 0 = 0                 |
| `0000000000000000`  | `0000000000000001`  | `0000000000000001` | 0 + 1 = 1                 |
| `0000000000000001`  | `0000000000000001`  | `0000000000000010` | 1 + 1 = 2                 |
| `0111111111111111`  | `0000000000000001`  | `1000000000000000` | 32767 + 1 = -32768 (overflow) |
| `1111111111111111`  | `0000000000000001`  | `0000000000000000` | -1 + 1 = 0 (wraparound)   |
| `1010101010101010`  | `0101010101010101`  | `1111111111111111` | 0xAAAA + 0x5555 = 0xFFFF  |

### 3. Implementation (Logisim)

Representation of the Add16 Chip in the logisim software using the previous gates.
Built by cascading:

    1 Half Adder (for the least significant bit, a[0] + b[0]).

    15 Full Adders (for bits a[1..15] + b[1..15] + carry)

<img src="/nand2tetris/logisim/add16.png" width="500" height="200px"/> 


### 4. Implementation (HDL)

The function in the above abstraction can help in the implementation of 16-bit Adder Chip.

You can use the Half Adder and Full Adder Chips you've built earlier.

(Representation of the Add16 Chip in HDL using previous gates.)


```hdl
CHIP Add16 {
    IN  a[16], b[16];
    OUT out[16];

    PARTS:
    // LSB: Half Adder (no carry-in)
    HalfAdder(a=a[0], b=b[0], sum=out[0], carry=c1);
    
    // Bits 1-15: Full Adders (propagate carry)
    FullAdder(a=a[1], b=b[1], c=c1, sum=out[1], carry=c2);
    FullAdder(a=a[2], b=b[2], c=c2, sum=out[2], carry=c3);
    FullAdder(a=a[3], b=b[3], c=c3, sum=out[3], carry=c4);
    FullAdder(a=a[4], b=b[4], c=c4, sum=out[4], carry=c5);
    FullAdder(a=a[5], b=b[5], c=c5, sum=out[5], carry=c6);
    FullAdder(a=a[6], b=b[6], c=c6, sum=out[6], carry=c7);
    FullAdder(a=a[7], b=b[7], c=c7, sum=out[7], carry=c8);
    FullAdder(a=a[8], b=b[8], c=c8, sum=out[8], carry=c9);
    FullAdder(a=a[9], b=b[9], c=c9, sum=out[9], carry=c10);
    FullAdder(a=a[10], b=b[10], c=c10, sum=out[10], carry=c11);
    FullAdder(a=a[11], b=b[11], c=c11, sum=out[11], carry=c12);
    FullAdder(a=a[12], b=b[12], c=c12, sum=out[12], carry=c13);
    FullAdder(a=a[13], b=b[13], c=c13, sum=out[13], carry=c14);
    FullAdder(a=a[14], b=b[14], c=c14, sum=out[14], carry=c15);
    FullAdder(a=a[15], b=b[15], c=c15, sum=out[15], carry=c16); // Discarded
}
 ```