# 🖥️ Computer System Architecture – CPU Sim Lab

<p align="center">
  <img src="https://img.shields.io/badge/CPU%20Simulator-CPU%20Sim%204-blue?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Architecture-Mano's%20Basic%20Computer-purple?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Language-Assembly-orange?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Practicals-3--11-green?style=for-the-badge" />
</p>

## 📌 About the Project

This repository contains the practical implementations of **Computer System Architecture (CSA)** using **CPU Sim 4**, based on **Mano's Basic Computer**.

The project explores the fundamental concepts of computer organization, including arithmetic and logical operations, memory-reference instructions, register-reference instructions, data manipulation, and program control.

The practicals demonstrate how a computer processes instructions, performs calculations, transfers data between registers and memory, and executes programs using an assembly-style instruction set.

## 🎯 Objectives

* Understand the architecture of Mano's Basic Computer.
* Learn the working of the Accumulator (AC), E register, Program Counter (PC), Address Register (AR), and Instruction Register (IR).
* Implement arithmetic operations such as addition and subtraction.
* Perform logical operations such as AND, OR, NOT, XOR, NOR, and NAND.
* Understand memory-reference and register-reference instructions.
* Implement conditional skip and branching instructions.
* Perform circular shift operations.
* Develop programs to calculate the sum of integers using loops.
* Understand the fetch, decode, and execute cycle.

## 🛠️ Tools & Technologies

| Tool                        | Purpose                           |
| --------------------------- | --------------------------------- |
| CPU Sim 4                   | CPU architecture simulation       |
| Mano's Basic Computer       | Reference architecture            |
| Assembly-style instructions | Programming the simulated machine |
| GitHub                      | Project hosting and documentation |

## 🧠 Architecture

This project is based on **Mano's Basic Computer**, a model computer architecture used to study the internal working of a CPU.

<details>
<summary><b>Main CPU Components</b></summary>

* **AC (Accumulator):** Stores operands and intermediate arithmetic or logical results.
* **E (Extend):** Stores the carry or extend bit and participates in circular shift operations.
* **PC (Program Counter):** Holds the address of the next instruction.
* **AR (Address Register):** Holds the memory address used by the CPU.
* **IR (Instruction Register):** Holds the current instruction.
* **Memory:** Stores instructions and data.
* **Control Unit:** Coordinates instruction execution and the flow of data.
* **ALU:** Performs arithmetic and logical operations.

</details>

## 📚 Practicals Included

| Practical | Topic                                                                    |
| --------- | ------------------------------------------------------------------------ |
| 03        | Addition of two user-entered numbers                                     |
| 04        | Subtraction of two user-entered numbers                                  |
| 05        | Logical operations: AND, OR, NOT, XOR, NOR, NAND                         |
| 06        | Memory-reference instructions and multiplication using repeated addition |
| 07        | Register-reference instructions: CLA, CMA, CME, HLT                      |
| 08        | Register-reference instructions: INC, SPA, SNA, SZE                      |
| 09        | Register-reference instructions: CIR, CIL                                |
| 10        | Sum of integers until a negative number is entered                       |
| 11        | Sum of integers until zero is entered                                    |

---

# 💻 Practical Implementations

## 🟢 Practical 3: Addition of Two User-Entered Numbers

**Aim:** To write an assembly program that accepts two numbers from the user, adds them, and displays the result.

**Logic:**

$$
SUM = A + B
$$

### Source Code

```asm
INP
STA A
INP
ADD A
STA SUM
OUT
HLT

A:      .data 1 0
SUM:    .data 1 0
```

### Explanation

| Instruction | Description                         |
| ----------- | ----------------------------------- |
| `INP`       | Takes the first number as input     |
| `STA A`     | Stores the first number in memory   |
| `INP`       | Takes the second number             |
| `ADD A`     | Adds the first number to the second |
| `STA SUM`   | Stores the result                   |
| `OUT`       | Displays the sum                    |
| `HLT`       | Stops program execution             |

### Example Output

```text
Input 1: 5
Input 2: 3
Output: 8
```

**Result:** The program successfully adds two user-entered numbers and displays their sum.

---

## 🟢 Practical 4: Subtraction of Two User-Entered Numbers

**Aim:** To subtract two user-entered numbers using the 2's complement method.

**Logic:**

$$
DIFF = A - B = A + (\overline{B}+1)
$$

### Source Code

```asm
INP
STA A
INP
CMA
INC
ADD A
STA DIFF
OUT
HLT

A:      .data 1 0
DIFF:   .data 1 0
```

### Explanation

| Instruction | Description                         |
| ----------- | ----------------------------------- |
| `INP`       | Accepts the minuend A               |
| `STA A`     | Stores A in memory                  |
| `INP`       | Accepts the subtrahend B            |
| `CMA`       | Calculates the 1's complement of B  |
| `INC`       | Adds 1 to obtain the 2's complement |
| `ADD A`     | Adds A to the 2's complement of B   |
| `STA DIFF`  | Stores the difference               |
| `OUT`       | Displays the result                 |
| `HLT`       | Stops execution                     |

### Example Output

```text
Input A: 9
Input B: 4
Output: 5
```

**Result:** The program performs subtraction using the 2's complement method.

---

## 🟢 Practical 5: Logical Operations

**Aim:** To perform AND, OR, NOT, XOR, NOR, and NAND operations on two user-entered numbers.

Mano's Basic Computer provides AND and CMA as fundamental logical instructions. The other operations in this practical are constructed using these instructions and Boolean algebra.

### Source Code

```asm
INP
STA A
INP
STA B

; AND = A . B
LDA A
AND B
STA RAND
OUT

; OR = (A' . B')'
LDA B
CMA
STA NB
LDA A
CMA
STA NA
AND NB
CMA
STA ROR
OUT

; NOT A
LDA NA
OUT

; NOT B
LDA NB
OUT

; XOR = (A + B) . (A . B)'
LDA RAND
CMA
STA RNAND
AND ROR
STA RXOR
OUT

; NOR = (A + B)'
LDA ROR
CMA
STA RNOR
OUT

; NAND = (A . B)'
LDA RNAND
OUT

HLT

A:      .data 1 0
B:      .data 1 0
NA:     .data 1 0
NB:     .data 1 0
RAND:   .data 1 0
ROR:    .data 1 0
RXOR:   .data 1 0
RNOR:   .data 1 0
RNAND:  .data 1 0
```

### Explanation

| Operation | Boolean Expression      | Description                            |
| --------- | ----------------------- | -------------------------------------- |
| AND       | \(A \cdot B\)           | Output is 1 when both bits are 1       |
| OR        | \(A+B\)                 | Output is 1 when at least one bit is 1 |
| NOT A     | \(\overline A\)         | Inverts the bits of A                  |
| NOT B     | \(\overline B\)         | Inverts the bits of B                  |
| XOR       | \(A\oplus B\)           | Output is 1 when the bits differ       |
| NOR       | \(\overline{A+B}\)      | Complement of OR                       |
| NAND      | \(\overline{A\cdot B}\) | Complement of AND                      |

### Example Output

For the inputs:

```text
A = 1100
B = 1010
```

| Operation | Result |
| --------- | ------ |
| AND       | 1000   |
| OR        | 1110   |
| NOT A     | 0011   |
| NOT B     | 0101   |
| XOR       | 0110   |
| NOR       | 0001   |
| NAND      | 0111   |

**Output order:** AND, OR, NOT A, NOT B, XOR, NOR, NAND.

**Result:** The program implements six logical operations using the basic logical instructions of Mano's Basic Computer.

---

## 🟢 Practical 6: Memory-Reference Instructions

**Aim:** To study memory-reference instructions such as ADD, LDA, STA, BUN, and ISZ by implementing multiplication using repeated addition.

**Logic:**

$$
PROD = X \times N
$$

For this program:

$$
PROD = 5 \times 3 = 15
$$

### Source Code

```asm
LOOP:   LDA PROD
        ADD X
        STA PROD
        ISZ CTR
        BUN LOOP
        LDA PROD
        HLT

X:      .data 1 5
CTR:    .data 1 -3
PROD:   .data 1 0
```

### Explanation

| Instruction | Description                                                              |
| ----------- | ------------------------------------------------------------------------ |
| `LDA PROD`  | Loads the current product into AC                                        |
| `ADD X`     | Adds the multiplicand                                                    |
| `STA PROD`  | Stores the updated product                                               |
| `ISZ CTR`   | Increments the counter and skips the next instruction if it becomes zero |
| `BUN LOOP`  | Branches back to the loop                                                |
| `HLT`       | Stops execution                                                          |

The counter is initialized to -3. Each loop increments it by 1. When it reaches zero, `ISZ` skips `BUN LOOP`, terminating the loop.

### Example Output

```text
X = 5
N = 3
Product = 15
```

**Result:** The program multiplies two numbers using repeated addition and memory-reference instructions.

---

## 🟢 Practical 7: Register-Reference Instructions

**Aim:** To implement and observe the register-reference instructions CLA, CMA, CME, and HLT.

### Source Code

```asm
LDA NUM
CLA
CMA
CME
HLT

NUM:    .data 1 25
```

### Explanation

| Instruction | Function      | Operation       |
| ----------- | ------------- | --------------- |
| `LDA`       | Load AC       | AC ← M[NUM]     |
| `CLA`       | Clear AC      | AC ← 0          |
| `CMA`       | Complement AC | AC ← AC'        |
| `CME`       | Complement E  | E ← E'          |
| `HLT`       | Halt          | Stops execution |

### Expected Register Changes

| Instruction | AC (Hex) | E |
| ----------- | -------- | - |
| `LDA NUM`   | 0019     | 0 |
| `CLA`       | 0000     | 0 |
| `CMA`       | FFFF     | 0 |
| `CME`       | FFFF     | 1 |
| `HLT`       | FFFF     | 1 |

**Result:** The program demonstrates how register-reference instructions manipulate the accumulator and extend bit.

---

## 🟢 Practical 8: Conditional Skip Instructions

**Aim:** To implement and test INC, SPA, SNA, and SZE register-reference instructions.

### Source Code

```asm
LDA NUM
INC
SNA
HLT

INC
SPA
HLT

SZE
HLT

INC
HLT

NUM:    .data 1 -2
```

### Explanation

| Instruction | Function                                         |
| ----------- | ------------------------------------------------ |
| `INC`       | Increments AC by 1                               |
| `SPA`       | Skips the next instruction if AC is non-negative |
| `SNA`       | Skips the next instruction if AC is negative     |
| `SZE`       | Skips the next instruction if E is zero          |
| `HLT`       | Halts execution                                  |

### Working

1. `LDA NUM` loads -2 into the accumulator.
2. `INC` changes AC from -2 to -1.
3. `SNA` skips the following HLT because AC is negative.
4. The next `INC` changes AC from -1 to 0.
5. `SPA` skips HLT because AC is non-negative.
6. `SZE` skips HLT because E is zero.
7. The final `INC` changes AC from 0 to 1.
8. The final HLT terminates the program.

### Expected Output

```text
Initial AC = -2
After INC  = -1
After INC  =  0
After INC  =  1
Final AC   =  1
```

**Result:** The program demonstrates conditional skipping and program control using register-reference instructions.

---

## 🟢 Practical 9: Circular Shift Instructions

**Aim:** To implement the CIR and CIL instructions and observe the circular movement of bits between the accumulator and E register.

### Source Code

```asm
LDA NUM

CIR
CIR
CIL
CIL

HLT

NUM:    .data 1 9
```

### Explanation

| Instruction | Function                                 |
| ----------- | ---------------------------------------- |
| `CIR`       | Circulates E and AC one bit to the right |
| `CIL`       | Circulates E and AC one bit to the left  |
| `HLT`       | Stops execution                          |

### Working

The initial accumulator value is 9, represented as a 16-bit value:

```text
AC = 0000 0000 0000 1001
E  = 0
```

| Instruction | AC (Binary)         | E |
| ----------- | ------------------- | - |
| Initial     | 0000 0000 0000 1001 | 0 |
| CIR         | 0000 0000 0000 0100 | 1 |
| CIR         | 1000 0000 0000 0010 | 0 |
| CIL         | 0000 0000 0000 0100 | 1 |
| CIL         | 0000 0000 0000 1001 | 0 |

**Result:** The program demonstrates circular right and left shift operations using AC and E.

---

## 🟢 Practical 10: Sum of Integers Until a Negative Number Is Entered

**Aim:** To continuously accept integers from the user and calculate their sum until a negative, non-zero number is entered.

The negative number is not included in the final sum.

### Source Code

```asm
LOOP:   INP
        SPA
        BUN DONE
        ADD SUM
        STA SUM
        BUN LOOP

DONE:   LDA SUM
        OUT
        HLT

SUM:    .data 1 0
```

### Explanation

| Instruction | Description                                      |
| ----------- | ------------------------------------------------ |
| `INP`       | Reads the next integer                           |
| `SPA`       | Skips the next instruction if AC is non-negative |
| `BUN DONE`  | Exits the loop for negative input                |
| `ADD SUM`   | Adds the current number to the running sum       |
| `STA SUM`   | Stores the updated sum                           |
| `BUN LOOP`  | Repeats the input process                        |
| `OUT`       | Displays the final sum                           |
| `HLT`       | Stops execution                                  |

### Example

```text
Input:  2
Input:  3
Input:  4
Input: -1

Output: 9
```

**Result:** The program calculates the sum of non-negative integers until a negative number is entered.

---

## 🟢 Practical 11: Sum of Integers Until Zero Is Entered

**Aim:** To accept integers from the user and calculate their sum until zero is entered.

### Source Code

```asm
LOOP:   INP
        SZA
        BUN ADDIT
        BUN DONE

ADDIT:  ADD SUM
        STA SUM
        BUN LOOP

DONE:   LDA SUM
        OUT
        HLT

SUM:    .data 1 0
```

### Explanation

| Instruction | Description                              |
| ----------- | ---------------------------------------- |
| `INP`       | Reads an integer                         |
| `SZA`       | Skips the next instruction if AC is zero |
| `BUN ADDIT` | Branches to the addition section         |
| `BUN DONE`  | Exits when the input is zero             |
| `ADD SUM`   | Adds the input to the running total      |
| `STA SUM`   | Stores the updated sum                   |
| `BUN LOOP`  | Repeats the process                      |
| `LDA SUM`   | Loads the final sum                      |
| `OUT`       | Displays the result                      |
| `HLT`       | Stops execution                          |

### Example

```text
Input:  5
Input:  3
Input:  2
Input:  0

Output: 10
```

**Result:** The program calculates the sum of user-entered integers until zero is entered.

---

# 🔄 Instruction Execution Cycle

Mano's Basic Computer follows the instruction cycle, which consists of fetching, decoding, and executing instructions.

```text
        ┌─────────────────┐
        │      FETCH      │
        │ Read instruction│
        └────────┬────────┘
                 │
                 ▼
        ┌─────────────────┐
        │      DECODE     │
        │ Interpret opcode│
        └────────┬────────┘
                 │
                 ▼
        ┌─────────────────┐
        │     EXECUTE     │
        │ Perform operation│
        └────────┬────────┘
                 │
                 ▼
        ┌─────────────────┐
        │  STORE / UPDATE │
        │ Update registers│
        │ or memory       │
        └────────┬────────┘
                 │
                 ▼
        ┌─────────────────┐
        │  NEXT INSTRUCTION│
        └─────────────────┘
```

# 📂 Repository Structure

```text
CSA-CPU-Sim/
│
├── README.md
│
├── Practicals/
│   ├── Practical-3-Addition
│   ├── Practical-4-Subtraction
│   ├── Practical-5-Logical-Operations
│   ├── Practical-6-Memory-Reference
│   ├── Practical-7-Register-Reference
│   ├── Practical-8-Skip-Instructions
│   ├── Practical-9-Circular-Shift
│   ├── Practical-10-Sum-Negative-Termination
│   └── Practical-11-Sum-Zero-Termination
│
├── Machine/
│   └── BasicComputer.cpu
│
└── Screenshots/
    ├── Machine-Configuration.png
    ├── Register-Setup.png
    └── Program-Execution.png
```

*This is a suggested folder structure. Rename the files and folders to match your actual repository.*

# 🚀 How to Run

1. Install and launch CPU Sim 4.
2. Open the `BasicComputer.cpu` machine configuration, if included.
3. Select the required practical program.
4. Load the program into the simulator.
5. Enter the input values when prompted.
6. Execute the instructions using the simulator.
7. Observe the changes in AC, E, PC, AR, IR, and memory.
8. Verify the final result.

# 📖 Learning Outcomes

By completing these practicals, I explored:

* The internal architecture of Mano's Basic Computer.
* Register organization and data transfer.
* Binary arithmetic and 2's complement subtraction.
* Boolean algebra and logical operations.
* Memory-reference and register-reference instructions.
* Conditional skip instructions and branching.
* Circular shift operations using AC and E.
* Loop construction using BUN and ISZ.
* Input/output operations and program termination.
* CPU instruction execution and simulation using CPU Sim 4.

# 🎓 Conclusion

This project provides practical experience with **Computer System Architecture using CPU Sim 4**. Through these practicals, the fundamental operations of Mano's Basic Computer are explored, including arithmetic, logical, memory-reference, and register-reference instructions.

The programs demonstrate how a processor handles data, executes instructions, manages memory, and performs iterative calculations. The project helps bridge the gap between theoretical concepts of computer organization and their practical implementation through simulation.

# 👨‍💻 Author

**Khushal Khadiya**
Computer Science Student
Computer System Architecture – CPU Sim Lab

---

⭐ If you find this repository useful for learning computer architecture, consider giving it a star!
