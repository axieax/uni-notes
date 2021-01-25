# Mips Basics

Register - place that can store a single value

A typical modern CPU has:

- a set of data registers (usually 32 bit)
- a set of control registers (incl PC - program counter - a CPU register which tracks execution *- some instructions modify pc (branches and jumps)*)
- an arithmetic-logic unit (ALU)
- access to memory (RAM)
- a set of simple instructions
  - transfer data between memory and registers
  - push values through the ALU to compute results
  - make tests and transfer control of execution

Executing an instruction (4 bytes long) involves:

- determine what the operator is
- which registers, if any, are involved
- determine which memory location, if any, is involved
- carry out the operation with the relevant operands
- store result, if any, in appropriate register

Classes of instructions:

- load and store (transfer data between registers and memory)
- computational (perform arithmetic/logical operations)
- jump and branch (transfer control of program execution)
- coprocessor (standard interface to various co-processors)
- special (miscellaneous tasks, e.g. syscall)

MIPS instructions are 32-bits long, and specify an operation (e.g. load, store, add, branch) and one or more operands (e.g. registers, memory addresses, constants). Possible instruction formats:

OPCODE (6 bits) R1 (5 bits) R2 (5 bits) R3 (5 bits) Unused (11 bits)

OPCODE (6 bits) R1 (5 bits) Memory address or Constant value (21 bits)

Assembly language - write instructions using names rather than bit string, refer to registers using either numbers or names, allow names (labels) to be associated with memory addresses

MIPS CPU has:

- 32 general purpose registers (32-bit)
- 16/32 floating-point registers (for float/double)
- PC - 32-bit register (always aligned on 4-byte boundary)
- HI, LO - for storing resutls of multiplication and division

## Integer Registers

| Number   | Names        | Conventional Usage                                 |
| -------- | ------------ | -------------------------------------------------- |
| 0        | $zero        | Constant 0                                         |
| *1*      | *$at*        | *Reserved for assembler*                           |
| 2, 3     | \$v0, \$v1   | Expression evaluation and results of a function    |
| 4 .. 7   | \$a0 .. \$a3 | Arguments 1-4                                      |
| 8 .. 16  | \$t0 .. \$t7 | Temporary (not preserved across function calls)    |
| 16 .. 23 | \$s0 .. $s7  | Saved temporary (preserved across function calls)  |
| *24, 25* | *\$t8, \$t9* | *Temporary (preserved across function calls)*      |
| *26, 27* | *\$k0, \$k1* | *Reserved for OS kernel*                           |
| 28       | $gp          | Pointer to global area                             |
| 29       | $sp          | Stack pointer                                      |
| 30       | $fp          | Frame pointer                                      |
| 31       | $ra          | Return address (used by function call instruction) |

add \$6, \$7, \$8 # Reg[6] <- Reg[7] + Reg[8]

li R<sub>d</sub>, imm # Load immediate Reg[R<sub>d</sub>] <- imm

- embed content in bitstring

la R<sub>d</sub>, add # Load address Reg[R<sub>d</sub>] <- addr (usually a label)

- memory address fixed before program run
- if vec is the label for memory address 0x10000100 then these two instructions are equivalent:
  - la	$7, vec
  - li     $7, 0x10000100

Neither pseudo-instructions la or li access memory, unlike lw

li	\$7, 15 translated to addi	\$7, \$0, 15; for large constants, translate li/la to two instructions

move R<sub>d</sub>, R<sub>s</sub> # Move data reg-to-reg Reg[R<sub>d</sub>] <- Reg[R<sub>s</sub>] (destination first)

Integer arithmetiic instructions (all arithmetic is signed - 2's complement):

- add R<sub>d</sub>, R<sub>s</sub>, R<sub>t</sub>	# Reg[R<sub>d</sub>] <- Reg[R<sub>s</sub>] + Reg[R<sub>t</sub>]
- addi R<sub>d</sub>, R<sub>s</sub>, imm	# Reg[R<sub>d</sub>] <- Reg[R<sub>s</sub>] + imm (immediate/constant)
- sub R<sub>d</sub>, R<sub>s</sub>, R<sub>t</sub>	# Reg[R<sub>d</sub>] <- Reg[R<sub>s</sub>] - Reg[R<sub>t</sub>]
- mul R<sub>d</sub>, R<sub>s</sub>, R<sub>t</sub>	# Reg[R<sub>d</sub>] <- Reg[R<sub>s</sub>] * Reg[R<sub>t</sub>]
- div R<sub>d</sub>, R<sub>s</sub>, R<sub>t</sub>	# Reg[R<sub>d</sub>] <- Reg[R<sub>s</sub>] / Reg[R<sub>t</sub>]
- rem R<sub>d</sub>, R<sub>s</sub>, R<sub>t</sub>	# Reg[R<sub>d</sub>] <- Reg[R<sub>s</sub>] % Reg[R<sub>t</sub>]
- neg R<sub>d</sub>, R<sub>s</sub>	# Reg[R<sub>d</sub>] <- - Reg[R<sub>s</sub>]

instruction + i: immediate (spim allows second operand r<sub>t</sub> to be replaced by a constant and will generate appropriate real MIPS instruction(s))

instruction + u: do not stop execution on overflow

Logic instructions:

- and R<sub>d</sub>, R<sub>s</sub>, R<sub>t</sub>	# Reg[R<sub>d</sub>] <- Reg[R<sub>s</sub>] & Reg[R<sub>t</sub>]
- andi R<sub>d</sub>, R<sub>s</sub>, imm	# Reg[R<sub>d</sub>] <- Reg[R<sub>s</sub>] & imm
- or R<sub>d</sub>, R<sub>s</sub>, R<sub>t</sub>	# Reg[R<sub>d</sub>] <- Reg[R<sub>s</sub>] | Reg[R<sub>t</sub>]
  - ori (immediate)
- not R<sub>d</sub>, R<sub>s</sub>	# Reg[R<sub>d</sub>] <- Reg[R<sub>s</sub>]
- xor R<sub>d</sub>, R<sub>s</sub>, R<sub>t</sub>	# Reg[R<sub>d</sub>] <- Reg[R<sub>s</sub>] ^ Reg[R<sub>t</sub>]
  - xori (immediate)

Bit manipulation instructions:

- sll R<sub>d</sub>, R<sub>s</sub>, R<sub>t</sub>	# Shift left logical Reg[R<sub>d</sub>] <- Reg[R<sub>s</sub>] << Reg[R<sub>t</sub>]
- sll R<sub>d</sub>, R<sub>s</sub>, imm	# Shift left logical Reg[R<sub>d</sub>] <- Reg[R<sub>s</sub>] << imm
- srl R<sub>d</sub>, R<sub>s</sub>, imm	# Shift right logical Reg[R<sub>d</sub>] <- Reg[R<sub>s</sub>] >> imm
- sra R<sub>d</sub>, R<sub>s</sub>, imm	# Shift right arithmetic Reg[R<sub>d</sub>] <- Reg[R<sub>s</sub>] >> imm
- rol R<sub>d</sub>, R<sub>s</sub>, imm	# Rotate left Reg[R<sub>d</sub>] <- rot(Reg[R<sub>s</sub>] imm left)
- ror R<sub>d</sub>, R<sub>s</sub>, imm	# Rotate left Reg[R<sub>d</sub>] <- rot(Reg[R<sub>s</sub>] imm left)

Jump instructions (control flow of program execution):

- j label	# Jump to location
- jal label	# Jump and link
- jr R<sub>s</sub>	# Jump via register
- jalr R<sub>s</sub>	# Jump and link via reg

Branch instructions:

- beq R<sub>s</sub>, R<sub>t</sub>, label	# Branch on equal - if (Reg[R<sub>s</sub>] == Reg[R<sub>t</sub>]) PC <- label
- bne R<sub>s</sub>, R<sub>t</sub>, label	# Branch on not equal - if (Reg[R<sub>s</sub>] != Reg[R<sub>t</sub>]) PC <- label
- blt R<sub>s</sub>, R<sub>t</sub>, label	# Branch on less than - if (Reg[R<sub>s</sub>] < Reg[R<sub>t</sub>]) PC <- label
- ble R<sub>s</sub>, R<sub>t</sub>, label	# Branch on less or equal - if (Reg[R<sub>s</sub>] <= Reg[R<sub>t</sub>]) PC <- label
- bgt R<sub>s</sub>, R<sub>t</sub>, label	# Branch on equal - if (Reg[R<sub>s</sub>] > Reg[R<sub>t</sub>]) PC <- label
- bge R<sub>s</sub>, R<sub>t</sub>, label	# Branch on equal - if (Reg[R<sub>s</sub>] >= Reg[R<sub>t</sub>]) PC <- label

Pseudo instructions:

- li \$t5, const --> ori \$t5, \$0, const (or with zero)
- la \$t3, label (where label is very big) --> lui \$at, label[32..16] ->  ori \$t3, \$at, label[15..0]
  - using reserved register $at (1), 
- bge \$t1, \$t2, label --> slt \$at, \$t1, \$t2 -> beq \$at, \$0, label
- blt \$t1, \$t2, label --> slt \$at, \$t1, \$t2 -> bne \$at, \$0, label

System calls (syscall):

| Service       | n    | Arguments                              | Result         |
| ------------- | ---- | -------------------------------------- | -------------- |
| printf("%d")  | 1    | int in $a0                             | -              |
| printf("%f")  | 2    | float in $f12                          | -              |
| printf("%lf") | 3    | double in $f12                         | -              |
| printf("%s")  | 4    | $a0 = string                           | -              |
| scanf("%d")   | 5    | -                                      | int in $v0     |
| scanf("%f")   | 6    | -                                      | float in $f0   |
| scanf("%lf")  | 7    | -                                      | double in $f0  |
| fgets         | 8    | buffer address in \$a0, length in \$a1 | -              |
| sbrk (malloc) | 9    | nbytes in $a0                          | address in $v0 |
| printf("%c")  | 11   | char in $a0                            | -              |
| scanf("%c")   | 12   | -                                      | char in $v0    |
| exit(status)  | 17   | status in $a0                          | -              |

## Integer arithmetic instructions

![image-20201006172326901](/Users/axie/Desktop/UNSW/Year 1/Term 3/COMP1521/Notes/images/image-20201006172326901.png)

- in 2's-complement (immediate is signed - add -1 to subtract 1)
- instruction + u: do not stop execution on overflow
- spim allows second operand r<sub>t</sub> to be replaced by a constant and will generate appropriate real MIPS instruction(s)

<img src="/Users/axie/Desktop/UNSW/Year 1/Term 3/COMP1521/Notes/images/image-20201006172647050.png" alt="image-20201006172647050" style="zoom:67%;" />

- mult of two 32-bit --> 64-bit (top 32 bits in hi, bottom 32 bits in lo - use mflo or mfhi to retrieve these values)
- pseudo-instruction rem r<sub>d</sub>, r<sub>s</sub>, r<sub>t</sub> translated to div r<sub>s</sub>, r<sub>t</sub> plus mfhi r<sub>d</sub>
- pseudo-instruction div r<sub>d</sub>, r<sub>s</sub>, r<sub>t</sub> translated to div r<sub>s</sub>, r<sub>t</sub> plus mflo r<sub>d</sub>
- divu and multu are unsigned equivalents of div and mult

## Bit manipulation instructions

![image-20201006172923638](/Users/axie/Desktop/UNSW/Year 1/Term 3/COMP1521/Notes/images/image-20201006172923638.png)

not r<sub>d</sub>, r<sub>s</sub> --> nor r<sub>d</sub>, r<sub>s</sub>, $0

## Shift instructions

![image-20201006173256902](/Users/axie/Desktop/UNSW/Year 1/Term 3/COMP1521/Notes/images/image-20201006173256902.png)

- srl and srlv shift zeros into most-significant bit (shift 0 into the top bit as you shift right)
  - this matches shift in C of unsigned value
- sra and srav propagate most-significant bit (if top bit is 1, shift 1 into the top bit as you shift right)
  - this eansures shifting a negative number divides by 2
- spim provides rol and ror pseudo-instrucitons which rotate bits

## Jump instructions

<img src="/Users/axie/Desktop/UNSW/Year 1/Term 3/COMP1521/Notes/images/image-20201006173540026.png" alt="image-20201006173540026" style="zoom:80%;" />

- jump instruction unconditionally transfers execution to a new location
- assembler will calculate correct value for X from location of label in code
- jal & jalr set $r_{31}$ ($ra) to address of the next instruction
  - used for function calls
  - return can then be implemented with jr $ra

## Branch instructions

![image-20201006173724758](/Users/axie/Desktop/UNSW/Year 1/Term 3/COMP1521/Notes/images/image-20201006173724758.png)

- branch instruction conditionally transfers execution to a new location
- shift by 2: I (number of instructions we want to jump, where each instruction is 4 bytes long; pc contains address of currently executing instruction)
- assembler will calculate correct value for I from location of label in code
- spim allows second operand r<sub>t</sub> to be replaced by a constant and will generate appropriate real MIPS instruction(s)

## Miscellaneous instructions

![image-20201006173936929](/Users/axie/Desktop/UNSW/Year 1/Term 3/COMP1521/Notes/images/image-20201006173936929.png)

lui helps get upper part of 32-bit value

Example translations:

| Pseudo-instructions   | Real instructions                                            |
| --------------------- | ------------------------------------------------------------ |
| move \$a1, \$v0       | addu \$a1, \$0, \$v0                                         |
| li \$t5, 42           | ori \$t5, \$0, 42                                            |
| li $s1, 0xdeadbeef    | lui \$at, 0xdead<br />ori \$s1, \$at, 0xbeef<br />*can't use s1 for all registers - atomic operation* (exception) |
| la $t3, label         | lui \$at, label[31..16]<br />ori \$t3, \$at, label[15..0]    |
| bge \$t1, \$t2, label | slt \$at, \$t1, \$t2<br />beq \$at, \$0, label<br />*(a < b) == 0 OR not (a < b)* |
| blt \$t1, \$t2, label | slt \$at, \$t1, \$t2<br />bne \$at, \$0, label<br />*(a < b) != 0 OR (a < b)* |

## Key system calls

| Service      | $v0  | Arguments                              | Returns     |
| ------------ | ---- | -------------------------------------- | ----------- |
| printf("%d") | 1    | int in $a0                             | -           |
| printf("%s") | 4    | string in $a0                          | -           |
| scanf("%d")  | 5    | -                                      | int in $v0  |
| fgets        | 8    | buffer address in \$a0, length in \$a1 | -           |
| exit(0)      | 10   | status in $a0                          | -           |
| printf("%c") | 11   | char in $a0                            | -           |
| scanf("%c")  | 12   | -                                      | char in $v0 |



C signed overflow - undefined

C unsigned overflow wraps around

MIPS language:

- \# comments
- : labels
- . directives
- assembly language instructions

Specify:

- data objects that live in the data region
- functions (instruction sequences) that live in the code/text region

Each instruction or directive appears on its own line