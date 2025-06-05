

## 1. Overview

This project details the construction and observation of a simple crystal oscillator circuit designed to generate a clock signal around 16 MHz. The oscillator is built using a 16.000 MHz crystal, a 74HC04 hex inverter IC from Texas Instrument , and a few passive components. The circuit was assembled and tested on a standard solderless breadboard.

The primary aim was to create a basic "raw" crystal oscillator. The observed output waveform, captured via an oscilloscope, is functional in terms of frequency generation but exhibits significant noise and distortion, appearing more like a noisy, somewhat square-like wave rather than a clean sine or square wave.

## 2. Circuit Diagram
![20250605_124948](https://github.com/user-attachments/assets/16740898-de9c-4abd-9757-19122195a5fd)

The oscillator circuit is based on a Pierce oscillator configuration, utilizing two inverter gates from a 74HC04 IC.




**Key components as shown in the diagram:**
*   **Crystal (XTAL):** 16.000 MHz (This is the primary frequency-determining element)
*   **Capacitors (C1, C2):** 2 x 22 pF (picofarad). These are connected from each leg of the crystal to ground, forming the load capacitance.
*   **Resistor (R1):** 1 kΩ. This resistor is in series with the crystal, typically on the path to the input of the first inverter.
*   **Resistor (R2):** 100 kΩ. This is a feedback resistor for the first inverter, connected between its input and output to bias it into its linear operating region.
*   **IC (U1):** 74HC04 Hex Inverter.
    *   The first inverter gate (with R2) forms the core of the oscillator.
    *   The second inverter gate is used as an output buffer to shape and drive the output signal.

## 3. Components List

*   **1x Crystal:** 16.000 MHz
*   **1x 74HC04 Hex Inverter IC** (Note: only two of the six available inverter gates are used in this circuit)
*   **Resistors:**
    *   1x 1 kΩ
    *   1x 100 kΩ
*   **Capacitors:**
    *   2x 22 pF
*   **Solderless Breadboard**
*   **Jumper Wires**
*   **Power Supply** (e.g., 5V for the 74HC04)

## 4. Circuit Explanation

The circuit operates as a Pierce oscillator:

1.  **Inverter as Amplifier:** The first gate of the 74HC04 hex inverter is configured to act as an inverting amplifier. The 100 kΩ feedback resistor (R2) biases the inverter into its active (linear) region, allowing it to provide the necessary gain for oscillation.
2.  **Resonant Network:** The 16 MHz crystal, along with the two 22 pF load capacitors (C1 and C2), forms a pi-network. This network acts as a resonant tank circuit, providing a 180-degree phase shift at or very near the crystal's series resonant frequency. The inverter itself provides another 180-degree phase shift.
3.  **Oscillation Condition:** For sustained oscillation (as per the Barkhausen stability criterion), the total phase shift around the feedback loop must be 360 degrees (or an integer multiple of 360 degrees), and the loop gain must be at least unity at the oscillation frequency. The crystal's high Q-factor ensures frequency stability.
4.  **Series Resistor (R1):** The 1 kΩ resistor (R1) in series with the crystal helps to:
    *   Limit the drive level to the crystal, preventing it from being overdriven and potentially damaged.
    *   Improve the stability of the oscillator by damping unwanted oscillation modes.
5.  **Output Buffer:** The output from the first inverter (the oscillator core) is fed into a second inverter gate from the same 74HC04 IC. This second inverter serves as a buffer, which:
    *   Isolates the oscillator stage from the load, preventing changes in load from affecting the oscillator's frequency or stability.
    *   Sharpens the edges of the waveform, making it more suitable as a digital clock signal.
    *   Provides increased drive capability for the output.

## 5. Breadboard Implementation

The circuit was prototyped on a standard solderless breadboard.

![20250605_124301](https://github.com/user-attachments/assets/1d7c9dec-46e0-4816-902e-2bd88cf523e7)


## 6. Observed Output & Performance


![20250605_124247](https://github.com/user-attachments/assets/279d6b0f-461d-47e7-9486-1f8e40255fa5)


The output of the oscillator was observed using a Hantek DSO2D15 digital storage oscilloscope.



**Key Oscilloscope Readings:**
*   **Frequency:** Approximately **16.13 MHz**. This is close to the nominal 16.000 MHz of the crystal.
*   **Waveform Shape:** The output signal is not a clean sine wave or a perfect square wave. It appears as a somewhat distorted square-like wave with noticeable noise, ringing, or irregularities.
*   **Peak-to-Peak Voltage (PKPK):** Approximately **9.84 V**.
*   **Duty Cycle:** Approximately **64.19%**.

**Notes on Performance:**
*   The feedback loop, utilizing the 100 kΩ resistor, was described as potentially "kind of weak," though the circuit does oscillate.
*   The output signal is quite noisy. Attempts were made to clean up the signal using various filtering components (ferrite beads, inductors, bulk capacitors, small capacitors). However, these efforts reportedly did not improve the signal quality and, in some cases, made it worse. This is a common issue with high-frequency circuits on breadboards due to parasitic capacitances and inductances.

## 7. Known Issues and Limitations

*   **Noisy Output:** The most significant issue is the high level of noise and distortion in the output waveform.
*   **Breadboard Parasitics:** Solderless breadboards are not ideal for high-frequency circuits due to inherent stray capacitance, inductance, and poor grounding, which can lead to signal integrity problems.
*   **Unsuccessful Filtering:** Standard passive filtering techniques attempted did not yield improvements to the waveform.

## 8. Conclusion

This project successfully demonstrates the operation of a basic 16 MHz crystal oscillator using a 74HC04 hex inverter. The circuit generates a signal at the expected frequency range. However, the output quality is compromised by noise and distortion, characteristic of "raw" oscillator outputs on breadboard setups. This README documents the circuit as built and its observed performance, including its imperfections.

## 9. Potential Future Work

*   **PCB Implementation:** Transferring the circuit to a properly designed Printed Circuit Board (PCB) with good layout practices (e.g., short traces, ground plane) would likely significantly reduce noise and improve signal integrity.
*   **Component Value Tuning:** Experiment with different values for the feedback resistor (R2), series resistor (R1), and load capacitors (C1, C2) to observe their impact on waveform shape, stability, and startup time.
*   **Advanced Filtering/Shaping:** Investigate more sophisticated output filtering or Schmitt trigger buffering to achieve a cleaner square wave output.
*   **Noise Source Analysis:** Further investigation to pinpoint the exact sources of noise in the current setup.
