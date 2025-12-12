# Design Assumptions & Implementation Details

**Project:** 16-Bit Calculator
**Date:** 10.12.2025

## 1. System Architecture & Timing
* **Event-Driven Design:** Instead of a global continuous clock signal, the system operates on an asynchronous, **event-driven architecture**. The physical act of pressing a key on the keyboard generates a trigger signal. This signal acts as a pseudo-clock pulse to drive registers and state transitions.
* **Subcircuit Strategy:** Although hierarchical subcircuits were initially considered, a **flat design structure** was retained to maintain transparency. Logical blocks are visually grouped and demarcated using labeled rectangles for clarity rather than encapsulation.

## 2. Logic & State Management
* **State Memory (RS Latches):** RS Latches are extensively used as the primary memory units for control logic. They are responsible for storing the state of:
    * The selected mathematical operation (+, -, *, /).
    * The calculation status (whether `=` has been pressed).
    * Display visibility (ON/OFF states).
    * Flag indicators (Negative sign and Error status).
    * Operand sequencing (Tracking whether the system is currently inputting Operand 1 or Operand 2).
* **Data Storage:** Standard 16-bit **Registers** are utilized to store the numerical values of Operand 1 and Operand 2.
* **Direct Calculation Prevention:** Directly pressing the `=` key without entering a value for the second operand no longer results in a calculation with the second operand being considered as zero. The system now requires at least a manual entry of `0` for the second operand before pressing `=`.

## 3. Arithmetic Logic Unit (ALU)
* **Hybrid Implementation:** The arithmetic logic uses a combination of built-in components and hardware description language:
    * **Addition & Subtraction:** Implemented using the standard arithmetic units provided by the *Digital* simulation software.
    * **Multiplication & Division:** Implemented using custom **Verilog modules** to ensure precise handling of signed integers and overflow/error boundaries.

## 4. Input & Output Processing
* **Input Encoding:** A **Priority Encoder** is employed to map the distinct input signals from keyboard keys (0, 1, ... 9) into binary values for processing.
* **Output Formatting (Binary to BCD):** To display the 16-bit binary results as human-readable decimal numbers, a custom conversion logic was implemented. The system separates digits by applying sequential **division operations by 1000, 100, and 10** to isolate specific decimal places.
* **Display Component:** The **"Seven-Segment Hex Display"** component was chosen over raw 7-segment distinct LEDs due to its ease of integration and simplified wiring for 4-bit groups.

## 5. Aesthetics & User Interface
* **Color Scheme:** The visual design follows a high-contrast, stylized theme:
    * **Displays:** Configured to **"Matrix Green"** for high visibility.
    * **Buttons & Controls:** Configured to **"Eva-01 Purple"** (inspired by *Neon Genesis Evangelion*).
* **Viewing Recommendation:** The circuit topology and color palette are optimized for **Dark Mode**. It is recommended to view the simulation with a dark background for the best visual experience.