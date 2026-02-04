# <u>Introduction</u>
*Combinational Circuits only depend on the current inputs applied. Any change in inputs will change the output.
Sequential Circuits not only depend on the current inputs but also the previously entered inputs.
A complex sequential data path requires hand-full of hardware:
- Combinational Circuits to generate outputs as results.
- Storage Modules (like registers) to save those results.
- Control Units that follows a specific set of steps to compute a function using the data path.

> [!IMPORTANT] Important
> A Control Unit is a ***Sequential Circuit*** and uses storage modules to save its current state (a specific step in the algorithm) in order to determine its next state using the inputs it currently recieves.

***Sequential Circuits*** also require a timing control signal called a ***clock***
It's used to determine when a value should be stored in the storage module.

> [!IMPORTANT] Important
> ***Clock*** signals are needed because different ***Combinational Circuits*** with different data paths have different propagation delays. The circuits that have shorter propagation delays generate their outputs sooner than those with longer propagation delays, resulting in the computation of inaccurate data. ***Clock*** signals validity of the data and allows the storage module to save it.


# <u> SR Latch </u>
