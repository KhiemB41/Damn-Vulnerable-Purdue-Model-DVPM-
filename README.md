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

The **Damn Vulnerable Purdue Model (DVPM)** is a comprehensive, intentionally vulnerable industrial control system (ICS) and SCADA security testing environment. Built on the Purdue Enterprise Reference Architecture, it provides a realistic platform for:

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
| **Hybrid Architecture** | Proxmox VMs/Virtualbox + Docker containers |
| **Multiple Protocols** | Modbus, DNP3, OPC UA, Profinet |
| **Pre-built Vulnerabilities** | Default creds, no auth, buffer overflows |
| **Complete Monitoring** | Wazuh SIEM + Grafana dashboards |
| **Attack Scenarios** | 15+ documented attack chains |

---

## 🏗️ Architecture

### Purdue Model Implementation

Level 4/5: Enterprise Zone: Kali Linux VM (Penetration testing)

            
Level 3.5: IT/OT DMZ:
            - pfSense Firewall
            - Wazuh SIEM
            
            
Level 3: Operations Management:
            - Windows Engineer VM
            - Historian (InfluxDB/Grafana)
            
            
Level 2: Supervisory Control:FUXA SCADA/HMI (Docker)

            
Level 1: Basic Control:
            - PLC1 - OpenPLC (Water Pump)
            - PLC2 - OpenPLC (Valve Control)
            - RTU - DNP3 Server
            
Level 0: Physical Process: Field Device Simulator


### Network Diagram

