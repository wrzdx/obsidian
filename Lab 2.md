---
tags:
  - 1stYear
---
# What are the main units of the cpu?

- **CU (Control unit)** – retrieves instructions  
- **ALU (Arithmetic-Logic unit)** - executes operations
- **Registers** - store current data
![|300](Pasted%20image%2020241024164108.png)

# What is memory hierarchy? Why do we need it?

The **memory hierarchy** organizes different levels of memory based on their speed and capacity. Closer memory (like registers and cache) is fast and provides quick access to frequently used data, while larger, slower memory (like RAM and storage) holds data that is accessed less frequently. This arrangement optimizes **system performance** by reducing delays in accessing critical data while efficiently managing larger storage needs.
![|300](Pasted%20image%2020241024164748.png)

# For what communication bus is used for?

**Communication bus** is used for data transfer between various components of the computer (CPU, memory, peripherals).

# What registers are used for?

**Registers** are used to temporarily store data, instructions, and memory addresses that are actively being used by the CPU. This allows for quick access during processing, helping the CPU execute operations efficiently without the need to access slower memory types.

# What does the Control Unit?

The **Control Unit (CU)** retrieves instructions from memory, decodes them to determine the required actions, and coordinates the entire process by directing components such as the ALU, registers, and memory to perform the necessary operations. It manages the flow of data and ensures correct instruction execution.

# What does the Arithmetic Logic Unit?

The **Arithmetic Logic Unit (ALU)** performs all arithmetic operations (such as addition, subtraction, multiplication, and division) and logical operations (such as AND, OR, NOT) on the data. It takes inputs from the registers, processes them according to the instructions from the Control Unit, and sends the result back to the registers or memory for further use.

# What System Memory is used for?

**System memory (RAM)** is used for temporarily storing a larger volume of data and instructions that the CPU needs while running programs. Unlike registers, which store small, immediate data for processing, RAM holds the active programs and their data. It provides fast access compared to external storage but is slower than registers and cache, allowing the CPU to quickly retrieve necessary information during program execution. Data in RAM is volatile and gets erased when the system is powered off.

# Which Fundamental Ideas of Computer Architecture do you know?

The **fundamental ideas of computer architecture** include:

1. Memory hierarchy.
2. Design simplification through abstraction.
3. Moore’s law for CPU performance.
4. Performance through parallelism.
5. Performance through pipelining.
6. Performance through speculation.
7. Dependability through redundancy.
8. Optimize for the common case.
9. Finite State Machines (FSM).

These principles guide the design and optimization of computer systems to achieve higher performance, efficiency, and reliability.

# What states the Moores Law?

**Moore’s Law** states that the number of transistors on a microchip doubles approximately every two years, leading to an exponential increase in computational power and performance over time. 

# What is a Moore's Law stagnation? Why does it happen?

**Moore's Law stagnation** happens because further increases in CPU performance are limited by issues like excessive heat generation and the fundamental limit of signal transmission speed, which is bound by the speed of light. These factors make it harder to keep improving processor speeds at the same pace.

# What does Performance via Parallelism mean?

**Performance via Parallelism** means improving the performance of a system by executing multiple operations or instructions simultaneously. Instead of performing tasks one after the other, parallelism allows multiple tasks to run at the same time, using multiple processors or cores, which leads to faster overall execution and better system efficiency.

# What is the major problem with it?

The major problem with **parallelism** is **synchronization and data consistency**. When multiple processes or threads run simultaneously, coordinating them to ensure they work together correctly and accessing shared data without conflicts becomes challenging.

# What does Performance via Pipelining mean?

**Performance via Pipelining** means improving system performance by dividing tasks or instructions into smaller stages, where each stage processes a different part of the task simultaneously. In a CPU, pipelining allows multiple instructions to be processed at different stages of execution (fetch, decode, execute) at the same time, increasing throughput and overall efficiency.

# What Pipeline steps do you remember?

1. **IF:** Instruction Fetch 
2. **ID:** Instruction Decode 
3. **EX:** Execution 
4. **MEM:** Memory access (optional stage) 
5. **WB:** register Write Back

# What is the clock cycle?

A **clock cycle** is the basic time unit used by the CPU to synchronize and coordinate all its operations. During each clock cycle, the CPU can perform basic tasks like fetching an instruction, decoding it, executing an operation, or transferring data.

# What does Performance via Prediction mean?

**Performance via Prediction** refers to techniques that improve CPU performance by guessing the flow of program execution. This includes **branch prediction** to pre-fetch instructions and **speculative execution** to run instructions ahead of time based on these guesses. By doing so, processors reduce delays and increase efficiency.

# What does Dependability via redundancy mean?

**Dependability via Redundancy** means enhancing system reliability by including additional components or systems that can assist in case of failure.

# What is the finite state machine?

A **Finite State Machine (FSM)** is a computational model that represents a system with a finite number of states and transitions between those states based on inputs. It consists of defined states, rules for transitioning between states, an initial state, and potentially final states. FSMs are commonly used in applications like digital circuit design, control systems, and software modeling to manage system behavior.

