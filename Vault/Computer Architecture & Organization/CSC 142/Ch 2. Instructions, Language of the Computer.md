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



