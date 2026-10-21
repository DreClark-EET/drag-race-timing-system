# drag-race-timing-system
A digital logic timing circuit simulated in NI Multisim and prototyped on a physical breadboard.

## 📐 Schematic & Simulation Architecture
Below is the validated design schematic modeled within NI Multisim to verify state propagation and clock signal intervals before hardware procurement.

![NI Multisim Circuit Schematic Diagram](<img width="664" height="622" alt="DragRaceTimingMultisimDiagram" src="https://github.com/user-attachments/assets/886fc918-b331-43ee-aa9a-8621d11579f3" />)

---

## 🔬 Physical Hardware Prototyping & Testing
The system was fully breadboarded using 7400-series discrete TTL logic integrated circuits. Testing was split into stagnant validation states to ensure proper power rail routing and logic transitions.

### Hardware Stagnant Power State:
![Physical Breadboard Assembly - System Powered Off](<img width="4032" height="3024" alt="BreadboardCircuitOff" src="https://github.com/user-attachments/assets/72cafddb-64b6-4077-987a-2f0a9c338749" />)

### Active Sequential State Testing:
![Physical Breadboard Assembly - System Powered On and Counting](<img width="4032" height="3024" alt="BreadboardCircuitOnAndCounting" src="https://github.com/user-attachments/assets/167cafbf-fc12-4223-8eb4-a4048f8b561e" />)
