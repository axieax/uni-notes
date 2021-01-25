# Integer types

*Note: common sizes stated below - doesn't apply on all hardware*

| Type               | Size (bytes or 8 bits) | Min                        | Max                        |
| ------------------ | ---------------------- | -------------------------- | -------------------------- |
| char               | 1                      | -128                       | 127                        |
| signed char        | 1                      | -128                       | 127                        |
| unsigned char      | 1                      | 0                          | 255                        |
| short              | 2                      | -32,768                    | 32,767                     |
| unsigned short     | 2                      | 0                          | 65,535                     |
| int                | 4                      | -2,147,483,648             | 2,147,483,647              |
| unsigned int       | 4                      | 0                          | 4,294,967,295              |
| long               | 8                      | -9,223,372,036,854,775,808 | 9,223,372,036,854,775,807  |
| unsigned long      | 8                      | 0                          | 18,446,744,073,709,551,615 |
| long long          | 8                      | -9,223,372,036,854,775,808 | 9,223,372,036,854,775,807  |
| unsigned long long | 8                      | 0                          | 18,446,744,073,709,551,615 |

Range of 32 bit int:

​	unsigned (>= 0): 0 to $2^{32}$

​	signed: $\frac{-2^{32}}{2}$ to $\frac{2^{32}}{2}$ ==leftmost digit used to represent sign==

Also, unsigned %u.

Common bug: 

```c	
int c;
while ((c = getchar()) != EOF) {
  putchar(c);
}
```

getchar() variable should be `int` type, not `char`. This also applies for `getc` and `fgetc`. 

> #include <limits.h>

#defines INT_MIN, INT_MAX etc.

> #include <stdint.h>

| Type     | Min                        | Max                        |
| -------- | -------------------------- | -------------------------- |
| int8_t   | -128                       | 127                        |
| uint8_t  | 0                          | 255                        |
| int16_t  | -32,768                    | 32,767                     |
| uint16_t | 0                          | 65,535                     |
| int32_t  | -2,147,483,648             | 2,147,483,647              |
| uint32_t | 0                          | 4,294,967,295              |
| int64_t  | -9,223,372,036,854,775,808 | 9,223,372,036,854,775,807  |
| uint64_t | 0                          | 18,446,744,073,709,551,615 |

## Sizeof

When sizeof's operand is a type, it has to be enclosed in parentheses. But when sizeof's operand is a variable, this is not required.

e.g. `sizeof var` and `sizeof (type)`

\# bits of a variable = 8 * sizeof x

## Integer representation

Each digit represented by bits (starting at 2<sup>0</sup> on the RHS)

- Decimal (base/radix = 10): 0, 1, 2, 3, 4, 5, 6, 7, 8, 9
- Binary (base/radix =  2 = 2<sup>1</sup>): 0, 1
  - 1 bit representation: *0b01001000111110101011110010010111*
- Hexadecimal (base/radix = 16 = 2<sup>4</sup>): 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, F
  - 4 bit representation: *0100 1000 1111 1010 1011 1100 1001 0111 or 0x48FABC97*
  - Prefix: 0x
  - C: %x
- Octal (base/radix = 8 = 2<sup>3</sup>): 0, 1, 2, 3, 4, 5, 6, 7
  - 3 bit representation: *01 001 000 111 110 101 011 110 010 010 111 or 0 11076536227*
  - Prefix: 0
  - C: %o

e.g. 170 ($10 \times 2^4 + 10 \times 2 ^ 0$) = 0x**A**<u>A</u> = **1010** <u>1010</u>

## Bitwise operations

Everything is ultimately a string of bits. 

- `&` logical AND on each corresponding pair of bits (only 1 if both 1), e.g. for checking whether a bit is set
  - bit_1 & bit_2
  - e.g. for checking odd numbers - `n % 2 == 1` or `n & 1`
- `|` logical OR on each corresponding pair of bits, e.g. ensuring that a bit is set
  - bit_1 | bit_2
- `~` NEGATION flips each bit, e.g. creating useful bit patterns
  - ~ bit_1
- `^` XOR only 1 if both bits different (one 0 one 1), e.g. for generating hashes, graphic operation, cryptography
  - bit_1 ^ bit_2
  - x ^ y ^ y == x
- `<<` Left Shift - moves/shifts each bit `n` positions to the left - left-end bit vanishes, right-end bit replaced by zero
  - bit_1 << n *(n is a small positive integer)*
  - $x << n = 2^n x$
    - e.g. $x << 3 = 2^3 \times x = 8x$
  - **Don't left shift negative values** - use unsigned int
  - `uint64_t z = 1 << 31` won't work because 1 is int (32 bits)
  - Type cast `((uint64_t) 1)` instead of `1` allows for 1 << 54
  - Bit string: want `n` number of 1's at the end: 2<sup>n</sup> - 1. 1's at the start: invert ~
- `>>` Right Shift - moves/shifts each bit `n` positions to the right - right-end bit vanishes, left-end bit replaced by zero
  - **Note: shifts involving negative values are not portable (implementation defined) - use unsigned values to be safe/portable**
  - bit_1 >> n *(n is a small positive integer)*

## [Two's complement](https://www.cs.cornell.edu/~tomf/notes/cps104/twoscomp.html): 

To get two's complement negative notation of an integer - write number in binary, invert the digits (~) and add one to the result (works both ways). This works because the negative of a number is just it subtract from 0 --> method of subtraction and "borrowing" from the digit before. 

e.g. The negative of 5 (0000 0101) is -5 (1111 1011) = -256 + (128 + 64 + 32 + 16 + 8 + 2 + 1)

A leading 1 means the number is negative. 

e.g. The negative of 0xFF is 0x01 (same method). Thus 0xFF is -1 (signed) or 255 (unsigned).

e.g. ~(255 or 16<sup>2</sup>) = ~0xFF = ~(1111 1111) = 0000 0000 = 0

With two's complement, you can do addition and subtraction by adding. 

**Ensure type is correct, e.g. default int (32 - goes to 64 if not enough): 0xFF gets interpreted as 0x0000FF if 8 bit type not specified (e.g. int8_t) **

For an n-bit binary number, the representation of -b is 2<sup>n</sup> - b

e.g. for an 8-bit string:-n = 2<sup>8</sup> - n

- -1
  - 1 = 0000 0001
  - -1 = 2<sup>8</sup> - 1 = 1 0000 0000 - 0000 0001 = 1111 1111

![image-20201002131601789](/Users/axie/Desktop/UNSW/Year 1/Term 3/COMP1521/Notes/images/image-20201002131601789.png)

==Flip the bits, Plus one.==

16 bit 0x8000 -> you get 0x8000 using two's complement method - no opposite positive --> -128

## Overflow:

`for (int8_t i = -128; i <= 127; i++)` may cause an infinite loop because 127 + 1 = 128 --> -128 or undefined

1u << 33 for unsigned

1L * 1000 * 1000 for long (prevent overflow)