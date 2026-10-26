# 17S-Cyberspace-Operations-Lab

# Hybrid Enterprise SIEM & Endpoint Telemetry Lab

## 🔬 Overview
This repository documents the design, deployment, and operational testing of a local, hybrid enterprise security monitoring lab built on Apple Silicon (macOS) hardware. 

The lab implements a containerized Security Information and Event Management (SIEM) and Extended Detection and Response (XDR) platform (Wazuh) communicating with virtualized Linux endpoint agents across an isolated virtual network sandbox. It was designed to demonstrate practical defensive cyber operations, security event correlation, real-time log ingestion, and adversary activity detection.

---

## 🏗️ Architecture & Network Topology

| Component | Technical Specification / Configuration |
| :--- | :--- |
| **Host System** | Apple MacBook Air M4 (macOS) |
| **Container Engine** | Docker Desktop (Rosetta 2 Emulation enabled) |
| **SIEM / XDR Platform** | Wazuh 4.x Stack (Manager, Indexer, Dashboard) hosted via Docker |
| **Target Endpoint** | Ubuntu Server ARM64 Virtual Machine (`Ubuntu-Target-VM`) in VirtualBox |
| **Virtual Sandbox Network**| Isolated Host-Only Network (`192.168.56.0/24`) |
| **Host Gateway IP** | `192.168.56.1` |
| **Target Endpoint IP** | Dynamic allocation within `192.168.56.0/24` subnet |

---

## ⚙️ Engineering & Deployment Steps

### 1. Network & Virtual Environment Provisioning
* Established an isolated Host-Only network adapter in Oracle VM VirtualBox (`192.168.56.0/24`) to sandbox guest-to-host telemetry traffic without exposing services externally.
* Adjusted host kernel memory mapping requirements for the Wazuh Elasticsearch/Indexer engine:
  ```bash
  sysctl -w vm.max_map_count=262144
2. SIEM Platform Deployment
Deployed single-node Wazuh SIEM containers using Docker Compose on the host system.
Verified native host dashboard accessibility at https://localhost.
3. Endpoint Agent Enrollment
Provisioned the Ubuntu-Target-VM ARM64 endpoint attached to the Host-Only network.
Downloaded and registered the native Linux Debian agent package (.deb aarch64) pointed to host manager IP 192.168.56.1.
Enabled and initialized the agent service (wazuh-agent.service).
🎯 Threat Simulation & Real-Time Detection
To validate end-to-end telemetry ingestion and rule correlation, an authentication attack scenario was executed against the target endpoint:
Target Tactic: Simulated Brute Force / Unauthorized Access Attempt (Mapped to MITRE ATT&CK T1110 - Brute Force).
Execution: Enabled openssh-server on the Ubuntu target and generated unauthorized login attempts with invalid credentials:ssh invaliduser@localhost


Telemetry Path: Local auth logs (/var/log/auth.log) \rightarrow Wazuh Agent \rightarrow Encrypted Transport \rightarrow Wazuh Manager \rightarrow Real-Time Correlation Engine.
📸 Technical Evidence & Verification
1. Endpoint Agent Active Connection
Wazuh agent successfully enrolled and active on Ubuntu-Target-VM.
2. SIEM Threat Detection & Event Parsing
Real-time SSH authentication failure ingested and surfaced under Wazuh Threat Hunting Events dashboard.
🚀 Key Takeaways & Skills Demonstrated
Defensive Cyber Operations: Practical experience deploying enterprise-grade SIEM/XDR architecture and telemetry agents.
Log Analysis & Correlation: Verification of event log paths (/var/log/auth.log) and rule-based alert triggering.
Virtualization & Systems Engineering: Troubleshooting cross-architecture hardware emulation (Apple Silicon / ARM64 vs x86) and virtual network sandboxing.

## 📸 Evidence & Screenshots
<img width="1710" height="1107" alt="Screenshot 2026-10-25 at 7 30 55 PM" src="https://github.com/user-attachments/assets/f4d00b3a-c2ec-4ca1-a52d-a77bb3f11e9d" /> 
<img width="1710" height="1107" alt="Screenshot 2026-10-25 at 7 41 06 PM" src="https://github.com/user-attachments/assets/7e59375d-028f-403c-86a8-83e7f6bca3f4" />
