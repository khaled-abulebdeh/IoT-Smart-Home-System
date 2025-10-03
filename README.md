#  IoT Smart Home System

This project is divided into **two parts**:

1. **IoT System on Cisco Packet Tracer** → A simulated IoT smart environment with multiple sensors and actuators connected through a gateway to a cloud server.  
2. **Python Simulation** → A simplified Python implementation that simulates the process with only a fire detector and a sprinkler.

---

## 📑 Table of Contents
- [Part A — Packet Tracer IoT System](#part-a--packet-tracer-iot-system)  
  - [Overview](#overview)  
  - [Sensors and Actions](#sensors-and-actions)  
  - [System Flow](#system-flow)  
  - [Server Configuration](#server-configuration)  
- [Part B — Python Simulation](#part-b--python-simulation)  
  - [Overview](#overview-1)  
  - [How It Works](#how-it-works)  
  - [How to Run](#how-to-run)  
- [Requirements](#requirements)  
- [Contributors](#contributors)  

---

## Part A — Packet Tracer IoT System

### Overview
The IoT system is built in **Cisco Packet Tracer** and demonstrates how sensors and actuators interact with a gateway and cloud server. Sensors generate events, the gateway processes them, and the cloud logs them for monitoring.

### Sensors and Actions
- **Fire Sensor and Smoke Sensor** → Triggers **Sprinkler** when fire is detected.  
- **CO2 Sensor** → Opens **Windows** automatically when CO2 exceeds a threshold.  
- **Motion Sensor** → Enables **Lights** in rooms when motion is detected.  

### System Flow
1. **Sensors** send readouts (fire, smoke, CO2 level, motion detection) to the **Gateway**.  
2. The **Gateway** interprets sensor values and activates actuators (sprinkler, windows, lights).  
3. The **Gateway** also forwards events to the **Cloud Server** for logging and remote monitoring.  

### Server Configuration
- **Cloud server credentials**:  
  - **Username**: `moh`  
  - **Password**: `moh`  
- The cloud server stores and displays events received from the gateway.  

---

## Part B — Python Simulation

### Overview
The Python part provides a **separate simplified implementation** that focuses on simulating the **fire detection process**.  

It demonstrates:
- A **Fire Detector** sending signals.  
- A **Sprinkler** actuator being triggered by the fire signal.  

### How It Works
- The Python script uses simple socket communication to simulate how a sensor sends a fire event to the gateway.  
- When fire is detected (`FIRE ON`), the **Sprinkler** is activated.  
- When fire is cleared (`FIRE OFF`), the **Sprinkler** is deactivated.  

### How to Run
1. Run the **gateway** (included in the Python script).  
2. Run the **fire detector simulation**.  
3. Observe the sprinkler actuator being enabled/disabled based on the detector’s input.  

---

## Requirements
- **Cisco Packet Tracer** (for IoT system simulation).  
- **Python 3.8+** (for Python simulation).  
- Standard Python libraries:  
  - `socket`  
  - `threading`  
  - `time`  
  - `datetime`  

---

## Contributors
- **Khaled Abu Libdeh**
- **Mohammed Shamasnah**
- **Mahmoud Duhaide**
