# Day-03-Elasticsearch-Setup
30‑Day MyDFIR SOC Analyst Challenge Elasticsearch Setup Tutorial

# 📌 Objective
Set up and configure an Elasticsearch instance inside your Vultr VPC environment. This includes provisioning the VM, installing Elasticsearch, securing access, and preparing the instance for Kibana integration.

# 🧠 Skills Learned
- Creating and configuring a Vultr VPC Networks
- Deploying a Ubuntu 22.04 server for Elasticsearch
- Installing Elasticsearch via .deb package
- Managing systemd services (enable, start, status)
- Editing elasticsearch.yml for network access
- Resetting Elasticsearch built‑in user passwords
- Applying firewall rules to restrict access
- Connecting via SSH and performing system updates

# 🛠️ Tools Used
- Vultr Cloud Platform (VPC + VM deployment)
- Ubuntu 22.04 LTS
- PowerShell / SSH
- Elasticsearch 8.x
- Nano (config editing)
- systemctl
- Vultr Firewall Groups

# 🏗️ Environment Architecture
- VPC Network
  - IPv4 Range: <ip-adress>
- Elasticsearch VM
  - Location: Atlanta
  - Specs: 4 vCPU, 16GB RAM, 80GB SSD
  - Private IP: <ip-adress>
  - Public IP: Assigned by Vultr
- SSH Access
  - User: root
  - Port: 22

# 📜 Steps Performed
1️⃣ Create VPC
- Navigate to Network → VPC Networks
- Create a new VPC
- Set IPv4 range: <ip-adress>/24
- Name it MYDFIR-30-Day-Challenge
- Reference Image #1

2️⃣ Deploy Elasticsearch VM
- Navigate to Compute → Instances → Click Deploy New Server 
- Region: same as VPC
- OS: Ubuntu 22.04
- Plan: 4 vCPU / 16GB RAM / 80GB SSD
- Disable: Auto‑backups, IPv6
- Attach VPC 2.0
- Name host: DFIR-ELK
- Deploy
- Reference Image #2

3️⃣ SSH Into the Server
bash
- ssh root@<PUBLIC-IP>

4️⃣ Update System
bash
- apt-get update && apt-get upgrade -y

5️⃣ Download & Install Elasticsearch
bash
- wget <ElasticSearch-deb-download-link>
- Reference Image #3
- dpkg -i elasticsearch-8.x.x-amd64.deb

6️⃣ Save Auto‑Generated Security Credentials
During installation, Elasticsearch prints:
- Built‑in user password
- Enrollment token
- Security bootstrap info
Save this output in a text file for later use.

7️⃣ Reset Password (If Needed)
bash
- cd /usr/share/elasticsearch/bin
- ./elasticsearch-reset-password -u elastic

8️⃣ Edit elasticsearch.yml
bash
- cd /etc/elasticsearch
- ls
- nano elasticsearch.yml

Modify:

yaml
- network.host: <ip-adress>
- http.port: 9200
- Save with Ctrl + X, then Y.

9️⃣ Apply Firewall Rules
In Vultr:
- Create a Firewall Group
- Restrict SSH to your IP only
- Attach the firewall group to your VM

🔟 Start Elasticsearch Service
bash
- systemctl daemon-reload
- systemctl enable elasticsearch.service
- systemctl start elasticsearch.service
- systemctl status elasticsearch.service

# 🖼️ Reference Images

Reference #1
![Create_VPC_Network](<images/Create VPC Network.png>)

Reference #2
![Deployed_New_Server_Instance](<images/Deployed New Server Instance.png>)

Reference #3
![Downloaded_ElasticSearch](<images/Downloaded ElasticSearch.png>)
