# 🏙️ Thermal Management Systems for Urban Air Mobility (UAM) eVTOLs

## ✈️ Project Overview
This project simulates thermal management strategies for **next-generation electric Vertical Take-Off and Landing (eVTOL)** aircraft used in **Urban Air Mobility (UAM)**. 

The repository contains **two distinct simulation models** developed in **MATLAB/Simulink**:
1.  **Centralized Liquid Cooling System:** For high-power avionics and flight control computers.
2.  **Localized Environmental Control System (ECS):** For sensitive optical sensors (LiDAR).

**Note:** These models use synthetic heat loads and mathematical representations of components to validate thermal control logic under civilian aviation standards (NASA/SAE). No physical hardware or restricted sensor data was used.

---

# 🔹 Module A: Centralized Liquid Cooling System
**Target:** Avionics, Cockpit Display, Flight Control Computer (FCC).

## 🌡️ System Architecture  
This module simulates an active **liquid-based cooling loop** (Ethylene Glycol 60% / Water 40%) designed to manage high-heat-flux components distributed across the aircraft.

### Subsystems Modeled
*   **Avionics Loop:** Cools navigation sensors (GNSS, IMU) using a cold plate interface.
*   **Cockpit Loop:** Regulates cabin electronics temperature for pilot/passenger safety.
*   **FCC Loop:** Ensures thermal stability of primary flight computers.

### Control Logic
*   **Ideal Set-point:** 25 °C.
*   **Mechanism:** PI Controllers dynamically adjust flow valves based on real-time temperature feedback.
*   **Active Thermal Management:**
    *   **Heating:** Inline heater activates if $T_{liquid} < 15^\circ C$ (Cold start/High altitude).
    *   **Cooling:** Radiator fan activates if any component $T > 35^\circ C$.

### 🖼️ System Diagram (Centralized Loop)
<img width="1475" height="724" alt="CTMS Architecture" src="https://github.com/user-attachments/assets/3241bdc9-281b-4bcc-ae6f-de3cfbfcc9ff" />

---

# 🔹 Module B: LiDAR Environmental Control System (ECS)
**Target:** LiDAR Pod (Obstacle Detection Sensor).

## 📡 System Architecture
Unlike the centralized liquid loop, the LiDAR sensor requires a **localized, hybrid cooling solution** due to its placement in an external pod. This model simulates a **solid-state cooling and air-ventilation system** (No liquid loop).

### 🔧 Physics Modeled
The Simulink model represents the LiDAR as a **mathematical heat source** enclosed in a Carbon Fiber/Polymer Foam pod.

*   **Cooling Mechanism:**
    *   **Cold Plate:** Passive conduction interface.
    *   **Thermoelectric Cooler (TEC):** Active Peltier cooling for rapid heat reduction.
    *   **Heatsink & Air Vents:** Forced air convection to dissipate heat to the ambient environment.
*   **Heating Mechanism:**
    *   **Kapton Film Heaters:** Simulated to activate to prevent lens fogging in cold conditions (< 5 °C).

### 🖼️ Simulation Model (LiDAR)
<img width="1123" height="612" alt="Screenshot 2025-12-10 205019" src="https://github.com/user-attachments/assets/50b12e1b-8f07-4876-a5ed-25deaa64dcbc" />

*Figure 1: Simulink block diagram showing the interaction between the TEC, Heatsink, and Air Vents logic.*

---

## 📈 Simulation Results

### 1. Centralized Liquid Loop Results
**Scenario:** Standard Urban Flight Profile (Ambient 25 °C).
- **Cockpit Display:** Cooled from **39 °C → 31 °C** (Stabilized).
- **Flight Control Computer:** Cooled from **37 °C → 28 °C** (Optimal).
- **Avionics Module:** Warmed from **10 °C → 24 °C** (Cold-start protection).

<img width="686" height="452" alt="Simulation Graph" src="https://github.com/user-attachments/assets/04319118-0bf3-44b1-91ee-95385b04f4ec" />

### 2. LiDAR ECS Results
**Scenario:** Extreme Heat Day Operation.
*   **Initial Condition:** Sensor initialized at **45 °C** (Ambient 45 °C).
*   **Target Operational Range:** 20 °C – 40 °C.
*   **Performance:**
    *   The TEC and Vents activated immediately upon initialization.
    *   Heat was successfully dissipated via the heatsink.
    *   **Final Temperature:** Stabilized at **34–35 °C**.

<img width="698" height="519" alt="Screenshot 2025-12-10 205104" src="https://github.com/user-attachments/assets/f77a241d-17f4-4249-b073-e9bbd2c13d54" />

*Figure 2: Scope result showing LiDAR pod temperature dropping from 45°C to a safe 34°C.*

---

## 🧩 Technical Capabilities 

This repository demonstrates proficiency in:
- **MATLAB/Simulink:** creating custom thermal plants and logical control loops.
- **Heat Transfer Physics:** Modeling conduction (cold plates), convection (radiators/vents), and radiation.
- **Control Theory:** Tuning PI controllers for thermal lag compensation.
- **Civilian Safety Standards:** Adhering to temperature limits defined for commercial avionics.

---

## 🧾 References  
- **NASA**: eVTOL Power and Thermal Management Studies.  
- **SAE ARP1256**: Aircraft Environmental Control Systems (Civilian Standard).
