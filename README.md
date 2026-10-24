# drag-race-timing-system
A digital logic timing circuit simulated in NI Multisim and prototyped on a physical breadboard. This system is engineered to replicate a drag strip's sequential traffic light ("Christmas Tree") and timer electrical system.

## Detailed Circuit Operation & Logic Breakdown

To validate the timing system's functionality, the circuit architecture is divided into three core subsystems: the clock generator, the sequential control logic, and the display drivers.

### 1. The Clock Base (555 Timer)
* **Operation:** A **555 timer IC** is configured in **Astable mode** to serve as the master system clock. 
* **Validation Metric:** The values of resistors R1, R2 and capacitor C1 were specifically calculated and tuned to output a precise 10Hz square wave (0.1-second pules). This ensures the run-time counter registers increments at exact tenth-of-a-second intervals.

### 2. Sequential Control Logic (74LS76 Flip-Flops & Logic Gates)
* **Operation:** The staging light sequence (the "Christmas Tree") is driven by a synchronous state machine utilizing **74LS76 JK Flip-Flops**. 
* **The Sequence:** When the manual start switch (S2) is toggled, the clock pulses step the circuit through sequential states: Pre-Stage LED → Stage LED → Green Light (Go).
* **Interlocking Protection:** An **AND-gate logic matrix (74LS08)** acts as a safety interlock. The binary counter subsystem is strictly held at zero until the state machine safely registers the final "Green Light" state, preventing premature timing triggers.

### 3. High-Speed Counter & Display Driver (7493 & 7447 ICs)
* **Operation:** Once the Green Light state is active, the 10Hz clock signal is routed directly into a chain of **7493 4-Bit Binary Counters**. 
* **BCD Conversion:** The raw binary output from the counters is fed directly into **7447 BCD-to-7-Segment Decoder/Drivers**, which handle the active-low current required to display digits on the dual-digit display panel.
* **Global Reset:** Toggling the master reset switch (S3) sends an immediate clear pulse to the 7493 counter pins and forces the JK flip-flops back to their initial standby state, cleanly wiping the system memory for the next race.


## Schematic & Simulation Architecture
Below is the validated design schematic modeled within NI Multisim to verify state propagation and clock signal intervals before hardware procurement.

![NI Multisim Circuit Schematic Diagram](https://github.com/user-attachments/assets/632fa4c6-32f1-4a5e-ab46-862c56fb5f3d)

## Troubleshooting & Debugging

During the physical breadboarding phase, the circuit did not function perfectly on the first initialization. A hardware validation process utilizing a digital logic probe was executed to isolate and resolve the following root causes:

### 1. Signal Tracing & Node Correction (The Reset Mechanism)
* **The Problem:** The global reset switch failed to zero out the counter displays or hold the sequential states reliably.
* **The Diagnostic Process:** Used a digital logic probe to trace the voltage state transition when the switch was compressed. 
* **The Root Cause:** Discovered the capacitor was tied to the incorrect side of the logic junction, filtering out the brief high-to-low transition pulse required by the clear pins.
* **The Fix:** Re-routed the capacitor node relative to the junction according to the validated Multisim blueprint, establishing a clean, reliable clearing signal.

### 2. Component Failure Isolation (Defective 7400-Series Logic Gates)
* **The Problem:** The staging logic refused to step forward sequentially, staying stuck on a fixed standby state despite receiving an active clock pulse from the 555 timer.
* **The Diagnostic Process:** Probed the input pins of the basic 7400-series logic gate ICs to confirm the signal was arriving, then checked the corresponding output pins. 
* **The Root Cause:** The input signals were valid, but the output pins remained stagnant, isolating internal gate damage within one of the standard logic gate packages.
* **The Fix:** Swapped out the defective basic 7400 IC with a fresh unit and re-validated the output states, restoring sequential operation.

### 3. Point-to-Point Wiring Verification
* **The Problem:** Weird timing behavior occurred due to cross-wiring lines on the dense breadboard layout.
* **The Root Cause:** Minor point-to-point wiring mismatches between the basic logic gate outputs and the downstream counter inputs.
* **The Fix:** Used a logic probe to trace the signal paths step-by-step against the IC datasheets, correcting the physical layout mismatches to ensure accurate sequential routing.




## Physical Hardware Prototyping & Testing
The system was fully breadboarded using 7400-series discrete TTL logic integrated circuits. Testing was split into stagnant validation states to ensure proper power rail routing and logic transitions.

### Power State OFF:
![Physical Breadboard Assembly - Power State OFF](https://github.com/user-attachments/assets/e5322f28-d125-4758-b357-15b526c6281d)

### Power State ON:
![Physical Breadboard Assembly - Power State ON](https://github.com/user-attachments/assets/6c0e4017-5910-4521-b373-0f441bbd1ca9)

### Full Demonstration:
![Physical Breadboard Assembly - Full Demonstration](https://github.com/user-attachments/assets/c1da6070-af01-4f1d-964e-38e4d15b3793)
