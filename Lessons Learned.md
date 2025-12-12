## 2. Lessons Learned
Throughout the design and debugging process, several critical technical challenges were encountered. Overcoming these provided valuable insights into digital logic design and simulation nuances.

### A. Component Naming & External Files
* **Issue:** Integrating Verilog files initially caused "Unknown module type" errors despite correct code syntax.
* **Resolution:** It was discovered that the **Label** in the *Digital* component settings must exactly match the `module Name` defined inside the Verilog code.
* **Lesson:** Consistency between the simulation environment's properties and the HDL (Hardware Description Language) code definition is mandatory for successful instantiation.

### B. Parallel ALU & Status Flags
* **Issue:** When performing a Division operation, the "Negative" indicator would sometimes light up incorrectly if the simultaneous Subtraction operation resulted in a negative value.
* **Resolution:** A dedicated **Status Multiplexer** was implemented alongside the Result Multiplexer. This ensures that only the status flags (Negative/Error) of the *selected* operation are forwarded to the LEDs.
* **Lesson:** In a parallel ALU architecture, computing all results simultaneously is efficient, but status flags must be multiplexed just like the data to avoid false positives from non-selected operations.

### C. Reset Logic & Tri-State Buffers
* **Issue:** Attempting to use Tri-State buffers to force a "0" into the Register for resetting caused simulation errors and undefined states.
* **Resolution:** The logic was redesigned to use a **Multiplexer** at the Register input. The 'C' button selects a constant `0` input, while standard operation selects the ALU result.
* **Lesson:** In FPGA and digital simulation contexts, Multiplexers are significantly more stable and predictable than Tri-State logic for routing data paths and reset signals.

### D. 7-Segment Display Blanking
* **Issue:** The standard "Hex Display" component lacks an Enable pin, making it difficult to turn off the display during an error state.
* **Resolution:** A workaround was implemented by using a **Controlled Buffer** on the data line. Cutting the data flow (High-Z) effectively blanks the display.
* **Lesson:** When high-level components lack specific control pins, data-path interruption can serve as an effective alternative control mechanism.

### E. Propagation Delay & Signal Synchronization
* **Issue:** Logic gates introduced a slight propagation delay on one of the input paths to the Register, while the control signal arrived instantly. This timing mismatch (Race Condition) caused the Register to latch incorrect data or glitches before the input logic had fully settled.
* **Resolution:** A manual **Delay Component** was inserted into the faster signal path to compensate for the gate latency. This synchronized the arrival times of both the data and control signals.
* **Lesson:** Even in simulation, logic gates consume time. In asynchronous (event-driven) designs, ensuring "Timing Closure" by balancing signal paths is critical to prevent race conditions and ensure data integrity.