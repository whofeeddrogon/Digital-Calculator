## Summary of Results
The 16-bit signed integer calculator project was successfully designed, simulated, and verified using the *Digital* software. The final system meets all design requirements and constraints outlined in the project specifications.

Key achievements include:
* **Functional Accuracy:** The system correctly performs Addition, Subtraction, Multiplication, and Division on signed 16-bit integers. It adheres strictly to the 4-digit decimal display limit (-9999 to +9999).
* **Hybrid Implementation Success:** The integration of custom Verilog modules for complex arithmetic (Multiplication/Division) alongside standard logic gates proved highly effective. This allowed for precise handling of signed integers and boundary checks without excessive wiring complexity.
* **Robust Error Handling:** The system successfully identifies and handles edge cases:
    * **Overflow:** Inputs or results exceeding $\pm9999$ trigger the overflow indicator.
    * **Divide-by-Zero:** Attempting to divide by zero triggers the Error LED and blanks the main display to prevent undefined behavior.
* **Event-Driven Efficiency:** The decision to utilize an event-driven architecture (using key presses as clock pulses) resulted in a responsive system without the need for a continuous clock signal, simulating a low-power design approach.
* **User Interface:** The visual hierarchy, established through "Eva-01 Purple" controls and "Matrix Green" displays, provides clear feedback. The custom "Binary-to-BCD" logic using sequential dividers ensures accurate decimal representation on the Hex displays.