# <u>Introduction</u>
*A register is designed to store a single value that is readily available when needed.*
*Memory is designed to store the code and data of programs during execution.*
*Implementing memory requires much less hardware than a latch or flip-flop but requires more time to read or write data.*


> [!IMPORTANT] Important
> The storage size of memory is defined in terms of ***bytes (B)***, 8 bits per byte.
![[Screenshot 2025-11-14 at 3.27.24 PM.png]]

#### The Figures below represent two logical views of 1024 B (1 KB) memory
![[Screenshot 2025-11-14 at 3.29.00 PM.png]]
***On the left***:
- Memory is viewed as having 1024 locations, each with 1 B content.
- 1024 addresses x 8 bits requires a 10-bit address. 
- 1024 = 2<sup>10</sup> to identify each of the 1 B (8 byte) content.
***On the right:***
- Memory is viewed as having 512 locations, each with 2 B content.
- 512 x 16 bits requires a 9-bit address.
- 512 = 2<sup>9</sup> to identify each of the 2 B (16 byte) content.

> [!IMPORTANT] Important
> The performance of a Von Neumann machine directly depends on fast data can be read or written to memory.
> The speed of CPUs has increased at a faster rate than that of memory. Faster memory technologies and better memory architectures have helped bridge the gap.
> [[Chapter 6 Sequential Circuits (Large Designs)#<u> Pipelined </u>|Pipelining]] has been used to increase concurrency by overlapping memory operations and reduce average read/write time.
> Parallelism has been used to deliver more data in less time to improve performance of multiprocessor systems and real-time applications.

---
# <u>Memory Technologies</u>
Memory technologies are categorized as read-only memory (ROM) or random access memory (RAM).
The hardware used to store 1 bit of data is called a ***memory cell***.
In a ROM cells are nonvolatile (retains their content when not powered).
In a RAM cells are volatile (loses their content when not powered).

![[Screenshot 2025-11-14 at 3.47.08 PM.png]]
*Circuit examples of an SRAM and DRAM cell*

##### <u>nMOS Transistor</u>
- On the bottom is an nMOS pass transistor with three pins labeled **a**, **b**, and **e**.
- If **e** (enable) = 1 then current flows in either direction between **a** to **b** or **b** to **a**. 
- if **e** = 0 then pins **a** and **b** are electrically isolated.
##### <u>SRAM Cell</u>
- When the cell is selected, the two nMOS pass transistors connect **d** to **q** and **/d** to **/q**.
- The cell content can now be read or written as **q** or **/q**.
- When the cell is not selected, the two pass transistors keep the two cross-coupled NOT gates isolated from **q** and **/q** signals.
- During this time the cell retains its stored value **d** as long as the cell is powered.
##### <u> DRAM Cell </u>
- When cell is selected and memory is performing a write operation the capacitor is charged to a voltage level representing logic 1.
- Otherwise, the nMOS pass transistor keeps the capacitor isolated and not connected to ***q*** signal.
- If the isolated capacitor is charged to logic 1 voltage level, it retains its charge for only a short time (64ms).
	- It must be refreshed periodically during a ***refresh cycle*** otherwise content would be lost over time due to current leak.

---
# <u> Random Access Memory</u>
*RAMs are designed to function as the main storage for programs and data during execution.*
- *A RAM cell is called static (**[[Chapter 7 Memory#<u>SRAM Cell</u>|SRAM]]**) if logic 1 is stored as a **static** charge (retained as long as memory is powered).*
- *A RAM cell is called dynamic (**[[Chapter 7 Memory#<u> Modern DRAM </u>|DRAM]]**) if logic 1 is stored as a dynamic charge, and can be retained for a short period of time before needing to be refreshed.

| SRAM                                 | DRAM                            |
| ------------------------------------ | ------------------------------- |
| Requires two transistors             | Requires one transistor         |
| Requires two cross-coupled NOT gates | Requires one small capacitor    |
| Much Larger than the DRAM cell       | Much smaller than the SRAM cell |

[[Chapter 7 Memory#<u>Memory Technologies</u>|SRAMs]] require more hardware and are thus more expensive per byte, but they are faster than [[Chapter 7 Memory#<u>Memory Technologies</u>|DRAMs]]  because they do not require refresh and write-after-read cycles.
[[Chapter 7 Memory#<u>Memory Technologies</u>|DRAMs]] are used as main memory and [[Chapter 7 Memory#<u>Memory Technologies</u>|SRAMs]] as cache memory to decrease average time required to access data as discussed in [[Chapter 10 Memory System]].

---
## <u> Memory Cell Array </u>
*All memories internally use 2D cell organizations in order to:
- Reduce total number of signals required to select a target cell
- Refresh multiple cells at the same time*
A 2D cell organization required two selections per cell but far fewer selection signals.
![[Screenshot 2025-11-23 at 10.54.14 PM.png]]

When one of the row-selection signals is asserted, all the cells in that row are selected at the same time. This is called ***row-activation***.
- The row selection signal is the output of an address decoding circuit, so it doesn't require a fan-out to activate a large number of cells.
- The signal enables a transistor that allows a power source to activate all cells on that row.

The content of each cell on the activated row is determined or ***sensed*** as logic 0 or logic 1 using a special circuit called a ***sense amplifier***.
- The ***sense amplifier*** compares the cells voltage level with a reference voltage source like 50% of the voltage needed to represent logic 1.
- During a read operation if the cell contains logic 0 it will pull down the reference voltage slightly causing the ***sense amplifier*** to read logic 0.
- Otherwise, the voltage level for logic 1 in the cell will pull the reference voltage slightly up, causing it to detect logic 1.

Only one sense amplifier per column is needed.
- The logic 0 or 1 from the sense amplifier is latched, and made available to the tri-state buffers controlled by the column-selection signals.
- In the case of [[Chapter 7 Memory#<u>Memory Technologies</u>|DRAMs]] , the output of the latch is also used to refresh the target cells after each read.

---
## <u> Word Access </u>
In the figure below is a 512 x 2 (2 bit word) memory organized as such:
- 1024 cells are organized as two separate 32 x 16 x 1 cell arrays.
- effectively creating a 32 x 16 x 2 array.
- cells are accessed two at a time, one from each of the 32 x 16 x 1 cell arrays.
Selecting row 0 and col 0 will select the cell at the intersection of row 0 and column 0 as well as the cell at the intersection of row 0 column 16.
![[Screenshot 2025-11-23 at 11.10.28 PM.png]]

---
## <u> Burst Access </u>
*Burst Access refers to the memory's to transfer a burst of data
- can be small (a few bytes)
- can be large, the size of a large block (e.g. 4 KB) called a ***page*

Burst accessing is implemented by activating a row and then asserting the column selection signals one at a time and in some specific order to either read or write a specific set of cells.
- Each burst access must be first preceded by a row activation operation.
- If page access or ***page mode access*** expands multiple rows, then memory may be enabled to automatically activate each succeeding row when access from the current row is complete.
	- This increases memory efficiency.

> [!IMPORTANT] IMPORTANT
> In order to make memory even more efficient, the cells can be organized into banks, each a cell array.
 Memory is designed using four banks, each a 32 x 32 x 1 cell array. 
 A row activation operation in another bank can be started while the memory operation on the current bank is still in progress. 
 Makes bank-access turn around time shorter when memory is required to perform operations that involve different banks.
Most modern memory chips support word access, are multibanked, and support burst and page mode access.
![[Screenshot 2025-11-23 at 11.29.54 PM.png]]

---
## <u> Memory Organization </u>
*Memory organization refers to the internal components and their organization within a memory chip. 
Several memory chips create a ***Memory Unit***.

Memory units have a memory communication protocol including
- address bus
- data bus
- control bus

##### **Address Bus**
- specifies the address of a single memory location, which could be the starting address of a burst or page access.
- selects a set of target cells for read or write operations
##### **Data Bus**
- used to communicate with other components in the system.
##### **Control Bus**
- used to specify read or write operations.

![[Screenshot 2025-11-24 at 10.45.08 PM.png]]
**SRAM**
- Requires a 10-bit address bus with signals labeled a<sub>0</sub> to a<sub>9</sub>
- a 1-bit data bus labeled ***d***
- three active low control bus signals labeled _ _ce (chip enable), _we(write enable), and _oe(output enable).

> [!IMPORTANT] IMPORTANT
> When _ce is asserted, selects the memory chip and a set of target cells to perform either a read if _we = 1 (not asserted) or a write if _we = 0 (asserted).
> when  _oe is asserted, causes the data from the SRAM to appear on the data bus during a read operation.

**DRAM**
- Has many more cells and requires cells to be refreshed.
- has additional control signals like row address strobe (ras) and column address strobe (cas)
	- used to specify a single memory address in two parts, a row address and column address, using the address bus.
- _ _ras and _cas are also used to place memory in a refresh cycle mode.

---
## <u> Modern DRAM </u>
*A modern DRAM chip is designed to operate synchronously. It is called a synchronous DRAM (SDRAM)
May contain one or more [[Chapter 6 Sequential Circuits (Large Designs)#<u> Pipelined </u>|Pipelined Data Paths]] to increase memory bandwidth

Uses interface signals (below) as a 4-bit instruction called a ***memory command*** to select and send row and column addresses.
Also uses an ***access mode*** ([[Chapter 7 Memory#<u> Word Access </u>|single access]] or [[Chapter 7 Memory#<u> Burst Access </u>|burst access]] to the chip)
- _ _ce (chip enable)
- _ _ras (row address strobe)
- _ _cas (column address strobe)
- _ _we (write enable)
![[Pasted image 20251124231244.png]]
![[Pasted image 20251124231341.png]]

> [!IMPORTANT] Important
> SDRAM operates at the speed of one data item per clock cycle.
> A double data rate (DDR, DDR2, DDR3, etc..) SDRAM operates at two data items per clock cycle.
> One data item is transferred on the positive edge of the clock cycle, and the other on the negative edge.

---
## <u> SRAM </u>

![[Screenshot 2025-11-25 at 6.32.06 PM.png]]
*Schematic logic model of an SRAM Cell*

- It contains an [[NOT DONE Chapter 4 Sequential Circuits (Core Modules)#<u> SR Latch </u>|SR Latch]] (without the clock).
- Also contains three tri-state buffers.
- Two resistors that connect the outputs of the tri-state buffers to ground (pull down resistors)
	- Causes outputs to become 0 instead of high impedance (Z) when tri-state buffers are not enabled.
	- Makes the *s* and *r* inputs of the SR Latch both 0, causing the latch to retain its stored 0 or 1 value when cell is not selected.

![[Pasted image 20251125184121.png]]
*The internal organization of a 16 x 1 SRAM using a 4 x 4 x 1 cell array.*

---
## <u> Memory Timing </u>
*Memory timing specifies the timing of [[Chapter 7 Memory#<u> SRAM </u>|SRAM]]* or [[Chapter 7 Memory#<u> Modern DRAM </u>|DRAM]] control signals or the timing of [[Chapter 7 Memory#<u> Modern DRAM </u>|SDRAM]] commands.

> [!IMPORTANT] IMPORTANT
> The total time required to select target cells and perform read or write operations is called ***Memory Access Time***
> A ***Memory Cycle*** includes both ***Memory Access Time*** and ***Data Transfer Time***
> 
> ***Memory Access Time*** is directly proportional to the size of the memory cell array, which determines the size of the row and col decoders inside the memory chip.


#### SRAM Read Cycle
![[Pasted image 20251125185533.png]]
- At the start of the read cycle, a memory address is placed on the address bus before or at the same time the _ _ce_ is asserted.
- The _ _oe_ signal is used with the _ _ce_ to control one or more output tri-state buffers.
- In order to minimize duration of the read cycle, _ _oe_ can be asserted at any time within a max time after the _ _ce_ is asserted.
- The _ _oe_ allows the data bus to be used only when data from the cell array is available and NOT before.
- _ _ce_ is deasserted last because it would disable the output tri-state buffers as well as the column decoder.

#### SRAM Write Cycle
![[Pasted image 20251125185948.png]]
- Operates the same as a read cycle except the data must be placed on the data bus at the same time that _ _ce_ is asserted or within a maximum delay after _ _we_ is asserted.

> [!IMPORTANT] IMPORTANT
> A memory cycle is initiated by the CPU and typically takes multiple CPU clock cycles to complete

#### DRAM Read & Write Cycles
*Read and Write cycles of a DRAM require that the target memory address be issued in two parts using the [[Chapter 7 Memory#**Address Bus**|Address Bus]]
- Row Addresses
- Col Addresses
*This reduces the size of the [[Chapter 7 Memory#**Address Bus**|Address Bus]]  and can reduce the total time required to complete a [[Chapter 7 Memory#<u> Burst Access </u>|Burst Access]]*

![[Pasted image 20251125190755.png]]
*DRAM read and write cycles*
- A DRAM read or write cycle begins by issuing a row address and asserting the _ _ce_ signal.
- The _ _ras_ signal is asserted so the DRAM can load the row address into an internal register and activate the next target row.
- The column address is issued and the _ _cas_ is asserted.
- This selects one or more target cells on the activated row.
- The _ _oe_ and _ _we_ signals function the same as [[Chapter 7 Memory#SRAM Read Cycle|SRAM Read and Write Cycles]]

> [!IMPORTANT] IMPORTANT
> DRAMs require refresh cycles to restore the content of each cell.
> A ***cas-before-ras*** refresh cycle requires the assertion of the _ _cas_ signal before the _ _ras_ to switch the DRAM into refresh mode.
> 
> DRAMs are used to build [[Chapter 7 Memory#<u> Modern DRAM </u>|SDRAM]].

## <u> High-Order (Course) Interleaving </u>
*Divides total logical memory space into two or more continuous data regions.*
*The data of each region is stored in separate memory modules or even memory units.*

> [!IMPORTANT] IMPORTANT
> In a k-way high-order interleaving, the k most significant address bits are used to partition the logical memory space into 2<sup>k</sup> regions.

![[Pasted image 20251125192729.png]]
![[Pasted image 20251125192757.png]]
*An example of high-order interleaving*

## <u> Fine-Order (Fine) Interleaving </u>
![[Pasted image 20251125192839.png]]
*An illustration of Fine-Order Interleaving*




