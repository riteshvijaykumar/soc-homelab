# 🛡️ Wazuh SIEM Installation Guide (Single-Node Deployment)

A complete step-by-step guide to deploying **Wazuh SIEM** on Ubuntu Server using the official installation assistant.

# Overview

This guide installs a **single-node Wazuh deployment** containing:

- Wazuh Manager
- Wazuh Indexer
- Wazuh Dashboard
- Filebeat

The installation uses the official **wazuh-install.sh** deployment script.

---

# Lab Environment

| Component | Value |
|-----------|-------|
| OS | Ubuntu Server 24.04 LTS |
| RAM | 8 GB Minimum |
| CPU | 4 vCPU Recommended |
| Storage | 50 GB |
| Wazuh Version | Latest Stable |
| Deployment | Single Node |



# Prerequisites

Before beginning, ensure:

- Fresh Ubuntu Server installation
- Internet connectivity
- Root or sudo privileges
- Minimum 4GB RAM (8GB recommended)
- Static IP recommended

Check system information:

```bash
hostnamectl
```

---

# Step 1 — Update Ubuntu

Update package repositories.

```bash
sudo apt update
sudo apt upgrade -y
```

Reboot if required.

```bash
sudo reboot
```

---

# Step 2 — Install Curl

The installer requires curl.

```bash
sudo apt install curl -y
```

Verify:

```bash
curl --version
```

---

# Step 3 — Download the Wazuh Installer

Download the official installation script.

```bash
curl -sO https://packages.wazuh.com/4.12/wazuh-install.sh
```

Give execute permission.

```bash
chmod +x wazuh-install.sh
```

Verify the file exists.

```bash
ls
```

Output should include:

```
wazuh-install.sh
```

---

# Step 4 — Install Wazuh

Run the installation assistant.

```bash
sudo ./wazuh-install.sh -a
```

The installer automatically installs:

- Wazuh Manager
- Wazuh Indexer
- Wazuh Dashboard
- Filebeat

Installation may take **10–30 minutes**.

---

## Installation Completed

At the end, the script displays something similar to:

```
INFO: --- Summary ---
INFO: You can access the dashboard:

https://<SERVER-IP>

Username: admin
Password: <generated-password>
```

**Save the generated password.**

---

# Step 5 — Verify Services

Check Manager

```bash
sudo systemctl status wazuh-manager
```

Check Indexer

```bash
sudo systemctl status wazuh-indexer
```

Check Dashboard

```bash
sudo systemctl status wazuh-dashboard
```

Check Filebeat

```bash
sudo systemctl status filebeat
```

Expected status:

```
active (running)
```

---

# Step 6 — Access Wazuh Dashboard

Open your browser.

```
https://SERVER-IP
```

Example

```
https://192.168.232.136
```

A browser warning appears because Wazuh uses a self-signed certificate.

Choose:

```
Advanced
Proceed
```

---

# Step 7 — Login

Default username

```
admin
```

Password

```
Generated during installation
```

You should now see the Wazuh Dashboard.

---

# Step 8 — Change Admin Password (Recommended)

Run:

```bash
sudo tar -O -xvf wazuh-install-files.tar wazuh-install-files/wazuh-passwords.txt
```

Or use the password generated during installation.

Change it from the Dashboard after logging in.

---

# Common Troubleshooting

## Dashboard Not Opening

Check:

```bash
sudo systemctl status wazuh-dashboard
```

---

## Indexer Failed

Check:

```bash
sudo systemctl status wazuh-indexer
```

View logs

```bash
sudo journalctl -u wazuh-indexer -n 100
```

---

## Manager Not Running

Restart:

```bash
sudo systemctl restart wazuh-manager
```

---

## Filebeat Issues

Restart:

```bash
sudo systemctl restart filebeat
```

---

## Agent Not Appearing

Verify:

- Correct Manager IP
- Agent service running
- Firewall allows port **1514** and **1515**

Windows

```powershell
NET START WazuhSvc
```

---

# Firewall Ports

| Port | Purpose |
|------|----------|
| 443 | Dashboard |
| 1514 | Agent Events |
| 1515 | Agent Registration |
| 55000 | Wazuh API |
| 9200 | Indexer |

---

# Directory Structure

```
/var/ossec/
/etc/filebeat/
/etc/wazuh-dashboard/
/etc/wazuh-indexer/
/usr/share/wazuh-dashboard/
```

---

# Installed Components

```
Ubuntu Server
      │
      ▼
+----------------------+
|  Wazuh Dashboard     |
+----------------------+
          │
          ▼
+----------------------+
|   Wazuh Indexer      |
+----------------------+
          │
          ▼
+----------------------+
|   Wazuh Manager      |
+----------------------+
          ▲
          │
Windows/Linux Agents
```

---

# References

- Official Wazuh Documentation: https://documentation.wazuh.com/
- Wazuh Installation Guide: https://documentation.wazuh.com/current/installation-guide/index.html
- Wazuh GitHub: https://github.com/wazuh/wazuh

---

# Author

**Ritesh V**

Cyber Security Engineering Student

KCG College of Technology

---

## License

This project is intended for educational and home lab purposes.