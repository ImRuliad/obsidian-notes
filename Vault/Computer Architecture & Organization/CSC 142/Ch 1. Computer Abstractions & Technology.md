
> [!Danger] The Seven Great Ideas in Computer Architecture
> - Use Abstraction to Simplify Design
> - Make the Common Case Fast
> - Performance via Parallelism
> - Performance via Pipelining
> - Performance via Prediction
> - Hierarchy of Memories
> - Dependability via Redundancy

---
#  Below Your Program 
*A typical application may consist of millions of lines of code and depend on many complex libraries, but hardware in a computer can only execute extremely simple low level instructions. To go from complex application software to simple instructions involves many layers that translate high level operations to low level simple instructions. This is **abstraction***

![[Screenshot 2026-01-30 at 5.34.54 PM.png]]
*System Software provides services to operating systems, compilers, loaders, assemblers*

Sitting between Application Software and Hardware is Systems Software, and there are two main types of Systems Software
- ***Operating System***, Interfaces between the user's program and hardware
	- Handles basic input and output operations
	- Allocates storage and memory
	- Provides protected sharing of the computer among multiple applications using it simultaneously
- ***Compiler***, A program that translates high-level language statements into assembly language statements.

---
# <u> From High-Level Language to the Language of Hardware </u>
*The first programmers communicated to computers in binary numbers. This was tedious so they created new notations that were closer to how humans think. They later invented programs to translate from this symbolic notation to binary. This was named an **assembler***

- ***Instruction*** - A command that computer hardware understands
- ***Assembler*** - A program that translates a symbolic version of instructions into the binary version
- ***Assembly Language*** - A symbolic representation of machine instructions.
![[Screenshot 2026-01-30 at 6.18.14 PM.png]]

---
# <u> Under the Covers </u>
*The five classic components of a computer are input, output, memory, datapath, and control. The last two are sometimes combined and called processor*
- The processor gets instructions and data from memory
- Input writes data to memory
- Output reads data from memory
- Control sends the signals that determine the operations of the datapath, memory, input, and output.

A ***Processor*** or ***CPU*** is comprised of two main components
- Datapath
- Control

***Datapath*** performs the arithmetic operations.
***Control*** tells the datapath, memory, and IO devices what to do according to the wishes of the instructions of the program

![[Screenshot 2026-01-30 at 6.33.03 PM.png]]![[Screenshot 2026-01-30 at 6.33.42 PM.png]]

---

# <u> Technologies for Building Processors and Memory </u>

***Volatile Memory*** - Storage such as DRAM that retains data only if it is receiving power.
***Nonvolatile Memory*** - A form of memory that retains data even in the absence of a power source and that is used to store programs between runs.

Volatile memory is also known as ***Primary Memory*** or ***Main Memory*** and Nonvolatile Memory is also known as ***Secondary Memory***

A ***Transistor*** is simply an on/off switch controlled by electricity. The ***Integrated Circuit (IC)*** combines dozens of hundreds of transistors into a single chip.
To describe the tremendous increase in the number of transistors per chip, the term ***Very Large Scale Integrated Circuit (VLSI)***

![[Screenshot 2026-01-31 at 9.05.59 PM.png]]

#### **The Manufacturing of ICs**
The process begins with a substance called ***silicon*** which does not conduct electricity well, thus it is called a ***semiconductor***.

With a special chemical process they can add materials to ***silicon*** that allow tiny areas to transform into one of three devices:
- Excellent conductors of electricity (using either microscopic copper or aluminum wire)
- Excellent insulators from electricity (like plastic sheathing or glass)
- Areas that can conduct or insulate under certain conditions (as a switch)

> [!DANGER] Transistors fall in the last category and thus a VLSI circuit is just billions of combinations of conductors, insulators, and switches manufactured into a single small package.

Heres the process...

1. The process starts with a ***silicon crystal ingot*** which are 8-12 inches in diameter and about 12-24 inches long.
2. The ingot is then finely sliced into ***wafers*** no more than 0.1 inches thick.
3. These wafers then go through a series of processing steps that place patterns of chemicals on each wafer, creating the transistors, conductors, and insulators.

> [!DANGER] Todays ICs contain only one layer of transistors but may have from two to eight levels of metal conductor, separated by layers of insulators. 

![[Screenshot 2026-01-31 at 10.36.37 PM.png]]

A single microscopic flaw can cause that area of the wafer failing. The simplest way to get around this is to place many independent components on a single wafer. This patterned wafer is then diced into components called ***dies***.

![[Screenshot 2026-01-31 at 10.38.44 PM.png]]
This allows to discard only dies that have flaws instead of losing the whole wafer. This concept is quantified by the ***yield*** of the process.

***Yield*** - The percentage of good dies from the total number of dies on the wafer.

Once good dies are found, they are connected to the I/O pins of a package via a process called ***bonding***, tested a final time, and then shipped to customers.

---
# <u> The Cost of an Integrated Circuit </u>

#### ***Cost per Die***
$$
CostPerDie = \frac{CostPerWafer}{DiesPerWafer \times yield}
$$
#### ***Dies per Wafer***
$$
DiesPerWafer = \frac{WaferArea}{DieArea}
$$
#### ***Yield***
$$
Yield = \frac{1}{(1 + (DefectsPerArea \times DieArea / 2))^2}
$$

---
# <u> Going Faster: Matrix Multiply in Python </u>

Imagine this block of code:
```python
for i in xrange(n):
	for j in xrange(n):
		for k in xrange(n):
			C[i][j] += A[i][k] * B[k][j]
```
Assuming a system with two Intel Skylake Xeon chips, each chip having 24 processors and running python 3.1
- Code above will take about 5 minutes if the matrices are 960 x 960
