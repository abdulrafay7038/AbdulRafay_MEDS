### Summary of Lecture 4

---

#### 1. **Sequential Logic and Finite State Machines (FSMs)**

- **Sequential circuits** differ from combinational circuits by having **memory**; outputs depend on both **current inputs and past states**.
- A **state machine** is a discrete-time, stateful system with:
  - A **finite number of states**, inputs, and outputs.
  - Defined **state transitions** based on inputs.
  - **Outputs** determined by current state (Moore machine) or state and inputs (Mealy machine).

- The design of FSMs involves three key components:
  - **State Register**: Holds the current state.
  - **Next State Logic**: Determines the next state based on current state and inputs.
  - **Output Logic**: Produces outputs based on the current state (and possibly inputs).

- The **D flip-flop** is a fundamental building block for state registers:
  - It is **edge-triggered** (captures input at clock rising edge).
  - Unlike a **transparent latch**, it prevents undesired output changes during the clock cycle.
  - Typically constructed with two latches in series.

- **State Register implementation**:
  - Multiple D flip-flops in parallel store multi-bit state.
  - Flip-flops are more transistor-heavy than simple memory elements (e.g., 34 transistors per flip-flop vs. 1 for DRAM cell).

- **Types of FSMs**:
  - **Moore Machine**: Output depends solely on the current state.
  - **Mealy Machine**: Output depends on current state and inputs.
  - Moore machines generally have simpler output logic but potentially more states.

---

#### 2. **Example: Smart Traffic Light Controller FSM**

- Two roads (Avenue A and Boulevard B), each with traffic sensors (1-bit inputs).
- Traffic lights have three states: **Red, Yellow, Green** (Swiss style).
- State can change every 5 seconds, but if traffic is detected on the green light avenue, the state remains unchanged (leading to fairness issues).
- The FSM has **four states**, represented as:

| State | Avenue A Light | Boulevard B Light | Description                     |
|-------|----------------|-------------------|--------------------------------|
| S0    | Green          | Red               | Initial/reset state             |
| S1    | Yellow         | Red               | Transition from A to B          |
| S2    | Red            | Green             | B has green                    |
| S3    | Red            | Yellow            | Transition from B to A          |

- The FSM is **Moore type**: outputs depend only on state.
- The state transition and output logic were converted into truth tables and simplified Boolean expressions using sum-of-products and logic minimization techniques.
- Encoding states with two bits ($S_1 S_0$) allows efficient hardware implementation.

---

#### 3. **Timing and Delays in FSMs**

- The clock cycle must be long enough to accommodate:
  - **Combinational logic delay** (next state and output logic).
  - **Flip-flop setup and hold times**.
- Too short clock cycles lead to incorrect state transitions or outputs.
- Timing diagrams illustrate state transitions, input changes, and reset behavior (asynchronous reset affects state immediately, independent of clock).

---

#### 4. **State and Output Encoding**

- **State Encoding Methods**:

| Encoding Type         | Description                                             | Pros                                  | Cons                                  |
|-----------------------|---------------------------------------------------------|-------------------------------------|--------------------------------------|
| **Binary (Fully Encoded)** | Uses minimum bits ($\log_2 N$ for $N$ states)           | Minimizes flip-flops                 | Can increase complexity of next state logic |
| **One-Hot Encoding**  | One bit per state, only one bit is high at a time        | Simplifies next state logic; easy to automate | Maximizes number of flip-flops        |
| **Output Encoding**   | Output values encoded directly into state bits (for Moore machines) | Minimizes output logic                | Limits flexibility; more complex next state logic |

- Designer must balance trade-offs based on design goals and constraints.

---

#### 5. **Moore vs. Mealy FSM Example: The "Smiling Snail"**

- Problem: Model a snail's brain that outputs a smile when it detects the sequence **1101**.
- Moore FSM: Output depends only on reaching a particular state after seeing the sequence.
- Mealy FSM: Output depends on current state and input, potentially reducing the number of states.
- Trade-off: Mealy FSM can have fewer states but more complex output logic.

---

#### 6. **Hierarchical FSM Design and Concurrency**

- Complex hardware systems comprise many concurrent FSMs interacting.
- Example: Different FSMs control instruction decoding, execution, accelerators, memory, etc.
- Hierarchical FSM design aids manageability, avoiding a monolithic FSM.

---

#### 7. **Introduction to FPGA and Hardware Description Languages (HDLs)**

- **FPGA (Field Programmable Gate Array)**:
  - A reconfigurable hardware platform with:
    - **Lookup Tables (LUTs)**: Small memory blocks implementing logic functions.
    - **Switch Boxes**: Configurable interconnections.
    - **Flip-flops**, memories, and specialized hardware blocks (e.g., multipliers).
  - Advantages: High performance, energy efficiency, reusability, low development cost.
  - Disadvantages: Less power efficient and slower than custom ASICs; considerable area and latency overhead.

- Modern systems combine CPUs, GPUs, FPGAs, and specialized accelerators for performance and flexibility.

- **Lab Overview**:
  - Students program FPGA boards using Verilog HDL and CAT (Computer-Aided-Tools).
  - Labs progress from simple combinational circuits to a 32-bit microprocessor.
  - Emphasis on design, simulation, debugging, and performance analysis.

---
#### 8. **Verilog Hardware Description Language (HDL) Basics**

- Verilog modules define hardware blocks with ports (inputs/outputs).
- Supports multi-bit signals and hierarchical design.

**Example module syntax:**

```verilog
module module_name (port_list);
    input  [n:0] a, b, c;
    output y;

    // functionality description

endmodule
```

#### 9. **Motivation for Using HDLs**

- Modern chips contain billions to trillions of transistors.
- Manual transistor-level design is infeasible.
- HDLs abstract hardware design into manageable, reusable modules.
- Hardware concurrency and timing are naturally expressed in HDLs.

---

### Key Insights

- **Sequential logic design requires careful handling of state memory elements and timing constraints.**
- **Finite State Machines provide a structured approach to modeling sequential systems with clear state, input, and output relationships.**
- **Trade-offs in FSM design include state encoding methods and output dependency (Moore vs. Mealy).**
- **FPGA technology provides a flexible platform for implementing complex hardware designs using LUTs and configurable interconnects.**
- **Hardware Description Languages like Verilog are essential for specifying, simulating, and synthesizing hardware designs efficiently.**

---

### Quantitative Data Table: Flip-Flop Transistor Count vs. DRAM Cell

| Component       | Number of Transistors | Notes                        |
|-----------------|----------------------|------------------------------|
| D Flip-Flop     | 34                   | Built from NAND gates + inverter |
| DRAM Cell       | 1                    | Single transistor memory cell |

---

### Timeline of Lecture Topics Covered

| Time Range         | Topic Covered                                        |
|--------------------|----------------------------------------------------|
| 00:00 - 00:10      | Review of sequential logic, latches, and flip-flops |
| 00:10 - 00:20      | FSM design principles, example traffic light FSM    |
| 00:20 - 00:30      | State encoding, output logic, timing considerations  |
| 00:30 - 00:40      | Moore vs Mealy FSMs, snail brain FSM example         |
| 00:40 - 00:50      | Introduction to FPGA architecture and lab logistics  |
| 00:50 - 01:00      | Lab exercises and FPGA programming overview          |
| 01:00 - 01:15      | Introduction to Verilog HDL and hardware concurrency |

---

