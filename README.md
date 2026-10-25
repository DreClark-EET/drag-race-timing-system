# drag-race-timing-system
A digital logic timing circuit simulated in NI Multisim and prototyped on a physical breadboard. This system is designed to replicate a drag strip's sequential traffic light ("Christmas Tree") and timer electrical system.

## Detailed Circuit Operation & Logic Breakdown

To validate the timing system's functionality, the circuit architecture is divided into three core subsystems: the clock generator, the sequential control logic, and the display drivers.

### 1. The Clock Base (555 Timer)
* **Operation:** A **555 timer IC** is configured in **Astable mode** to serve as the master system clock. 
* **Validation Metric:** The values of resistors R1, R2 and capacitor C1 were specifically calculated and tuned to output a precise 10Hz square wave (0.1-second pules). This ensures the run-time counter registers increments at exact tenth-of-a-second intervals.

### 2. Sequential Control Logic (74LS76 Flip-Flops , 74LS93 Counters, & Logic Gates)
* **Operation:** The staging light sequence (the "Christmas Tree") is driven by a synchronous state machine utilizing **74LS76 JK Flip-Flops** into a **74LS93 Ripple Counter**. 
* **The Sequence:** When the manual start switch (S2) is toggled, the clock pulses step the circuit through sequential states: Red LED (Ready) → Yellow (Set) LED → Green Light (Go).
* **Gated Clock & State Transition:** A **74LS08 AND gates'** inputs are selected so that when the **74LS93 Ripple Counter** reaches count 6 the **AND Gate** sends a 1 to the clock input of the main **74LS76 Flip-Flop** causing its Q outputs to flip and simultaneously stopping the lighting sequence while turning on the green LED & starting the stopwatch timing system. 

### 3. High-Speed Counter & Display Driver (74LS93 Counters & 74LS47 Decoders)
* **Operation:** Once the Green Light state is active, the 10Hz clock signal is routed directly into a chain of **7493 4-Bit Binary Counters**. 
* **BCD Conversion:** The raw binary output from the counters is fed directly into **7447 BCD-to-7-Segment Decoder/Drivers**, which handle the active-low current required to display digits on the dual-digit display.
* **Global Reset:** Toggling the master reset switch (S3) sends an immediate clear pulse to the 7493 counter pins and forces the JK flip-flops back to their initial standby state, cleanly wiping the system memory for the next race. This same system also allows for a **Power-On Reset** Signal.


## Schematic & Simulation Architecture
Below is the validated design schematic modeled within NI Multisim to verify state propagation and clock signal intervals before hardware procurement.

![NI Multisim Circuit Schematic Diagram](https://github.com/user-attachments/assets/632fa4c6-32f1-4a5e-ab46-862c56fb5f3d)

## Troubleshooting & Debugging

During the physical breadboarding phase, the circuit did not function perfectly on the first try. A hardware validation process utilizing a digital logic probe was executed to isolate and resolve the following root causes:

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
The validated schematic was brought to life on a physical breadboard using 7400-series TTL ICs, a 555 timer, indicator LEDs, and 7-segment display modules. Testing started with an unpowered powered state to moving to a initial power on state, and concluded with a real-time race sequence run.

### Power State OFF:
![Physical Breadboard Assembly - Power State OFF](https://github.com/user-attachments/assets/e5322f28-d125-4758-b357-15b526c6281d)
> *Initial layout verification ensuring clean wire routing, correct IC pin orientation, and proper decoupling capacitor placement across power rails before applying VCC.*

### Power State ON:
![Physical Breadboard Assembly - Power State ON](https://github.com/user-attachments/assets/6c0e4017-5910-4521-b373-0f441bbd1ca9)
> *Applying 5V power to verify standby bias levels. The initial state correctly holds the Red "Ready" LED lit while keeping the 7493 counters reset and the 7-segment displays at zero.*

### Full Demonstration:
![Physical Breadboard Assembly - Full Demonstration](https://github.com/user-attachments/assets/c1da6070-af01-4f1d-964e-38e4d15b3793)
> *Full hardware demonstration showing the start switch trigger, automatic progression through the LEDs, state transition gating via the 74LS08 AND gate, live 10Hz timing on the 7-segment displays & the master reset.*
> -*(Sped Up Slightly)*-
