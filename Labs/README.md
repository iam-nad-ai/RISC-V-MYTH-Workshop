Compile command:

`$ riscv64-unkown-elf-gcc -O<1/fast> -mabi=lp<XLEN> -march=rv<XLEN>i -o <output_program> <input_user_file> [<input_user_file>...]`

Assembly preview command:

`$ riscv64-unkown-elf-objdump -d <output_program>`

Run command:

`$ spike pk <output_program>`

Debug command:

`$ spike -d pk <output_program>`

The Application Binary Interface (ABI), also known as the System Call Interface, is used by the program to access the ISA registers. RISC-V architecture contains 32 registers of width 32/64 if using RV32I/RV64I, respectively:

| Register | ABI Name | Usage |
| -------- | -------- | ----- |
| x0 | zero | Hard-wired zero |
| x1 | ra | Return address |
| x2 | sp | Stack pointer |
| x3 | gp | Global pointer |
| x4 | tp | Thread opinter |
| x5-7 | t0-2 | Temporaries |
| x8 | s0/fp | Saved register/frame pointer |
| x9 | s1 | Saved register |
| x10-11 | a0-1 | Function arguments/return values |
| x12-17 | a2-7 | Function arguments |
| x18-27 | s2-11 | Saved registers |
| x28-31 | t3-6 | Temporaries |

There are 3 types of instructions:
1. **R-type:** operate only on registers<br>
    Ex: `add x8, x24, x8`
2. **I-type:** operate on registers and immediate values<br>
    Ex: `ld x8, 16(x23)`
3. **S-type:** operate on source registers and store in immediate value<br>
    Ex: `sd x8, 8(x23)`

1. picorv32 RISC-V Verilog code was taken as an example, which generated a firmware.hex as an output file
   
   <img width="778" height="554" alt="Screenshot 2026-07-29 at 19 21 06" src="https://github.com/user-attachments/assets/895da1ad-4f91-496b-84d6-7d89f4d313cf" />

3. Counter was implemented in TL Verilog which takes val1 and val2 as two random inputs and performs various arithmetic operations (sum, diff, prod, quot)

   <img width="547" height="277" alt="Screenshot 2026-07-29 at 19 25 24" src="https://github.com/user-attachments/assets/e001adbd-bfd9-4ad4-acf6-3b8becdedb7c" />

