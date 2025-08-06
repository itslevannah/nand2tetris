---
layout: default
title: Half Adder Chip
nav_order : 17
---
# Half Adder Chip

### 1. Half Adder Chip

The chip used to add two n-bit numbers is known as Adder, also known as n-bit Adder.
Half Adder chip is used to add 2-bits.

<img src="/nand2tetris/images/halfadder.avif" width="500" height="200px"/> 

### 2. Truth Table

```markdown
|  a  |  b  | sum | carry |
|-----|-----|-----|-------|
|  0  |  0  |  0  |   0   |
|  0  |  1  |  1  |   0   |
|  1  |  0  |  1  |   0   |
|  1  |  1  |  0  |   1   |
```

### 3. Implementation (Logisim)
Representation of the Half Adder Chip in the logisim software using the previous gates.

<img src="/nand2tetris/logisim/halfadder.png" width="500" height="200px"/> 


### 4. Implementation (HDL)

The function in the above abstraction can help in the implementation of Half Adder Chip:

sum = a XOR b

carry = a AND b

(Representation of the Half Adder Chip in HDL using previous gates.)


```hdl
CHIP HalfAdder {
    IN a, b;    // 1-bit inputs
    OUT sum,    // Right bit of a + b 
        carry;  // Left bit of a + b

    PARTS:
    Xor(a=a, b=b, out=sum);
    And(a=a, b=b, out=carry);
}
 ```

### 5. Video Tutorial
<iframe width="560" height="315" src="https://www.youtube.com/embed/DQIeT6HVnxk?si=-u7I1BBSfHv6Wd5L" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>