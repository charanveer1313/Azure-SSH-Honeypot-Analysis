# Azure-Based SSH Honeypot Analysis (Cowrie)

A medium-interaction SSH and Telnet honeypot (Cowrie) deployed on Microsoft Azure using Docker. This project is designed to attract, capture, and analyze brute-force attacks and malicious activity in a controlled environment.

## 📋 Features
- **Deception:** Mimics a vulnerable UNIX system to lure attackers.
- **Isolation:** Containerized using Docker to ensure host system security.
- **Logging:** Captures shell interaction, file uploads, and credential-stuffing patterns.
- **Cloud Scale:** Hosted on Azure for 24/7 global visibility.

## 🚀 How to Run

### 1. Prerequisites
Ensure you have the following installed on your Azure VM (Ubuntu recommended):
* Docker
* Docker Compose
* Git

### 2. Azure Configuration
Before deploying, you must configure your **Network Security Group (NSG)**:
1. Open the Azure Portal and navigate to your VM.
2. Go to **Networking** > **Inbound port rules**.
3. Add a rule to allow traffic on ports **2222** (SSH) and **2223** (Telnet).
   * *Note: Keep port 22 restricted to your own IP for secure management.*

### 3. Deployment
Clone this repository and launch the honeypot:
4. Verification

Test the honeypot by attempting to log in from your local machine:

Bash
ssh -p 2222 root@[YOUR_AZURE_VM_IP]
Any credentials entered here will be captured in the logs.

5. Analyzing Attack Logs

The honeypot stores all activity in JSON format. To view the captured data in real-time:

Bash
# Access logs within the container
docker exec -it cowrie tail -f /home/cowrie/cowrie/var/log/cowrie/cowrie.json
```bash
# Clone the repository
git clone [https://github.com/](https://github.com/)[YOUR_USERNAME]/Azure-SSH-Honeypot-Analysis.git
cd Azure-SSH-Honeypot-Analysis

# Build and start the container in detached mode
docker-compose up -d
# View Cowrie JSON logs
docker exec -it cowrie tail -f var/log/cowrie/cowrie.json
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
