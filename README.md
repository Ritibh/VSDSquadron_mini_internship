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

The command used to compile the smaller version using the RISC-V compiler is ```**riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=riscv64i -o sum1ton.o sum1ton.c**``` this will create the objdump file
and now using the command ``` **riscv64-unknown-elf-objdump -d sum1ton.o** ``` will generate the assembly code


---
![assemblyfast](https://github.com/user-attachments/assets/56cc1328-7fab-4b75-9e04-abae4bb54e4d)
---


# TASK 2:
## SPIKE Simulation and Debugging a simple C code with Interactive Debugging Mode using Spike
## What is SPIKE?
Spike is a free, open source C++ simulator for the RISC-V ISA that models a RISC-V core and cache system.It can be used to run programs and a Linux kernel, and can be a starting point for running software on a RISC-V target.

### Testing the SPIKE Simulator


The first step is to confirm the output of the  **sum1ton.c** code using the SPIKE Simulator. The command for it is:
```
**spike pk sum1ton.o**
```
---
![spike output](https://github.com/user-attachments/assets/5d7af266-b81a-4b56-a68a-5a1ef6316faf)
---

### Debugging the sum1ton.o assembly code
- open the **Objdump** of code by using the following command
```
riscv64-unknown-elf-objdump -d sum1ton.o | less
```
- open the debugger in another terminal by using the following command
```
spike -d pk sum1ton.o

```
#### Now we can perform the debug and know the contents of the Registers and what happens after every instruction and address

- To know the contents of a register at a particular address use the following command

```
until pc 0 100b0
```
```
reg 0 a0
```
this will show contents of register a0.

![debugging](https://github.com/user-attachments/assets/38505f96-c0e6-41fc-b42f-8da05d0e8ef3)



## Program to find table of a number
**now we will write a simple c code to calculate table of any number and then perform gcc/spike simulation and create objdump as well as debugging using SPIKE**

Below are the steps-

**1. write a C code and compile using  ``` gcc table.c ``` and get output using ``` ./a.out ```**

![simple_c_code](https://github.com/user-attachments/assets/ef5091ac-fa53-4c3e-aa80-31f1008d2849)


![simple_c_code_gcc_output](https://github.com/user-attachments/assets/71ecf5cb-cc33-4299-9e46-2f78430fc787)

**2. Now we will generate the assembly code and objdump using the -O1 and -Ofast command**



![simple_c_code_with_01](https://github.com/user-attachments/assets/f75be944-7505-4127-87aa-33dae6f24631)

using the command

```
riscv64-unknown-elf-gcc -o1 -mabi=lp64 -march=riscv64 table.o table.c
```

![simple_c_code_with_ofast](https://github.com/user-attachments/assets/33e39325-c2b4-4379-b7c6-735c3b4acfad)

using the command
```
riscv64-unknown-elf-gcc -ofast -mabi=lp64 -march=riscv64 table.o table.c
```







**3. Now we  will test the same output using spike**

   ```
   spike pk table.o

   ```

   ![simple_spike_op](https://github.com/user-attachments/assets/ef9554f5-288a-44a5-b8e6-260fdeb002f1)


**4. Now we will debug the assembly code with help of spike**

```
spike -d pk table.o

```
this will open the debugger and now we can start to debug

- First we will try to know the contents of a register , since the running of the main code starts from ``` 100b0 ``` address which has register ``` a0 ```

- we will identify the contents of ``` a0 ```

using

```
until pc 0 100b0
```

```
reg 0 a0

```
---
![contents a0](https://github.com/user-attachments/assets/27b1b9fa-230f-4264-8e99-503cc9e1543c)
---
---
![more debugging](https://github.com/user-attachments/assets/8db687e6-e9bc-41c5-8b5e-8c5fb86033eb)
---

# TASK 3:
## RISC-V Instruction types & List of 15 instructions from assembly code with 32 bit instruction

The RISCV ISA has 6 different types of Instructions as **R-type , I-type, S-type, B-type , U-type, J-type** as shown in below image

![riscv_instructions](https://github.com/user-attachments/assets/c02ff83d-75c1-4ebc-9057-607dc3b91cfc)

the RISC- V Instructions have a same specific format for all instructions which makes it easy to implement the hardware. The 32 bit field of instructions consist of -

```
1.  opcode : This sideband signal is used to identify the instruction format

2.  rd : one 0f X0-X31 Registers used as destinaton register to store the ouptut of the operation

3.  rs1 : one of X0-X31 registers used as source registers for data.

4. rs2 : one of X0-X31 registers used as source registers for data.

5. funct3/funct7 : sideband signals used for further decoding of the instruction format.

6. imm : contains immediate value to be processed by instruction
```

### R-type Instructions -
The R-type instructions perform all the arithmetic operations on rs1, rs2 and store in rd. The immediate value is 0 for R-type instructions.

Different R-type instructions are shown below image


![R_tpye](https://github.com/user-attachments/assets/a028d71d-5a4d-4f5c-8d6c-550596a4f678)

**example** ``` add x1,x2,x3```

### I-type Instructions -

There are three different types of I-type of instructions.

#### 1. Arithmetic Immediate operations -

These Instructions perform arithmetic operation on one of the source registers rs1 and immediate value.

example - ```addi,subi```

![I_type_0](https://github.com/user-attachments/assets/2adeef82-c056-4bec-9fbd-dac302b82bda)


#### 2. Load type Instructions - 

These type of instructions provide load operations i.e any data stored in the data memory can be retrieved to rd.

example - ```lb,lh```

![I_type_1](https://github.com/user-attachments/assets/fd20d408-9c02-4ecb-af1c-2e0e6bfdba61)



#### 3. Jump and Link Instructions - 

This provides jump operations. Target address is obtained by adding the sign extended 12 bit I-immediate to rs1 then setting LSB of result to zero.

![I_type_2](https://github.com/user-attachments/assets/e7436160-8da5-4528-afc9-a0337979a9fe)

### S-type of instructions- 

These instructions provide store operation to store the result into the memory from rs2.

![S_type](https://github.com/user-attachments/assets/2725d296-f94a-4f9f-99d9-c0877c06cc29)

example - ```SB,SH```

### B-type Instructions -

These are the branch Instructions , **example** - ``` BEQ,BNE,BLT,BGE``` . ALU performs the calculation of the branch target address and the decision to take branch is calculated by the control logic

![B_type](https://github.com/user-attachments/assets/8c3b4f55-483e-4769-ac06-9aaf6d7d64d3)

### U-tpye Instructions-

There are 2 types of U-type Instructions-

**1. LUI (Load Upper Immediate)** - This is used to build the 32 bit constants. The upper 20 bits of rd are filled with data and rest 12 bits are filled with 0.

**2. AUIPC (ADD upper immediate to PC)** - This is used to build PC-relative address. AUIPC forms a 32 bit offset from 20 bit U-immediate fillinf lower 12 bits with 0. , adds this offset to address of AUIPC instruction and places result in rd,


![U_type](https://github.com/user-attachments/assets/c9b5db01-9a96-47cc-ac64-2988e38d21da)


### J-type instructions -

**JAL(Jump and Link)** is used for unconditional jumps. the immediate offset is added to the address of the jump instructions to form jump target address.

![J_type](https://github.com/user-attachments/assets/f757ae68-99c6-48d0-9652-1a7bf2813325)











## 15 Types of Instructions in Assembly code-
1. ```addi x1, x2, 10```

- Instruction Format: I-type
- Binary Encoding: 000000000010 00010 000 00001 0010011
- 32-bit Instruction Code: 0x00210093

  
2. ```li x5, 0x0```

- Instruction Format: I-type (using addi x5, x0, 0x0)
- Binary Encoding: 000000000000 00000 000 00101 0010011
- 32-bit Instruction Code: 0x00000293

3. ```lui x10, 0x20000```

- Instruction Format: U-type
- Binary Encoding: 00100000000000000000 01010 0110111
- 32-bit Instruction Code: 0x20000537

4. ```mv x1, x2```

- Instruction Format: I-type (using addi x1, x2, 0)
- Binary Encoding: 000000000000 00010 000 00001 0010011
- 32-bit Instruction Code: 0x00010093

5. ```sw x5, 0(x10)```

- Instruction Format: S-type
- Binary Encoding: 0000000 00101 01010 010 00000 0100011
- 32-bit Instruction Code: 0x0050a023

6. ```lw x5, 0(x10)```

- Instruction Format: I-type
- Binary Encoding: 000000000000 01010 010 00101 0000011
- 32-bit Instruction Code: 0x0000a283

7. ```jal x0, 0x100```

- Instruction Format: J-type
- Binary Encoding: 00000000000100000000 00000 1101111
- 32-bit Instruction Code: 0x0000086f

8. ```beq x1, x2, label```

- Instruction Format: B-type (assuming offset is 0x4)
- Binary Encoding: 000000 00010 00001 000 00010 1100011
- 32-bit Instruction Code: 0x00210063

9. ```bne x1, x3, label```

- Instruction Format: B-type (assuming offset is 0x4)
- Binary Encoding: 000000 00011 00001 001 00010 1100011
- 32-bit Instruction Code: 0x00310063

10.``` slli x5, x1, 1```

- Instruction Format: I-type
- Binary Encoding: 0000000 00001 00101 001 00001 0010011
- 32-bit Instruction Code: 0x00109093

11. ```srli x6, x2, 2```

- Instruction Format: I-type
- Binary Encoding: 0000000 00010 00110 101 00010 0010011
- 32-bit Instruction Code: 0x0022b093

12. ```and x3, x4, x5```

- Instruction Format: R-type
- Binary Encoding: 0000000 00101 00100 111 00011 0110011
- 32-bit Instruction Code: 0x005201b3

13. ```or x2, x3, x4```

- Instruction Format: R-type
- Binary Encoding: 0000000 00100 00011 110 00010 0110011
- 32-bit Instruction Code: 0x004181b3

14. ```sub x3, x5, x2```

- Instruction Format: R-type
- Binary Encoding: 0100000 00010 00101 000 00011 0110011
- 32-bit Instruction Code: 0x402282b3


15. ```xor x1, x2, x3```

- Instruction Format: R-type
- Binary Encoding: 0000000 00011 00010 100 00001 0110011
- 32-bit Instruction Code: 0x003100b3


# TASK 4
## Functional simulation and waveform generation using iverilog and gtkwave on RISC-V Netlist.
### Below are the steps - 

**1. Installation of gtkwave and iverlog**
Firstly we need to install gtkwave and iverilog, to do so run the following commands
```
sudo apt get update
```
```
sudo apt install iverilog gtkwave
```

**2.Clone the Github Repository**

*```since designing of RISC-V is not part of this internship we need to clone the github repository```*

use the following command-
```
git clone https://github.com/vinayrayapati/rv32i
```

**3. Performing simulation**
Now to perform the simulation , change the directory ```cd rv32i```.

And run the following command-

```
iverilog -o iiitb_rv32i iiitb_rv321.v iiitb_32i_tb.v
```
and now to run simulation use 
```
./iiitb_rv32i
```

**4. Waveform Generation**

To view waveform , use
```
gtkwave iiitb_rv32i.vcd
```
This will open the wave form viewer , now add the following signals to view the instructions and output
```
- clk
- EX_MEM_IR[31:0]
- ID_EX_A[31:0]
- ID_EX_B[31:0]
- EX_MEM_ALUOUT[31:0]
```
Now we can start to view the results,

### ADD r1,r2,r3:

![add](https://github.com/user-attachments/assets/a1122752-eeaa-4cce-987a-8da3a727edbb)







### SUB r3,r1,r2:
![sub](https://github.com/user-attachments/assets/4f0d10d2-cc38-4795-81b0-6e7dd86399ec)

### AND r2,r1,r3:
![and](https://github.com/user-attachments/assets/7c52c3ca-d633-462a-acb7-2b07efb19db5)

### OR r8,r2,r5:
![or](https://github.com/user-attachments/assets/7d45ddb1-7fd7-4427-8d48-b40778e833e7)






### SLT r10,r2,r4:

![slt](https://github.com/user-attachments/assets/ae1fce4d-7fd9-47ec-a8c8-b01dc60c0a25)



# TASK 5:

## Implementation of 2 bit comparator using VSDsquadron mini board

## Project Overview

This project implements a 2 bit comparator , which compares two 2 bit values and displays the result using switching on of LED's. The result is calculated on the basis of output calculated using truth table of the 2 bit comparator.

## Components Required

1. VSDsquadron mini board
2. Breadboard
3. jumper wires
4. LED's (red,yellow,green)
5. Resistors(2.2kohm)
6. visual studio
7. Platform io

## Circuit Diagram


![circuit diagram](https://github.com/user-attachments/assets/3fab85a4-78b4-4f0a-807b-6111bd78b64a)



## Pin Connections

| COMPONENT | CONNECTION |
|--------|--------|
| LED| VSDsquadron board |
| LED1 | PIN4(PD4) |
| LED2 | PIN5(PD5) |
| LED3 | PIN6(PD6) | 

## TRUTH TABLE
| A1 | A0 | B1 | B0 | A>B |A=B | A<B |
|--------|--------|--------|--------|--------|--------|--------|
| 0 | 0 | 0 | 0 | 0 | 1 | 0 |
| 0 | 0 | 0 | 1 | 0 | 0 | 1 |
| 0 | 0 | 1 | 0 | 0 | 0 | 1 |
| 0 | 0 | 1 | 1 | 0 | 0 | 1 |
| 0 | 1 | 0 | 0 | 1 | 0 | 0 |
| 0 | 1 | 0 | 1 | 0 | 1 | 0 |
| 0 | 1 | 1 | 0 | 0 | 0 | 1 |
| 0 | 1 | 1 | 1 | 0 | 0 | 1 |
| 1 | 0 | 0 | 0 | 1 | 0 | 0 |
| 1 | 0 | 0 | 1 | 1 | 0 | 0 |
| 1 | 0 | 1 | 0 | 0 | 1 | 0 |
| 1 | 0 | 1 | 1 | 0 | 0 | 1 |
| 1 | 1 | 0 | 0 | 1 | 0 | 0 |
| 1 | 1 | 0 | 1 | 1 | 0 | 0 |
| 1 | 1 | 1 | 0 | 1 | 0 | 0 |
| 1 | 1 | 1 | 1 | 0 | 1 | 0 |



# TASK 6 : Demonstration

## OVERVIEW

This project implements a 2 bit comparator , which compares two 2 bit values and displays the result using switching on of LED's. The result is calculated on the basis of output calculated using truth table of the 2 bit comparator.

## Components Required 
1. VSDsquadron mini board
2. Breadboard
3. jumper wires
4. LED's (red,yellow,green)
5. Resistors(2.2kohm)
6. visual studio
7. Platform io

## CODE :

```
#include <ch32v00x.h>
#include <debug.h>
#include <stdio.h>

#define LED1_PIN GPIO_Pin_4 //yellow LED
#define LED2_PIN GPIO_Pin_5 //red LED
#define LED3_PIN GPIO_Pin_6 //green LED
#define LED_PORT GPIOD

void GPIO_Config(void) {
    // Enable the clock for GPIOD

    RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOD, ENABLE);

    // Configure PD4, PD5, and PD6 as outputs
    GPIO_InitTypeDef GPIO_InitStructure;
    GPIO_InitStructure.GPIO_Pin = LED1_PIN | LED2_PIN | LED3_PIN ;
    GPIO_InitStructure.GPIO_Mode = GPIO_Mode_Out_PP; // Push-pull output
    GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
    GPIO_Init(LED_PORT, &GPIO_InitStructure);
}

void compare_2bit(uint8_t a, uint8_t b) {
    // Clear all LEDs
    GPIO_ResetBits(LED_PORT, LED1_PIN | LED2_PIN | LED3_PIN);

    if (a > b) {
      // Light up LED1 if a > b
        GPIO_SetBits(LED_PORT, LED1_PIN);
    } else if (a == b) {
        // Light up LED2 if a == b
        GPIO_SetBits(LED_PORT, LED2_PIN);
    } else {
        // Light up LED3 if a < b
        GPIO_SetBits(LED_PORT, LED3_PIN);
    }  
    
}  

int main(void) {   
    NVIC_PriorityGroupConfig(NVIC_PriorityGroup_1);
    SystemCoreClockUpdate();
    Delay_Init();
    // Initialize the GPIO for the LEDs
    GPIO_Config();


    // Main loop to iterate over all possible 2-bit numbers  
     for (uint8_t a = 0; a <= 3; a++) {
        for (uint8_t b = 0; b <= 3; b++) {
            compare_2bit(a, b);
            Delay_Ms(5000); // Delay for visualization
        }
    }
    
    return 0;
}


```

## Project Image:

![20241115_233126](https://github.com/user-attachments/assets/9cefd4dd-f80b-4fff-8250-9ed871c4dfa6)

## Demonstration






































   


























