# drag-race-timing-system
A digital logic timing circuit simulated in NI Multisim and prototyped on a physical breadboard.

## 📐 Schematic & Simulation Architecture
Below is the validated design schematic modeled within NI Multisim to verify state propagation and clock signal intervals before hardware procurement.

![NI Multisim Circuit Schematic Diagram](<img width="664" height="622" alt="DragRaceTimingMultisimDiagram" src="https://github.com/user-attachments/assets/47d306d0-9c20-4bf0-b7e9-b3623b154b56" />)

---

## 🔬 Physical Hardware Prototyping & Testing
The system was fully breadboarded using 7400-series discrete TTL logic integrated circuits. Testing was split into stagnant validation states to ensure proper power rail routing and logic transitions.

### Hardware Stagnant Power State:
![Physical Breadboard Assembly - System Powered Off](<img width="4032" height="3024" alt="BreadboardCircuitOff" src="https://github.com/user-attachments/assets/04edfeef-bcc9-4c6d-8f6d-74df7aa9c03f" />)

### Active Sequential State Testing:
![Physical Breadboard Assembly - System Powered On and Counting](<img width="4032" height="3024" alt="BreadboardCircuitOnAndCounting" src="https://github.com/user-attachments/assets/aae33fa9-410d-4b6a-8a48-5da96c8ee18e" />)
