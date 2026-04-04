# Azure-SSH-Honeypot-Analysis
A cloud-based SSH honeypot deployed on Azure using Docker to analyze automated brute-force attack patterns.
Architecture: "Ubuntu VM on Azure -> Docker Container -> Cowrie."

Findings: Captured 50,000+ logs,
identified a Belgian-based botnet targeting 'solana' credentials.
Tools Used: grep, jq, traceroute, GeoIP.
# Azure-Based SSH Honeypot Analysis (Cowrie)

## Project Overview
This project involved deploying a medium-interaction SSH/Telnet honeypot (Cowrie) within a Dockerized environment on an Azure Virtual Machine. The goal was to analyze real-world automated brute-force attack patterns and gather threat intelligence on targeted credential stuffing.

## 🏗️ Technical Architecture
* **Cloud Provider:** Microsoft Azure (Ubuntu 20.04 LTS)
* **Containerization:** Docker (Isolated Environment)
* **Honeypot:** Cowrie (Configured to listen on port 2222)
* **Networking:** Azure Network Security Group (NSG) configured to forward traffic from Port 22 to the container.

## 📊 Key Findings
* **Total Logs Captured:** [50,000+]
* **Targeted Credentials:** Significant spike in `solana/solana` attempts, indicating botnets specifically targeting blockchain infrastructure.
* **Geographic Origin:** High volume of traffic originating from Hosting/Cloud providers (notably Google LLC) in Europe (Brussels).
* **Attacker Behavior:** Identified "Low and Slow" scanning patterns with an average session duration of 1.7 seconds, confirming high-speed automation.

## 🛠️ Tools Used
* **Linux CLI:** `grep`, `awk`, `tail` for real-time monitoring.
* **JSON Processing:** `jq` for parsing complex Cowrie event logs.
* **Networking:** `traceroute` and `whois` for origin verification and latency analysis.
* **Security:** HASSH fingerprinting for attacker software identification.
