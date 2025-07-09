---
layout: default
title: Full Adder Chip
nav_order : 18
---

# Full Adder Chip

### 1. Full Adder Chip

Full Adder chip is used to add 3-bits.

<img src="\images\fulladder.avif" width="500" height="200px"/> 

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

Representation of the Full Adder Chip in the logisim software using the previous gates.

<img src="\logisim\fulladder.png" width="500" height="200px"/> 


### 4. Implementation (HDL)

The function in the above abstraction can help in the implementation of Full Adder Chip.
You can use the Half Adder Chip you've built earlier.

sum = a XOR b XOR c

carry = (a AND b) OR (b AND c) OR (c AND a)

(Representation of the Full Adder Chip in HDL using previous gates.)


```hdl
CHIP FullAdder {
    IN a, b, c;  // 1-bit inputs
    OUT sum,     // Right bit of a + b + c
        carry;   // Left bit of a + b + c

    PARTS:
    HalfAdder(a=a, b=b, sum=sumab, carry=carryab);
    HalfAdder(a=sumab, b=c, sum=sum, carry=temp);
    Or(a=temp, b=carryab, out=carry);
}
 ```