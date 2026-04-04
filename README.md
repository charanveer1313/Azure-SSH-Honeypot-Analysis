# Azure-SSH-Honeypot-Analysis 🛡️

A medium-interaction SSH and Telnet honeypot (Cowrie) deployed on Microsoft Azure using Docker. This project serves as deception technology to analyze brute-force attack patterns and capture malicious behavior in a secure, isolated environment.

## 📋 Features
* **Deception:** Mimics a vulnerable UNIX system to lure attackers.
* **Isolation:** Containerized using Docker to ensure host system security.
* **Logging:** Captures shell interaction, file uploads, and credential-stuffing patterns.
* **Cloud Scale:** Hosted on Azure for 24/7 global visibility.

---

## 🏗️ Technical Architecture
* **Cloud Provider:** Microsoft Azure (Ubuntu 20.04 LTS)
* **Containerization:** Docker (Isolated Environment)
* **Honeypot:** Cowrie (Configured to listen on port 2222)
* **Analysis Tools:** Linux CLI (`grep`, `jq`) for log parsing.

---

## 🚀 How to Run

### 1. Prerequisites
Ensure you have the following installed on your Azure VM:
* Docker & Docker Compose
* Git

### 2. Azure Configuration
Configure your **Network Security Group (NSG)** in the Azure Portal:
1.  Navigate to your VM > **Networking** > **Inbound port rules**.
2.  Add a rule to allow traffic on ports **2222** (SSH) and **2223** (Telnet).
3.  **Important:** Keep port 22 restricted to your own IP to maintain secure access to the actual host.

### 3. Deployment
```bash
# Clone the repository
git clone [https://github.com/charanveer13/Azure-SSH-Honeypot-Analysis.git](https://github.com/charanveer13/Azure-SSH-Honeypot-Analysis.git)
cd Azure-SSH-Honeypot-Analysis

# Build and start the container in detached mode
docker-compose up -d
4. Verification

Test the honeypot by attempting to log in from your local machine:

Bash
ssh -p 2222 root@[YOUR_AZURE_VM_IP]
Note: Any credentials entered during this session will be captured in the logs.

5. Analyzing Attack Logs

The honeypot stores all activity in JSON format. To view the captured data in real-time:

Bash
docker exec -it cowrie tail -f /home/cowrie/cowrie/var/log/cowrie/cowrie.json
📊 Findings & Insights
During the initial deployment, the following patterns were observed:

Brute-Force Activity: High frequency of login attempts within minutes of the ports being opened.

Targeted Credentials: Significant targeting of "root" and "admin" accounts, along with specialized ecosystem keywords like "Solana."

🛠️ Built With
Cowrie - The Honeypot software.

Docker - Containerization.

Azure - Cloud Infrastructure.

Disclaimer: This project is for educational and research purposes only. Always comply with cloud provider terms of service when deploying security research tools.* **Geographic Origin:** High volume of traffic originating from Hosting/Cloud providers (notably Google LLC) in Europe (Brussels).
* **Attacker Behavior:** Identified "Low and Slow" scanning patterns with an average session duration of 1.7 seconds, confirming high-speed automation.

## 🛠️ Tools Used
* **Linux CLI:** `grep`, `awk`, `tail` for real-time monitoring.
* **JSON Processing:** `jq` for parsing complex Cowrie event logs.
* **Networking:** `traceroute` and `whois` for origin verification and latency analysis.
* **Security:** HASSH fingerprinting for attacker software identification.
