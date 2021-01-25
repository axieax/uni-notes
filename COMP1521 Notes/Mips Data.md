# MIPS data


## MIPS Load/Store Instructions

Work in bytes (8 bits) 

- 1 byte (8-bit) - loaded/stored using lb/sb
- 2 bytes (16-bit) - half-word - loaded/stored using lh/sh
- 4 bytes (32-bit) - word - loaded/stored using lw/sw

sb/sh: low (least significant bits) of source register are used

lb/lh: assumes byte/halfword contains a 8-bit/16-bit signed integer (high 24/16-bits of destination register set to 1 if 8-bit/16-bit integer negative)

lbu/lhu: assumes integer is unsigned (high 24/16-bits of destination register always set to 0)

<img src="/Users/axie/Desktop/UNSW/Year 1/Term 3/COMP1521/Notes/images/image-20201018172722714.png" alt="image-20201018172722714" style="zoom:67%;" />

I offset:

```assembly
.text
main:
	li 	 $t0, 1		          # i = 1 in $t0
	mul  $t1, $t0, 4        # $t1: 4 * i (each element is 4 bytes across)
	sw   $v0, numbers($t1)	# access numbers[i], whose address is given by &numbers[0] (label numbers) + 4 * i
# ($reg) dereferences $reg by using the value at $reg instead of the address of $reg itself

.data
numbers: .word 0, 0, 0, 0, 0
```

## Assembler Directives (instructions to assembler)

```assembly
.text  # following instructions placed in text
.data  # following objects placed in data
.globl # make symbol available globally

.space 18     # int8_t a[18];    <-- uninitialized 18 bytes
.align 2      # align next object on 4-byte addr (2 to the power of 2)
.word 2       # int32_t i = 2;
.word 1,3,5   # int32_t v[3] = {1,3,5};
.half 2,4,6   # int16_t h[3] = {2,4,6};
.byte 7:5     # int8_t b[5] = {7,7,7,7,7};
.float 3.14   # float f = 3.14;
.asciiz "abc" # char s[4] {'a','b','c','\0'};     <-- always use .asciiz instead of .ascii
.ascii "abc"  # char s[3] {'a','b','c'};
```

e.g. `int x[10];` --> `x: .space 40` (10 * sizeof(int) in bytes)

Endian - order bits are stored

endian.s or endian.c : store 0x03040506 and print first byte (8 bits) at address stored

Big endian if first byte is 3 (stored in order), or little-endian if first byte is 6 (reversed order stored)

## SPIM memory layout

| Region | Address    | Notes                                                  |
| ------ | ---------- | ------------------------------------------------------ |
| text   | 0x00400000 | instructions only; read-only; cannot expand            |
| data   | 0x10000000 | data objects; read/write; can be expanded              |
| stack  | 0x7fffefff | grows down from that address; read/write               |
| k_text | 0x80000000 | kernal code; read-only; only accessible in kernel mode |
| k_data | 0x90000000 | kernal data; only accessible in kernel mode            |

Pointer arithmetic:

- C: increment by 1 is fine if pointer type defined, e.g. int * for int array
- MIPS: increment by size of int (4 bytes) for int array

Unalign (depends on architecture):

Address has to be divisible by type (e.g. 4 byte type: address has to be divisible by 4, i.e. last two bits 0)

```c
uint8_t bytes[32];
uint32_t *i = (uint32_t *) &bytes[12];
*i = 0x03040506;
printf("%d\n", bytes[12]); // 6

// Doesn't work for dcc: but fine for gcc (but slower)
uint8_t bytes[32];
uint32_t *i = (uint32_t *) &bytes[13];
*i = 0x03040506; // Misaligned address
printf("%d\n", bytes[13]);
```

SPIM:

```assembly
.data
# Unaligned address for x
bad: .space 1
x:   .space 4
# Align 1
bad: .space 1
		 .space 3 	# padding
x:   .space 4
# Align 2 (optimal)
bad: .space 1
		 .align 2 	# padding - next bit of memory has to be aligned (boundary of 2 ^ 2)
x:   .space 4
```

SPIM: .space not automatically aligned, but .half, .word automatically aligned

## Data structures and MIPS

- Char (1 byte)
- Int (4 bytes)
- Double (8 bytes)
- Array (sequence of bytes in memory) - accessed by index (calculated on MIPS)
- Struct (sequence of bytes in memory) - accessed by fields (constant offsets on MIPS)



