---
layout: default
title: Inc16
nav_order : 20
---

# Inc16 Chip

### 1. Inc16 Chip

16-bit Incrementer chip is a special kind of Adder, used to increment a 16-bit input by 1.

<img src="/nand2tetris/images/inc16.png" width="500" height="200px"/> 

### 2. Truth Table


| Input (16-bit)          | Output (16-bit)         | Overflow |
|-------------------------|-------------------------|----------|
| `0000000000000000` (0)  | `0000000000000001` (1)  | `0`      |
| `0000000000000001` (1)  | `0000000000000010` (2)  | `0`      |
| `0000000000000010` (2)  | `0000000000000011` (3)  | `0`      |
| `0111111111111111` (32767) | `1000000000000000` (32768) | `0` |
| `1111111111111110` (65534) | `1111111111111111` (65535) | `0` |
| `1111111111111111` (65535) | `0000000000000000` (0)   | `1`      |



### 3. Implementation (HDL)

The function in the above abstraction can help in the implementation of 16-bit Incrementer Chip.

You can use the Add16 Chip you've built earlier.

Remember that 1 in 4-bit binary (say) is 0001.

(Representation of the Inc16 Chip in HDL using previous gates.)


```hdl
CHIP Inc16 {
    IN in[16];
    OUT out[16];

    PARTS:
   Add16(a=in, b[0]=true , b[1..15]=false, out=out);
}
 ```