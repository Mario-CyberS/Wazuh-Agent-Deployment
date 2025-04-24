# Wazuh Agents Setup & Configuration  
This project provides step-by-step instructions for deploying and configuring **Wazuh agents** on endpoint machines and managing agent connections to the Wazuh Manager. It also covers agent removal using the CLI.

---

## 🎯 Objective  
To deploy Wazuh agents to Linux endpoints, ensure proper communication with the Wazuh Manager, and manage agents via the Web UI or command-line interface.

---

## 🔍 Why Wazuh Agents?  
**Wazuh agents** are lightweight programs installed on endpoints (servers, desktops, etc.) that send system, security, and file integrity data to the central Wazuh Manager for analysis.

They are crucial for:
- Collecting endpoint logs
- Enabling file integrity monitoring (FIM)
- Providing real-time alerting for SOC teams
- Centralized visibility across an organization

---

## 📚 Skills Learned  
- Installing agents via Web UI instructions  
- Running agent-side configuration scripts  
- Verifying agent-to-manager communication  
- Managing and removing agents via the CLI  
- Troubleshooting firewall-related agent connection issues

---

## 🛠️ Tools Used  
<div>
  <img src="https://img.shields.io/badge/-Wazuh_Agent-000000?&style=for-the-badge&logo=Wazuh&logoColor=white" />
  <img src="https://img.shields.io/badge/-RHEL-EE0000?&style=for-the-badge&logo=Red-Hat&logoColor=white" />
  <img src="https://img.shields.io/badge/-Cisco_ASA-1BA0D7?&style=for-the-badge&logo=Cisco&logoColor=white" />
</div>

---

## 📝 Deployment Steps

### 1. Deploy Agent via Wazuh Web UI  
- Go to the Wazuh Web UI dashboard
- If no agents exist: Click `Deploy new agent` on the home screen  
- If agents exist:  
  ☰ → Agents management → Summary → `Deploy new agent`

Fill out the following, this is for a linux endpoint Wazuh Agent install:
- **Package**: `Linux (RPM amd64)`  
- **Wazuh Server Address**: `<YOUR WAZUH SERVER IP>`  
- **Agent Name**: `<YOUR ENDPOINT NAME>`

---

### 2. Run the Commands on the Endpoint  
On your endpoint system, run the installer command provided (Step 4 in Web UI):
Then run the three post-installation commands from Step 5 (also provided by Web UI). 
These commands register the agent and start the service.

### 3. Verify Agent Connection Status
On the endpoint, run:
```bash
sudo grep ^status /var/ossec/var/run/wazuh-agentd.state
```
- If it returns connected, the agent is communicating properly
- If it returns pending, check your firewall settings
Required ports to open on Cisco ASA firewall if any:
- 1514/TCP
- 1515/TCP
- 55000/TCP

### Remove an Agent Using CLI
If an agent becomes disconnected or is no longer needed:
```bash
sudo /var/ossec/bin/manage_agents
```
You’ll get a prompt – choose:
```bash
R - Remove an agent 
```
Enter the agent ID (e.g., 001, 003) from the list and confirm deletion.

---

### 👨‍💻 Author
Mario Tagaras | Florida State University Alum














