#  IoT Smart Home System

This project simulates an IoT-based fire and safety monitoring system using **two parts**:

1. **Packet Tracer Part** → Cisco Packet Tracer topology with server, sensors (CO2, smoke, fire, motion), and actuators (alarm, sprinkler, lights).  
   - Server **name**: `moh`  
   - Server **password**: `moh`  

2. **Python Simulation Part** → Python scripts that replicate the Packet Tracer behavior (sensors → gateway → cloud).

---

## 📑 Table of Contents
- [Project Description](#project-description)  
- [Part A — Packet Tracer](#part-a--packet-tracer)  
  - [Topology](#topology)  
  - [Configuration Steps](#configuration-steps)  
  - [Protocols / Messages](#protocols--messages)  
  - [Thresholds](#thresholds)  
- [Part B — Python Simulation](#part-b--python-simulation)  
  - [1) cloud_server.py](#1-cloud_serverpy)  
  - [2) gateway.py](#2-gatewaypy)  
  - [3) fire_sensor.py](#3-fire_sensorpy)  
  - [4) smoke_sensor.py](#4-smoke_sensorpy)  
  - [5) co2_sensor.py](#5-co2_sensorpy)  
  - [6) motion_sensor.py](#6-motion_sensorpy)  
  - [7) simulator.py (optional)](#7-simulatorpy-optional)  
  - [How to Run](#how-to-run)  
- [Requirements](#requirements)  
- [Contributors](#contributors)  

---

## 📝 Project Description
This system integrates multiple **IoT sensors** with a **gateway** and a **cloud server** to detect hazards and motion, then trigger responses:

- **CO2 Sensor** → Monitors CO2 concentration; alerts when above threshold (1000 ppm).  
- **Smoke Sensor** → Detects smoke, triggers alarm.  
- **Fire Sensor** → Detects fire, triggers alarm + sprinkler.  
- **Motion Sensor** → Detects motion, enables/disables lights.  

**Actuators**: Alarm, Sprinkler, Lights.  
**Gateway**: Aggregates sensor data, applies thresholds, forwards events to cloud.  
**Cloud Server**: Logs and visualizes events.  

---

## Part A — Packet Tracer

### Topology
- **Edge Layer** (sensors):  
  - Room1: Fire, Smoke, CO2 sensors  
  - Room2: Smoke, Motion sensor  
- **Gateway**: Home router/PC with TCP service.  
- **Cloud Server**: Hostname `moh`, password `moh`.  

### Configuration Steps
- **Network**: `192.168.1.0/24`  
  - Gateway: `192.168.1.1`  
  - Cloud Server: `192.168.1.10`  
  - Room1 Node: `192.168.1.101`  
  - Room2 Node: `192.168.1.102`  

- **Cloud server setup**:  
  - Hostname: `moh`  
  - Password: `moh`  
  - Enable HTTP/TCP listener  

- **Gateway setup**:  
  - TCP listener for sensors  
  - Forwards events to cloud  

### Protocols / Messages
**Sensor → Gateway**:  
- `REGISTER <TYPE> <ID>`  
- `SMOKE ON|OFF`  
- `FIRE ON|OFF`  
- `CO2 <value>`  
- `MOTION <ID> ON|OFF`  

**Gateway → Cloud**:  
- `EVENT|<timestamp>|<sensor_id>|<type>|<value>`  
- `ALERT|<timestamp>|CO2|<value>`  

### Thresholds
- CO2 → 1000 ppm  
- Smoke → ON/OFF  
- Fire → ON/OFF  
- Motion → ON enables lights  

---

## Part B — Python Simulation

Below are the Python files that simulate the Packet Tracer behavior.

### 1) cloud_server.py
```python
# cloud_server.py
import socket, threading, datetime

HOST, PORT = '127.0.0.1', 6000
def handle_client(conn, addr):
    with conn:
        while (data := conn.recv(1024)):
            text = data.decode().strip()
            print(f"[CLOUD] {datetime.datetime.utcnow()} | {addr} | {text}")
            conn.sendall(b"ACK\n")

def main():
    print("[CLOUD] Server started (name=moh,password=moh)")
    s = socket.socket(); s.bind((HOST, PORT)); s.listen(5)
    while True:
        conn, addr = s.accept()
        threading.Thread(target=handle_client, args=(conn, addr), daemon=True).start()

if __name__ == "__main__": main()
