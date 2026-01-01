---
layout: default
title: Module 4 - Number Systems
parent: Course Modules
nav_order: 5
permalink: /docs/modules/module-04/
---

# Module 4: Number Systems & Binary Representation
**Week 5**

---

## Overview

Deep dive into number systems, binary representations, and conversions critical for digital circuit design.

**Duration**: 1 week  
**Prerequisites**: Modules 0-3 completed

---

## Learning Objectives

By the end of this module, you will be able to:
1. Master binary, octal, decimal, and hexadecimal conversions
2. Understand signed number representations
3. Implement binary-to-BCD converters
4. Design magnitude comparators
5. Work with fixed-point representations

---

## Topics

### 1. Number System Fundamentals
- Binary (base-2): 0, 1
- Octal (base-8): 0-7
- Decimal (base-10): 0-9
- Hexadecimal (base-16): 0-9, A-F
- Conversion algorithms

### 2. Signed Number Representations

#### Sign-Magnitude
- MSB indicates sign (0=positive, 1=negative)
- Simple but has drawbacks
- Two representations of zero

#### 1's Complement
- Negative numbers: invert all bits
- End-around carry needed
- Still has two zeros

#### 2's Complement (Most Common)
- Negative numbers: invert bits + 1
- Range: $-2^{n-1}$ to $2^{n-1}-1$
- Only one zero
- Simplified arithmetic

### 3. BCD (Binary-Coded Decimal)
- Each decimal digit: 4 bits
- Easy decimal I/O
- Inefficient storage
- Special arithmetic rules

### 4. Fixed-Point Representation
- Fractional binary numbers
- Q-format notation
- Range vs precision tradeoffs

### 5. Magnitude Comparators
- Comparing binary numbers
- Cascading comparators
- Verilog implementation

---

## Assignment 4

**Due**: End of Week 5  
**Points**: 100

### Requirements

**Part 1**: Number Conversions (30 points)
Perform conversions:
- Decimal ↔ Binary ↔ Hex ↔ Octal
- Signed representations (all three methods)
- Fixed-point numbers
- Show all work

**Part 2**: 2's Complement Arithmetic (25 points)
- Addition and subtraction
- Overflow detection
- Range calculations
- Sign extension

**Part 3**: BCD Converter (25 points)
Design 8-bit binary to BCD converter:
- Create conversion algorithm
- Implement in Verilog
- Test with all possible inputs
- Synthesize and test

**Part 4**: Magnitude Comparator (20 points)
Design 8-bit comparator:
- Outputs: A>B, A=B, A<B
- Optimize for speed
- Implement and test

[Download Assignment Template](../assignments/assignment-04/)

---

## Resources

### Lecture Materials
- [Module 4 Slides](../../resources/lectures/module04_slides.pdf)

### Interactive Tools
- [Number Base Converter](https://www.rapidtables.com/convert/number/base-converter.html)
- [2's Complement Calculator](https://www.exploringbinary.com/twos-complement-converter/)
- [IEEE 754 Visualizer](https://www.h-schmidt.net/FloatConverter/IEEE754.html)

### Video Tutorials
- 2's Complement Explained (18 min)
- Binary to BCD Conversion (15 min)
- Fixed-Point Arithmetic (25 min)

---

## Key Formulas

### 2's Complement Range
For n-bit number:
- **Range**: $-2^{n-1}$ to $2^{n-1} - 1$
- **Example (8-bit)**: -128 to +127

### 2's Complement Conversion
**Positive to Negative**:
1. Invert all bits
2. Add 1

**Check**: Adding a number to its 2's complement gives 0

### BCD Encoding
Decimal digit → 4-bit BCD
```
0 → 0000    5 → 0101
1 → 0001    6 → 0110
2 → 0010    7 → 0111
3 → 0011    8 → 1000
4 → 0100    9 → 1001
```

### Overflow Detection (2's Complement)
**Addition**: Overflow if sign(A) = sign(B) ≠ sign(Sum)

**Subtraction**: Overflow if sign(A) ≠ sign(B) and sign(A) ≠ sign(Result)

---

## Design Examples

### 4-Bit Magnitude Comparator
```verilog
module comparator_4bit (
    input  [3:0] a, b,
    output       a_gt_b, a_eq_b, a_lt_b
);
    assign a_gt_b = (a > b);
    assign a_eq_b = (a == b);
    assign a_lt_b = (a < b);
endmodule
```

### Binary to BCD (Double-Dabble Algorithm)
```verilog
module bin2bcd (
    input  [7:0]  binary,
    output [11:0] bcd  // 3 BCD digits
);
    // Implementation uses shift-and-add-3 algorithm
    // See full code in assignment template
endmodule
```

---

## Common Mistakes

❌ **Sign extension errors**
- Must replicate sign bit when extending
- Example: 4-bit 1101 → 8-bit 11111101 (not 00001101)

❌ **Overflow confusion**
- Carry ≠ Overflow
- Carry is normal in unsigned arithmetic
- Overflow only matters for signed numbers

❌ **BCD vs Binary**
- BCD 10-15 are invalid codes
- Can't directly use binary arithmetic on BCD

✅ **Good Practice**
- Always specify signed vs unsigned
- Check for overflow in signed arithmetic
- Use systematic conversion procedures
- Verify edge cases (max, min, zero)

---

## Real-World Applications

### Where These Concepts Matter
- **2's Complement**: CPU arithmetic, DSP
- **BCD**: Digital clocks, calculators, displays
- **Fixed-Point**: Audio/video processing, embedded systems
- **Comparators**: Control logic, sorting, min/max finding

---

## Next Steps

After completing Module 4, proceed to:
- **[Module 5: Binary Arithmetic](module-05/)**
- Design adders and ALUs
- Multiplication and division

---

[← Previous Module](module-03/) | [Back to All Modules](../) | [Next Module →](module-05/)
