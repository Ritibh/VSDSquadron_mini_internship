# VSDSquadron_mini_internship
A 4-week internship based on VSDSquadron mini RISC-V Board based on RV32EC ISA .

## Details
### Name : Ritibh Singh
### Instructor : Kunal Ghosh


# TASK 1 :

## Installation of RISC-V toolchain using VDI. Writing a C code and compiling using RISC-V compiler and uploading snapshots 

so below are the steps to complete task 1 

### 1. Installation of Oracle Virtualbox and open the terminal

![virtual](https://github.com/user-attachments/assets/9e3dca42-232a-45b0-9827-5a83d094e23f)

using this click on the left column tab to open the terminal



### 2 . Writing C code, its compilation and output
Now write a C code to count the numbers from 1 to n using leafpad editor 
command for it is **leafpad sum1ton.c** and write c code,save it and compile using **gcc sum1ton.c** and run simulation using **./a.out**

---
![c_code](https://github.com/user-attachments/assets/1621f5c4-cccc-451e-8c68-cf2c997cf583)

---




![compilation output](https://github.com/user-attachments/assets/d46bafe2-62c9-4ccf-8a76-18f51d35fbd6)




### 3. Running the C code using RISC-V compiler and then generating the assembly code using objdump

The command used to compile using the RISC-V compiler is **riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=riscv64i -o sum1ton.o sum1ton.c** this will create the objdump file
and now using the command **riscv64-unknown-elf-objdump -d sum1ton.o** will generate the assembly code


---
![assemblygeneration](https://github.com/user-attachments/assets/92db2086-87fa-4a03-85c1-b258818141b4)
---

### 4. Generating a smaller version of assembly code using the fast command 

The command used to compile the smaller version using the RISC-V compiler is **riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=riscv64i -o sum1ton.o sum1ton.c** this will create the objdump file
and now using the command **riscv64-unknown-elf-objdump -d sum1ton.o** will generate the assembly code


---
![assemblyfast](https://github.com/user-attachments/assets/56cc1328-7fab-4b75-9e04-abae4bb54e4d)
---


# TASK 2:
## SPIKE Simulation and Debugging a simple C code with Interactive Debugging Mode using Spike
## What is SPIKE?
Spike is a free, open source C++ simulator for the RISC-V ISA that models a RISC-V core and cache system.It can be used to run programs and a Linux kernel, and can be a starting point for running software on a RISC-V target.
## Testing the SPIKE Simulator
The first step is to confirm the output of the **sum1ton.c** code using the SPIKE Simulator. The command for it is:
**spike pk sum1ton.o**


















