# Overview
A complete step-by-step guide to deploying **Wazuh Agent** on Windows VM using the official installation assistant.

# Step 1 — Install Windows Agent

Open Dashboard

```
Wazuh
    →
Agents
    →
Deploy New Agent
```

Select

- Windows
- Server IP
- Group: default

Copy the generated PowerShell command.

Run it in **Administrator PowerShell**.

Example:

```powershell
Invoke-WebRequest -Uri https://packages.wazuh.com/4.x/windows/wazuh-agent.msi -OutFile wazuh-agent.msi

msiexec.exe /i wazuh-agent.msi /q WAZUH_MANAGER=<SERVER-IP>
```

Start the service.

```powershell
NET START WazuhSvc
```

---

# Step 2 — Verify Agent

Dashboard

```
Agents
```

Expected status

```
Active
```

Agent information should include

- Hostname
- IP Address
- Operating System
- Last Keep Alive

---

# Useful Commands

Restart Manager

```bash
sudo systemctl restart wazuh-manager
```

Restart Dashboard

```bash
sudo systemctl restart wazuh-dashboard
```

Restart Indexer

```bash
sudo systemctl restart wazuh-indexer
```

Restart Filebeat

```bash
sudo systemctl restart filebeat
```

Check all services

```bash
sudo systemctl status wazuh-manager
sudo systemctl status wazuh-indexer
sudo systemctl status wazuh-dashboard
sudo systemctl status filebeat
```

View Manager logs

```bash
sudo journalctl -u wazuh-manager -f
```

View Dashboard logs

```bash
sudo journalctl -u wazuh-dashboard -f
```

View Indexer logs

```bash
sudo journalctl -u wazuh-indexer -f
```
---

# References

- Official Wazuh Documentation: https://documentation.wazuh.com/
- Wazuh Installation Guide: https://documentation.wazuh.com/current/installation-guide/wazuh-agent/wazuh-agent-package-windows.html
- Wazuh GitHub: https://github.com/wazuh/wazuh

---

# Author

**Ritesh V**

Cyber Security Engineering Student

KCG College of Technology

---

## License

This project is intended for educational and home lab purposes.