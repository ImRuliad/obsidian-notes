## Just like combinational circuits (CC), sequential circuits can also be broken up into
	- Small Circuits
	- Large Circuits
All small and large sequential circuits are made of flip-flops and a set of CCs.
Sequential circuits are subject to environmental hazards like transient faults that occur randomly. One way to protect against this is ***through fault-tolerant design.***

## Design Of A Sequential Circuit
	- The design of sequential circuits is typically done as a Finite State Diagram.
	- A Finite State Diagram is then converted into a circuit called a Finite State Machine.
	- Each state is a D Flip-Flop
	- The amount of states needed for a FSD is dependent on the amount of bits being handled. 3-bits e.g. 010 is 3 D Flip-Flops.
A large sequential circuit is typically partitioned into the design of a data path and a control unit.

The data path would contain
	- CC Modules like ALUs MUXs and Decoders
	- Small sequential circuits like registers and counters.


## An illustration of a 4-bit parallel-load register
![[Screenshot 2025-11-04 at 6.19.36 PM.png]]
This design of an n-bit register can be partitioned using n amounts of 1-bit register slices.
The behavior of this register slice can be formally modeled as an FSD.

## The FSD of a 1-bit register slice
![[Screenshot 2025-11-04 at 6.21.16 PM.png]]
After this is completed, we can make a detailed block diagram of the 1-bit register slice as a FSM.

## The FSM of a 1-bit register slice
![[Screenshot 2025-11-04 at 6.22.18 PM.png]]


# Multifunction Registers
This figure shows the block diagram of a four function register with an *n-bit* input X and output Z.
It has a *2-bit* function code *F = f<sub>1</sub> f<sub>0</sub>*
The register is enabled when active-high enable signal is asserted.
active-low reset initializes asynchronously to 0. 
![[Screenshot 2025-11-06 at 11.06.54 PM.png]]
# Finite State Machine Design
FSM can be labeled as either *Mealy* or *Moore*
- The minimum number of bits required to encode the states of an FSD is *log<sub>2</sub>K* where *K* is the number of states.

### Mealy
- Depends on current state and current inputs.
### Moore
- Synchronously depend on external inputs.
-![[Screenshot 2025-11-06 at 11.48.00 PM.png]]
# Sequential Circuit Timing
Flip Flops that share a common clock signal are expected to receive the sampling edge of the clock at the same time so that all flip flops can sample their inputs simultaneously and before the arrival of the next sampling edge.

Delays in the in the transmission of the clock signal result in some flip flops receiving the sampling clock edge later than other flip flops.
This is known as *clock skew* T<sub>cs</sub>.
- flip flops that receive sampling clock edge earlier change their inputs before others will.
- causes newly sampled inputs to modify all or some of the inputs for the flip flops who have not yet completed sampling their inputs.
- causes a *setup-time* or *hold-time* violation or invalid state transition.

The earlier time that a q<sup>new</sup> can change a d<sup>current</sup> is the sum of the minimum *clock-to-q* time T<sub>cq-min</sub> and the minimum *circuit delay propagation* delay T<sub>pd-min</sub> 
T<sub>cs</sub>  <= T<sub>cq-min</sub> + T<sub>pd-min</sub>
![[Screenshot 2025-11-07 at 12.04.26 AM.png]]