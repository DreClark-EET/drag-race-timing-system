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

![NI Multisim Circuit Schematic Diagram](https://github.com/user-attachments/assets/47d306d0-9c20-4bf0-b7e9-b3623b154b56)

---

## Physical Hardware Prototyping & Testing
The system was fully breadboarded using 7400-series discrete TTL logic integrated circuits. Testing was split into stagnant validation states to ensure proper power rail routing and logic transitions.

### Hardware Stagnant Power State:
![Physical Breadboard Assembly - System Powered Off](https://github.com/user-attachments/assets/04edfeef-bcc9-4c6d-8f6d-74df7aa9c03f)

### Active Sequential State Testing:
![Physical Breadboard Assembly - System Powered On and Counting](https://github.com/user-attachments/assets/aae33fa9-410d-4b6a-8a48-5da96c8ee18e)
