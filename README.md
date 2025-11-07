# 🛩️ eVTOL Centralized Thermal Management System

## Overview  
This project models a **Centralized Thermal Management System (CTMS)** for **Electric Vertical Take-Off and Landing (eVTOL)** aircraft.  
The system maintains optimal operating temperatures across avionics, cockpit, and flight-control computers using a **liquid-based cooling and heating loop**.  

It combines **temperature feedback**, **PI (Proportional-Integral) control**, and **active thermal regulation** to ensure component reliability and efficiency during flight.

---

## 🌡️ System Architecture  

The CTMS consists of **three primary subsystems**, each connected to a shared coolant loop using an **ethylene glycol–water mixture (60:40)**.

### 1. Avionics Cooling Loop  
- Includes sensors for flight dynamics (GNSS receiver, IMU, barometer).  
- Uses a cold plate connected to the main loop.  
- Temperature monitored via `temperature_avionics` feedback.

### 2. Cockpit Cooling Loop  
- Regulates cockpit display and electronics.  
- Controlled via a dedicated cold plate and `PI Valve (Cockpit)`.

### 3. Flight Control Computer (FCC) Loop  
- Ensures stable operation of flight-critical systems.  
- Uses its own PI valve with feedback from `temperature_FCC`.

---

## 🔧 Working Principle  

### Ideal Temperature Control  
- **Target temperature:** 25 °C  
- Each subsystem compares its current temperature to the ideal set-point.  
- The corresponding **PI Valve** adjusts:  
  - **Cold valve** → opens when temperature > 25 °C  
  - **Hot valve** → opens when temperature < 25 °C  

### Active Heating  
- When **liquid temperature < 15 °C**, the **inline heater** activates.  

### Active Cooling  
- When any subsystem’s **max temperature > 35 °C**, the **radiator fan** turns on for heat dissipation.  

### Coolant Circulation  
- The coolant flows continuously between the reservoir, radiator, cold plates, and PI-controlled valves, ensuring uniform temperature distribution.

---

## 🧠 Control Logic Summary  

| Condition | Action |
|------------|--------|
| `T_liquid < 15 °C` | Inline heater **ON** |
| `T_component > 35 °C` | Radiator fan **ON** |
| `T_component > 25 °C` | Cold valve **opens** |
| `T_component < 25 °C` | Hot valve **opens** |

---

## ⚙️ Components Modeled  

- **Reservoir:** Ethylene glycol (60%) + Water (40%) mixture  
- **Cold plates:** Interface for thermal exchange  
- **PI Controllers:** Independent feedback loops for each subsystem  
- **Sensors:** Temperature feedback for control logic  
- **Radiator & Fan:** Air-based heat rejection  
- **Inline Heater:** Prevents over-cooling in cold ambient conditions  

---

## 🧩 Simulation and Implementation  

This model can be simulated in **MATLAB/Simulink** to study:  
- Temperature stability under variable ambient conditions  
- Dynamic PI-controller response  
- Energy consumption and transient behavior during flight phases


## 📊 Ideal Operating Range  

| Subsystem | Ideal Temp | Safe Range | Cooling Trigger | Heating Trigger |
|------------|-------------|-------------|----------------|----------------|
| Avionics | 25 °C | 20–35 °C | > 35 °C | < 15 °C |
| Cockpit | 25 °C | 20–35 °C | > 35 °C | < 15 °C |
| FCC | 25 °C | 20–35 °C | > 35 °C | < 15 °C |

---

## 🖼️ System Diagram  


<img width="1475" height="724" alt="Screenshot 2025-09-18 172411" src="https://github.com/user-attachments/assets/3241bdc9-281b-4bcc-ae6f-de3cfbfcc9ff" />

---
## 📈 Simulation Results  

**Test Case:** Flight Control System thermal regulation  
**Ambient temperature:** 25 °C (298 K)

- The **cockpit display** cooled from **39 °C → 31 °C**  
- The **flight control computer** cooled from **37 °C → 28 °C**  
- The **avionics module (GNSS, IMU, Barometer)** warmed from **10 °C → 24 °C**  

All systems reached near their **ideal operational range (25–30 °C)** within the simulation period.

<img width="686" height="452" alt="Screenshot 2025-09-18 170447" src="https://github.com/user-attachments/assets/04319118-0bf3-44b1-91ee-95385b04f4ec" />


---
## 🧾 References  

- NASA eVTOL Power and Thermal Management Studies  
- SAE ARP1256: Aircraft Environmental Control Systems  
- MATLAB/Simulink Thermal Modeling Documentation  




