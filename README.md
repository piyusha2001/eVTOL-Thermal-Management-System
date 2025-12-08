# 🏙️ Thermal Management System for Urban Air Mobility (UAM) eVTOLs

## ✈️ Project Overview
This project models a **Centralized Thermal Management System (CTMS)** specifically designed for **next-generation electric Vertical Take-Off and Landing (eVTOL)** aircraft used in **Urban Air Mobility (UAM)**. 

As commercial electric air taxis move towards certification for city-based operations, managing heat dissipation in high-density avionics and flight computers is a critical safety challenge. This project simulates an active **liquid-based cooling loop** to ensure operational reliability during high-stress flight phases common in urban logistics and passenger transport.

---

## 🎯 Key Objectives
*   **Civilian Safety Compliance:** Maintain critical flight hardware within safe operating temperatures defined by civilian aviation standards (NASA/SAE).
*   **Efficiency for Urban Range:** Optimize the cooling loop to minimize power draw, extending the range of commercial electric aircraft.
*   **System Reliability:** Use **PI (Proportional-Integral) control** to dynamically regulate temperatures for avionics, cockpit electronics, and flight control systems.

---

## 🌡️ System Architecture  

The model simulates a thermal architecture for a commercial eVTOL, consisting of **three primary subsystems** connected to a shared coolant loop (Ethylene Glycol 60% / Water 40%).

### 1. Avionics Cooling Loop (Navigation & Safety)
- Cools standard commercial navigation sensors (GNSS receiver, IMU, barometer).  
- Uses a cold plate interface connected to the main loop.  
- Temperature monitored via `temperature_avionics` feedback.

### 2. Cockpit Cooling Loop (Pilot/Passenger Interface)
- Regulates the temperature for the cockpit display and cabin electronics to ensure pilot/passenger safety.  
- Controlled via a dedicated cold plate and `PI Valve (Cockpit)`.

### 3. Flight Control Computer (FCC) Loop  
- Ensures stable operation of the primary flight computers during autonomous hovering and transition phases.  
- Uses its own PI valve with feedback from `temperature_FCC`.

---

## 🔧 Working Principle  

### Ideal Temperature Control  
- **Target set-point:** 25 °C (Optimal for electronics longevity).  
- Each subsystem continuously compares its real-time temperature to the set-point.  
- The **PI Controller** dynamically adjusts flow:  
  - **Cold valve** → Opens when T > 25 °C  
  - **Hot valve** → Opens when T < 25 °C  

### Active Thermal Management  
- **Pre-Heating:** When **liquid temperature < 15 °C**, the **inline heater** activates (crucial for high-altitude or winter urban operations).  
- **Active Cooling:** When any subsystem’s **max temperature > 35 °C**, the **radiator fan** activates for rapid heat rejection.  

---

## 🧠 Control Logic Summary  

| Condition | Action | Safety Purpose |
|------------|--------|----------------|
| `T_liquid < 15 °C` | Inline heater **ON** | Prevent component freezing/lag |
| `T_component > 35 °C` | Radiator fan **ON** | Prevent thermal runaway |
| `T_component > 25 °C` | Cold valve **opens** | Maintain nominal operation |
| `T_component < 25 °C` | Hot valve **opens** | Optimize energy efficiency |

---

## ⚙️ Components Modeled  

- **Reservoir:** Ethylene glycol (60%) + Water (40%) mixture (Standard aviation coolant)  
- **Cold plates:** Interface for thermal exchange  
- **PI Controllers:** Independent feedback loops for precise regulation  
- **Sensors:** Temperature feedback for safety logic  
- **Radiator & Fan:** Air-based heat rejection system  
- **Inline Heater:** Environmental control for cold-start scenarios  

---

## 🧩 Simulation Capabilities 

This model is implemented in **MATLAB/Simulink** to analyze:  
- **Thermal Stability:** Response to variable ambient temperatures in city environments.  
- **Controller Tuning:** Dynamic response of PI controllers to sudden load changes.  
- **Energy Efficiency:** Power consumption of the cooling system during a standard urban mission profile.

---

## 📊 Ideal Operating Range  

| Subsystem | Ideal Temp | Safe Range | Cooling Trigger | Heating Trigger |
|------------|-------------|-------------|----------------|----------------|
| Avionics | 25 °C | 20–35 °C | > 35 °C | < 15 °C |
| Cockpit | 25 °C | 20–35 °C | > 35 °C | < 15 °C |
| FCC | 25 °C | 20–35 °C | > 35 °C | < 15 °C |

---

## 🖼️ System Diagram  

<img width="1475" height="724" alt="CTMS Architecture" src="https://github.com/user-attachments/assets/3241bdc9-281b-4bcc-ae6f-de3cfbfcc9ff" />

---

## 📈 Simulation Results  

**Test Case:** Thermal regulation during a simulated flight profile.  
**Ambient Condition:** 25 °C (Standard Day).

- **Cockpit Display:** Cooled from **39 °C → 31 °C** (Stabilized).
- **Flight Control Computer:** Cooled from **37 °C → 28 °C** (Optimal).
- **Avionics Module:** Warmed from **10 °C → 24 °C** (Cold-start protection).

All systems stabilized within the **civilian operational safety range (25–30 °C)**.

<img width="686" height="452" alt="Simulation Graph" src="https://github.com/user-attachments/assets/04319118-0bf3-44b1-91ee-95385b04f4ec" />

---

## 🧾 References  

- **NASA**: eVTOL Power and Thermal Management Studies.  
- **SAE ARP1256**: Aircraft Environmental Control Systems (Civilian Standard).  
- **MATLAB/Simulink**: Thermal Modeling Documentation.
