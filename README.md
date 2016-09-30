# Design-of-the-Basic-Microcontroller

Design of a microcontroller with the given specifications using Verilog with FPGA

Main Blocks: This microcontroller consists of three systems basically: memory, controller and ALU
----------------------
Memory: Required data and instructions are stored in the memory. Using basic flip flops will be enough
for this project.
----------------------
Instruction Memory: It is the memory block which instructions are stored. Instructions are read by the
controller and commands are given to the ALU. The content of the instruction data is predefined by the
user. You can define the content in a specific region of your Verilog code. The content of the instruction
memory is determined by the sets of instructions used in the operation of the microcontroller and your
algorithm of application.
----------------------
Data Memory: It stores the data taken from outside. ALU reads required data from this memory and
uses it. Data taken from input ports are stored into the data memory. You can design your Data memory
as a shift register to make write operation easier. However you should be able to read the stored data in
any address of your data memory using microcontroller designed.
----------------------
Controller: This unit will generate required signals between ALU and Memory units.
The controller reads the instructions from instruction memory unit and sends required signals to ALU. In
other words it translates from machine instructions to the control signals that implement them.
It includes several registers such as PC (program counter), MAR (Memory Address Register), IR
(Instruction register).
----------------------
reg1(Accumulator): 16 bit register. It can be read or write enabled.
----------------------
ALU(Arithmetic Logic Unit): The ALU is the basic part of the project where it makes the necessary
operations by using the data stored in memory and the 16 bit register “reg1”. The command bits are
used to determine the operation that is going to be done by using the input data in and register “reg1”.

The instructions are processed in the “Fetch-Decode-Execute” cycles. In the “Fetch” cycle, the
instruction is read from memory location pointed by the PC and written into the Instruction Register(IR).
In “Decode” cycle, the “Opcode”(OPC) of the instruction in IR is decoded. If the OPR is a memory
address, then the required data should be read from that memory location first. In Execute cycle, the
operation OPC is executed using the operand OPR.

<img src="https://github.com/emreatik/Design-of-the-Basic-Microcontroller/blob/master/Basic%20Microcontroller.PNG"/>
----------------------
Instruction Format
----------------------
First five bit of the instruction is Opcode (OPC) and remaining seven bit is Operand (OPR). You can
increase number of bits in OPR if needed. OPC represents the instruction code of the operation and OPR
represents the data to be used in the operation. If the OPR is a memory address instead of data, then 
8
the required data should be read from that memory location first. In Execute cycle, the operation OPC is
executed using the operand OPR.
Each instruction lasts for 7 clock cycles. At 8th clock cycle, program counter increases its instruction
address value by one and the next instruction is fetched.
In a basic microcontroller, each operation is performed by a set of microoperations in fetch and execute
cycles:
1. Fetch an instruction from memory
2. Decode the instruction
3. Execute the instruction
4. After an instruction is executed, the cycle starts again at step 1, for the next instruction.
Example: Cycle by cycle operation of two examples are given below. 

<img src="https://github.com/emreatik/Design-of-the-Basic-Microcontroller/blob/master/Example%201.PNG"/>

<img src="https://github.com/emreatik/Design-of-the-Basic-Microcontroller/blob/master/Example%202.PNG"/>
