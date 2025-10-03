# 🔥 IoT Fire & Safety Monitoring System

This project simulates an IoT-based fire and safety monitoring system using **two parts**:

1. **Packet Tracer Part** → Cisco Packet Tracer topology with sensors (CO2, smoke, fire, motion), actuators (alarm, sprinkler, lights), and a cloud server.  
   - Server **name**: `moh`  
   - Server **password**: `moh`  

2. **Python Simulation Part** → A set of Python scripts that replicate the Packet Tracer behavior (sensors → gateway → cloud).

---

## 📑 Table of Contents
- [Project Description](#project-description)  
- [Part A — Packet Tracer](#part-a--packet-tracer)  
  - [Topology](#topology)  
  - [Configuration Steps](#configuration-steps)  
  - [Protocols / Messages](#protocols--messages)  
  - [Thresholds](#thresholds)  
- [Part B — Python Simulation](#part-b--python-simulation)  
  - [Files](#files)  
  - [How to Run](#how-to-run)  
  - [Example Output](#example-output)  
- [Requirements](#requirements)  
- [Contributors](#contributors)  

---

## 📝 Project Description
This project combines **IoT hardware simulation in Packet Tracer** with a **software simulation in Python**. The system integrates four types of sensors and triggers corresponding actuators, while also sending event logs to a central cloud server.

- **CO2 Sensor** → Monitors CO2 concentration and alerts when above threshold (1000 ppm).  
- **Smoke Sensor** → Detects smoke, triggers local alarm.  
- **Fire Sensor** → Detects fire, triggers alarm + sprinkler.  
- **Motion Sensor** → Detects human presence, enables/disables lights.  

**Actuators**: Alarm, Sprinkler, Lights.  
**Gateway**: Aggregates data from sensors, applies thresholds, and forwards events to the cloud.  
**Cloud Server**: Logs, visualizes, and acknowledges events.  

---

## Part A — Packet Tracer

### Topology
- **Edge Layer** (two rooms):
  - Room1: Fire, Smoke, CO2 sensors  
  - Room2: Smoke, Motion sensor  
- **Gateway**: Home router/PC configured as TCP server.  
- **Cloud Server**: Hostname `moh`, password `moh`.  

### Configuration Steps
- **Network Setup**:
  - Subnet: `192.168.1.0/24`  
  - Gateway: `192.168.1.1`  
  - Cloud Server: `192.168.1.10` (`moh` / `moh`)  
  - Room1 Node: `192.168.1.101`  
  - Room2 Node: `192.168.1.102`  

- **Cloud Server**:
  - Hostname: `moh`  
  - Password: `moh`  
  - Enable TCP/HTTP services for event logging  

- **Gateway**:
  - TCP listener for sensors  
  - Forwards events to cloud  

### Protocols / Messages
- **Sensor → Gateway**:
  - `REGISTER <TYPE> <ID>`  
  - `SMOKE ON|OFF`  
  - `FIRE ON|OFF`  
  - `CO2 <value>`  
  - `MOTION <ID> ON|OFF`  

- **Gateway → Cloud**:
  - `EVENT|<timestamp>|<sensor_id>|<type>|<value>`  
  - `ALERT|<timestamp>|CO2|<value>`  

### Thresholds
- CO2: 1000 ppm  
- Smoke: binary (ON/OFF)  
- Fire: binary (ON/OFF)  
- Motion: ON enables lights  

---

## Part B — Python Simulation

The Python part simulates the Packet Tracer setup with **socket programming**. It consists of a cloud server, a gateway, and four sensors.

### Files
- `cloud_server.py` → Cloud that logs events.  
- `gateway.py` → Manages sensors/actuators, forwards data to cloud.  
- `fire_sensor.py` → Fire sensor simulation.  
- `smoke_sensor.py` → Smoke sensor simulation.  
- `co2_sensor.py` → CO2 sensor simulation.  
- `motion_sensor.py` → Motion sensor simulation.  
- `simulator.py` → Automates sensor events for testing.  

### How to Run
1. Start cloud:
   ```bash
   python cloud_server.py
