# 17S-Cyberspace-Operations-Lab
# Hybrid Enterprise SIEM & Endpoint Telemetry Lab

## 🔬 Project Overview
A local enterprise security lab built to simulate threat detection, log ingestion, and SIEM/XDR monitoring on an Apple Silicon (macOS) host infrastructure. Designed to practice defensive cyber operations, security event correlation, and telemetry analysis.

## 🏗️ Architecture & Network Topology
- **Host Engine:** MacBook Air M4 (macOS) running Docker Desktop with Rosetta emulation.
- **SIEM / XDR:** Wazuh 4.x Server deployed via Docker containers on the host.
- **Endpoint Target:** VirtualBox Ubuntu ARM64 Virtual Machine (`Ubuntu-Target-VM`).
- **Network Segmentation:** Isolated VirtualBox Host-Only network (`192.168.56.0/24`) routing traffic between guest telemetry agents and the host gateway (`192.168.56.1`).

## ⚙️ Implementation Steps
1. Configured a secure Host-Only network adapter sandbox in VirtualBox.
2. Deployed containerized Wazuh Manager and Dashboard with custom indexer resource parameters (`vm.max_map_count=262144`).
3. Provisioned and registered an ARM64 native Wazuh agent on the Ubuntu target endpoint via Debian package (`.deb`).

## 🎯 Threat Simulation & Detection
- **Attacker Tactic:** Simulated brute-force login attempts / unauthorized access (MITRE ATT&CK **T1110 - Brute Force**).
- **Telemetry Ingestion:** Monitored real-time authentication logs (`/var/log/auth.log`).
- **SIEM Validation:** Confirmed live rule matching, severity scoring, and alert generation on the Wazuh Dashboard.

## 📸 Evidence & Screenshots
