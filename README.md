# ⚡Damn Vulnerable Purdue Model - DVPM.


**A Complete Damn Vulnerable ICS/SCADA Security Testing Environment**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Platform](https://img.shields.io/badge/Platform-Proxmox%20%2B%20Docker-blue)](https://www.proxmox.com/)
[![Status](https://img.shields.io/badge/Status-Active-brightgreen)](https://github.com/KhiemB41/Damn-Vulnerable-Purdue-Model-DVPM)

---

## ⚠️ WARNING

THIS LAB IS INTENTIONALLY INSECURE. PLEASE BE CAREFUL!!!

🚫 DO NOT deploy on any production network

🚫 DO NOT connect to the internet

🚫 For education and authorized security testing ONLY

✅ Always operate in isolated environment

✅ Use snapshots before destructive tests

✅ Reset lab after each session



---

## 📋 Table of Contents

- [Overview](#-overview)
- [Architecture](#-architecture)
- [Quick Start](#-quick-start)
- [Components](#-components)
- [Security Testing](#-security-testing)
- [Documentation](#-documentation)
- [Contributing](#-contributing)
- [License](#-license)

---

## 🎯 Overview

The **Damn-Vulnerable-Purdue-Model (DVPM)** is a comprehensive, intentionally vulnerable industrial control system (ICS) and SCADA security testing environment. Built on the Purdue Enterprise Reference Architecture, it provides a realistic platform for:

- 🛡️ Security research and testing
- 🎯 Penetration testing practice
- 📊 SIEM detection validation
- 🔬 Vulnerability research
- 📚 Security education and training
- ⚠️ IT/OT Security Engineer

### Key Features

| Feature | Description |
|---------|-------------|
| **Purdue Model** | Full implementation of Levels 0-5 |
| **Hybrid Architecture** | Proxmox VMs + Docker containers |
| **Multiple Protocols** | Modbus, DNP3, OPC UA, Profinet |
| **Pre-built Vulnerabilities** | Default creds, no auth, buffer overflows |
| **Complete Monitoring** | Wazuh SIEM + Grafana dashboards |
| **Attack Scenarios** | 15+ documented attack chains |

---

## 🏗️ Architecture

### Purdue Model Implementation

┌─────────────────────────────────────────────────────────────────────────────────┐
│                           LEVEL 4/5 - ENTERPRISE ZONE                           │
│                              (net5: 10.0.5.0/24)                                │
│                                                                                 │
│    ┌─────────────────┐                                                          │
│    │   KALI LINUX    │  IP: 10.0.5.10                                           │
│    │   (PENTEST)     │  GW: 10.0.5.1                                            │
│    └────────┬────────┘                                                          │
│             │                                                                   │
│             │  Attacker attempts to access OT network                           │
│             ▼                                                                   │ 
│    ┌──────────────────────────────────────────────────────────────┐             │
│    │                   IT/OT DMZ (net1: 10.0.1.0/24)              │             │
│    │                                                              │             │
│    │  ┌──────────────────────────────────────────────┐            │             │
│    │  │          pfsense FIREWALL (FW)               │            │             │
│    │  │  WAN: 10.0.5.1 (IT Zone)                     │            │             │
│    │  │  LAN: 10.0.1.1 (DMZ)                         │            │             │
│    │  │  OPT1: 10.0.2.1 (Level 3)                    │            │             │
│    │  │  OPT2: 10.0.3.1 (Level 2)                    │            │             │
│    │  │  OPT3: 10.0.4.1 (Level 1/0)                  │            │             │
│    │  └──────────────────────────────────────────────┘            │             │
│    └──────────────────────────────────────────────────────────────┘             │
│             │                                                                   │
│             │  Firewall Rules enforce strict segmentation                       │
│             ▼                                                                   │
│    ┌──────────────────────────────────────────────────────────────┐             │
│    │                   LEVEL 3 - OPERATIONS                       │             │
│    │                   (net2: 10.0.2.0/24)                        │             │
│    │                                                              │             │
│    │  ┌─────────────────────┐  ┌─────────────────────┐            │             │
│    │  │  ENGINEER STATION   │  │    HISTORIAN        │            │             │
│    │  │  (Ubuntu/Win10)     │  │    (InfluxDB)       │            │             │
│    │  │  IP: 10.0.2.10      │  │    IP: 10.0.2.20    │            │             │
│    │  └─────────────────────┘  └─────────────────────┘            │             │
│    └──────────────────────────────────────────────────────────────┘             │
│             │                                                                   │
│             │  Modbus TCP (Port 502) / OPC UA                                   │
│             ▼                                                                   │
│    ┌──────────────────────────────────────────────────────────────┐             │
│    │                  LEVEL 2 - SUPERVISORY                       │             │
│    │                   (net3: 10.0.3.0/24)                        │             │
│    │                                                              │             │
│    │  ┌─────────────────────┐  ┌─────────────────────┐            │             │
│    │  │   HMI/SCADA         │  │   OPERATOR          │            │             │
│    │  │   (FUXA/ScadaBR)    │  │   (Web Client)      │            │             │
│    │  │   IP: 10.0.3.10     │  │   IP: 10.0.3.11     │            │             │
│    │  └─────────────────────┘  └─────────────────────┘            │             │
│    └──────────────────────────────────────────────────────────────┘             │
│             │                                                                   │
│             │  Modbus TCP / DNP3 / Profinet                                     │
│             ▼                                                                   │
│    ┌──────────────────────────────────────────────────────────────┐             │
│    │              LEVEL 1 - BASIC CONTROL                         │             │
│    │               (net4: 10.0.4.0/24)                            │             │
│    │                                                              │             │
│    │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐           │             │
│    │  │  PLC 1      │  │  PLC 2      │  │  RTU        │           │             │
│    │  │  (OpenPLC)  │  │  (OpenPLC)  │  │  (DNP3)     │           │             │
│    │  │  10.0.4.10  │  │  10.0.4.11  │  │  10.0.4.12  │           │             │
│    │  └─────────────┘  └─────────────┘  └─────────────┘           │             │
│    └──────────────────────────────────────────────────────────────┘             │
│             │                                                                   │
│             │  Digital/Analog I/O                                               │
│             ▼                                                                   │
│    ┌──────────────────────────────────────────────────────────────┐             │
│    │                  LEVEL 0 - PHYSICAL PROCESS                  │             │
│    │               (net4: 10.0.4.0/24)                            │             │
│    │                                                              │             │
│    │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐           │             │
│    │  │  Sensors    │  │  Actuators  │  │  Motors     │           │             │
│    │  │  (Simulated)│  │  (Simulated)│  │  (Simulated)│           │             │
│    │  │  10.0.4.20  │  │  10.0.4.21  │  │  10.0.4.22  │           │             │
│    │  └─────────────┘  └─────────────┘  └─────────────┘           │             │
│    └──────────────────────────────────────────────────────────────┘             │
│                                                                                 │
└─────────────────────────────────────────────────────────────────────────────────┘
