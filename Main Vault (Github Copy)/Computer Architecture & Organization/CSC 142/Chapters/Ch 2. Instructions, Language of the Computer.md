![[Screenshot 2026-02-07 at 7.12.30 PM.png]]

---
# 2.2 Operations of the Computer Hardware 
*Every Computer must be able to perform arithmetic*

The MIPS assembly language notation
`add a, b,c `
tells the computer to add two variables, `b`, and `c` and put their sum into `a`.  Each line can contain **AT MOST one instruction.**

#### Compiling Two C Assignments Statements into MIPS
Translate this ***Java*** code into MIPS assembly
```java
a = b + c;
d = a - e;
```
Here is the MIPS equivalent of the above
```assembly
add a, b, c
sub d, a, e
```

What about this complex statement in ***Java***?
```Java
f = (g + h) - (i + j);
```
Here is the MIPS equivalent of the above
```Assembly
add t0, g, h
add t1, i, j
sub f, t0, t1
```

---
# 2.3 Operands of the Computer Hardware
*Operands are restricted to registers in the hardware. Registers are primitives.*

> [!DANGER] The size of a register in MIPS is ***32 bits***. They are given the name ***Word***.
> ***Words*** are a natural unit of access in the computer. There are a limit of 32 registers, so there are 32 32-bit registers.
> The reason for a limit of 32 registers is that a large number of registers may increase the clock cycle time because it takes electronic signals longer when they travel further.

MIPS uses two-character names to represent these registers
- `$s0 $s1 ....` are used for registers that correspond to variables in C and Java programs
- `$t0 $t1 ....` are used for temp registers needed to compile the program into MIPS instructions.

It is the compilers job to associate program variables with registers. For example, the earlier statement
```java
f = (g + h) - (i + j);
```
will more accurately be represented as such
```Assembly
add $t0, $s1, $s2    # register $t0 contains g + h
add $t1, $s3, $s4    # register $t1 contains i + j
sub $s0, $t0, $t1    # f gets $t0 - $t1, which is (g + h) - (i + j)
```
 
#### Memory Operands
*Higher level programming languages can have data structures that far exceed the size that we can store in register. Arithmetic operations ONLY occur in these registers. We must be able to transfer data between main memory and registers. This is called a ***Load*** *operation*.

Imagine we wanted to convert this C++ code into MIPS
```cpp
A[12] = h + A[8];
```

This is the MIPS equivalent
```MIPS
lw $t0, 32($s3)    #Temp reg $t0 gets A[8]
add $t0, $s2, $t0  #Temp reg $t0 gets h + A[8]
```

> [!Danger] The reason we prepend ($s3) with 32 is because `load` and `stores` operate on `words`. Each `word` is 4 bytes or 32 bits. So if we want to get the 8th index from A we must use `4 x 8 = 32`

---
# 2.5 Representing Instructions in the Computer

Mapping register names to numbers

| Register Name | Register Number | Register Name | Register Number |
| ------------- | --------------- | ------------- | --------------- |
| $s0           | 16              | $t0           | 8               |
| $s1           | 17              | $t1           | 9               |
| $s2           | 18              | $t2           | 10              |
| $s3           | 19              | $t3           | 11              |
| $s4           | 20              | $t4           | 12              |
| $s5           | 21              | $t5           | 13              |
| $s6           | 22              | $t6           | 14              |
| $s7           | 23              | $t7           | 15              |

#### MIPS Fields

***R-Format***
![[Screenshot 2026-02-12 at 11.48.58 PM.png]]

| Field   | Definition                     | Size   |
| ------- | ------------------------------ | ------ |
| `op`    | opcode                         | 6 bits |
| `rs`    | first register source operand  | 5 bits |
| `rt`    | second register source operand | 5 bits |
| `rd`    | register destination operand   | 5 bits |
| `shamt` | shift amount                   | 5 bits |
| `funct` | function code                  | 6 bits |

***I-Format***
![[Screenshot 2026-02-12 at 11.52.59 PM.png]]

| Field           | Definition                     | Size    |
| --------------- | ------------------------------ | ------- |
| `op`            | opcode                         | 6 bits  |
| `rs`            | first register source operand  | 5 bits  |
| `rt`            | Second register source operand | 5 bits  |
| `const or addr` | Constant or Address            | 16 bits |

Since the constant or address is `16 bits` in size this means
- we can load any word within a region of 2 to the 15 power or 32,768 bytes.
- 8192 Words
- Of the address in the base register `rs`
- Constants limited to no larger than 32,768

---
# 2.6 Logical Operations

| Logical Operation | MIPS Instruction | Description                                                                                            |
| ----------------- | ---------------- | ------------------------------------------------------------------------------------------------------ |
| Shift left        | `sll`            | Moves all bits in a word to left                                                                       |
| Shift right       | `srl`            | Moves all bits in a word to right                                                                      |
| bit-by-bit AND    | `and` `andi`     | Compares each bit in a word and calculates a `1` only if a `1` is in both operands                     |
| bit-by-bit OR     | `or` `ori`       | Compares each bit in a word and calculates a `1` if a `1` is in either operand                         |
| bit-by-bit NOT    | `nor`            | Calculates the NOT of the OR with two operands. Calculates a `1` only if there is `0` in both operands |
#### `sll` example
```mips
sll $t2, $s0, 4
```
This shifts the bits in register `$s0` by 4 places and stores it in `$t2`.

> [!DANGER] Shifting left by `i` bits is the same as multiplying by `2^i`.

#### `and` example
Assume `$t2` contains `0000 0000 0000 0000 0000 1101 1100 0000`
Assume `$t1` contains `0000 0000 0000 0000 0011 1100 0000 0000`
```mips
and $t0, $t1, $t2
```
This ANDs the bits in `$t1` and `$t2` and stores it in `$t0`
The result would be `0000 0000 0000 0000 0000 1100 0000 0000`
#### `or` example
Assume `$t1` contains `0000 0000 0000 0000 0011 1100 0000 0000`
Assume `$t3` contains `0000 0000 0000 0000 0000 0000 0000 0000`
```mips
nor $t0, $t1, $t3
```
NORs the bits in `$t3` and `$t1` and stores it in `$t0`
The result would be `1111 1111 1111 1111 1100 0011 1111 1111`

#### Branch If Equal
```mips
beq register1, register2, L1
```
This branches to the statement labeled `L1` if the value in `register1` equals the value in `register2`.
#### Branch If Not Equal
```mips
bne register1, register2, L1
```
This branches to the statement labeled `L1` if the value in `register1` does NOT equal the value in `register2`

#### Example using BNE and BEQ
Assume this C code
```C
if (i==j) {
	f = g + h;
} else {
	f = g - h
}
```

MIPS Equivalent
```mips
bne $s3, $s4, Else
add $s0, $s1, $s2
Else: sub $s0, $s1, $s2
j Exit
Exit:
```
