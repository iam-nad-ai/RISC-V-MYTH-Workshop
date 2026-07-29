## [Introduction to RISC-V ISA] 
A RISC-V ISA is defined as a base integer ISA, which must be present in any implementation, plus optional extensions to the base ISA. Each base integer instruction set is characterized by
  1. Width of the integer registers (XLEN) 
  2. Corresponding size of the address space
  3. Number of integer registers (32 in RISC-V)
 Basic RISC-V CPU micro-architecture

Designing the basic processor of 3 stages fetch, decode and execute based on RISC-V ISA.
1. Fetch (Program Counter & Instruction Fetch)
   
Role: Fetches the next instruction from Instruction Memory using the current Program Counter (PC) address.
Logic: Increments the PC sequentially (PC+4) or updates it to a target address if a branch or jump is taken.

During fetch stage, processor fetches the instruction from the IM pointed by address given by PC. 
<img width="652" height="228" alt="Screenshot 2026-07-29 at 22 00 37" src="https://github.com/user-attachments/assets/2199d315-3d8b-48bc-876f-cb4e9022f77c" />

## [Instruction Decode]

6 types of Instructions:
  * R-type - Register 
  * I-type - Immediate
  * S-type - Store
  * B-type - Branch (Conditional Jump)
  * U-type - Upper Immediate
  * J-type - Jump (Unconditional Jump)

Instruction Format includes opcode, immediate value, source address and destination address. During decode stage, processor decodes the instruction based on instruction format and type of instruction. 

Role: Parses the fetched raw 32-bit instruction into operational fields (opcode, function codes, source/destination register addresses, and immediate values).
Logic: Generates immediate signals (Sign Extension) and determines the required control path for execution.

<img width="694" height="228" alt="Screenshot 2026-07-29 at 22 03 32" src="https://github.com/user-attachments/assets/6d87f0ac-0076-483c-a9b2-99c3003c8ff3" />

## [Register File Read]

Here the Register file is 2 read, 1 write which means 2 read and 1 write operation can happen simultaneously.
Role: Reads data from the general-purpose Register File based on the source register specifiers (rs1 and rs2).
Logic: Provides multi-port simultaneous access to supply dual operands to downstream logic within a single clock cycle.

<img width="659" height="232" alt="Screenshot 2026-07-29 at 22 05 54" src="https://github.com/user-attachments/assets/86503f7b-1175-49bc-8be4-03f42462f751" />

## [ALU]

During the execute stage at ALU, both the operands perform the operation based on opcode. 
Role: Performs core arithmetic (add, subtract), logical (AND, OR, XOR), and bitwise shifting operations
Logic: Takes inputs from the Register File or Immediate values and evaluates comparison conditions used for branching.

<img width="642" height="226" alt="Screenshot 2026-07-29 at 22 07 07" src="https://github.com/user-attachments/assets/e9d8bde3-2c60-417a-895d-9607727edce7" />


## [Control Logic for Jump and Branch]

During decode stage, branch target address is calculated and fed into PC mux. Before execute stage, once the operands are ready branch condition is checked. 

Role: Handles non-sequential program execution flow.
Logic:
Branches (BEQ, BNE, etc.): Evaluates ALU flags/comparison signals against condition rules; if true, redirects PC to PC+Immediate.
Jumps (JAL, JALR): Unconditionally redirects execution to the target address while saving the return address (PC+4) to the destination register.

<img width="602" height="228" alt="Screenshot 2026-07-29 at 22 08 05" src="https://github.com/user-attachments/assets/273a19f2-6ba3-49f0-b767-f8d3e9c7c6f1" />

## [Register File Write]
Role: Writes execution results back into the Register File at the destination register address (rd).
Logic: Uses multiplexers to select the write data source either the ALU result, loaded data from Data Memory, or the Return PC from a jump instruction.

<img width="641" height="221" alt="Screenshot 2026-07-29 at 22 12 01" src="https://github.com/user-attachments/assets/2c2d3e69-6720-4318-93b0-00df95f23bdc" />
