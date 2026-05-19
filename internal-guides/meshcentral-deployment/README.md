# Internal Deployment Guide: Centralized Endpoint Management via MeshCentral

## Project Overview
This guide documents the installation, perimeter security configuration, and agent deployment of **MeshCentral** within the Boyles IT lab environment. The purpose of this project is to simulate an enterprise-level Unified Endpoint Management (UEM) solution, enabling secure, browser-based remote support, telemetry tracking, and shell access without reliance on traditional SSH keys or heavy remote desktop software.

## Topology & Environment
* **Host OS:** Arch Linux (CachyOS kernel)
* **Guest Server VM:** Ubuntu Server (`osTicket` target)
* **Management Software:** MeshCentral (Node.js engine)
* **Hypervisor:** VirtualBox (NAT Network Topology)

---

## Deployment Architecture & Networking

### 1. Port Forwarding & Routing
Because the management console runs within an isolated NAT network, inbound traffic from the host machine is routed through explicitly mapped ports:

| Rule Name | Protocol | Host IP | Host Port | Guest IP | Guest Port |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `MeshCentral HTTPS` | TCP | `127.0.0.1` | `8443` | `10.0.2.15` | `8080` |

### 2. MeshCentral Configuration (`config.json`)
The application is configured to listen globally on all interfaces inside the guest OS, ensuring the loopback interface maps cleanly to the network socket:
```json
{
  "settings": {
    "cert": "127.0.0.1",
    "port": 8080,
    "aliasPort": 8443
  }
}
```

### 3. Perimeter Security (Firewall Rules)
To ensure minimum necessary exposure, both host and guest firewalls are secured via `ufw`:
* **Ubuntu Server VM:** Hardened to drop all traffic except incoming agent/console handshakes:
  ```bash
  sudo ufw allow 8080/tcp
  sudo ufw enable
  ```
* **Host Machine:** Maintained standard desktop firewall profiles while passing local loopback bindings to Firefox.

---

## Core Administrative Workflows Verified

### 🛡️ Endpoint Auditing & Live Telemetry
Using the integrated, secure browser tunnel, verified live root-level execution capability. System state audits are performed silently without interrupting end-user sessions:
* Resource Tracking: `top -b -n 1 | head -n 12`
* Security Log Auditing: `sudo tail -n 15 /var/log/auth.log`

### 📂 File Tree Auditing
Verified non-intrusive directory navigation using the granular background file explorer to allow for background patch deployment, configuration file synchronization, and remote log retrieval.

---

## Troubleshooting & Key Technical Insights
* **Browser TLS Hard-Blocks:** Encountered strict Chromium/Brave handshake drops due to local self-signed testing certificates. Successfully mitigated by utilizing an isolated Firefox network stack to manually verify and accept the custom local risk exception.
* **Loopback Socket Race Conditions:** Identified standard background file-streaming limits when running a centralized management server and background agent on the exact same loopback port (`8080`). Terminal text channels remain highly responsive under loopback configurations, while file streams operate optimally on separated, dedicated network devices.

---

## 🛠️ Incident Response Case Study: Simulated Database Outage

### Incident Overview
* **Symptom:** Critical corporate web portal outage throwing `500 Internal Server Error` and `Database Connection Failed` alerts across local subnets.
* **Impact:** High; full operational halt for data processing teams.

### Operational Remediation Lifecycle

1. **System Triage via UEM Platform:** Utilized the centralized MeshCentral console to establish a secure browser-based remote shell terminal directly into the application server, avoiding the reliance on localized SSH keys.

2. **Root Cause Analysis (RCA):**
   Executed service state checks and system diagnostic audits to evaluate database daemon status:
   ```bash
   sudo systemctl status mysql
   ```
   *Diagnostic Output:* Isolated the breakdown to an inactive/dead system daemon status, verifying a localized database service crash.

3. **System Correction:**
   Manually initialized system daemon recovery protocols and verified service baseline stability:
   ```bash
   sudo systemctl start mysql
   sudo systemctl status mysql
   ```

4. **Help Desk SLA Resolution:**
   Once service health was verified via live browser loops, logged into the osTicket administrative staff portal (`/scp`), formally claimed the outstanding ticket, documented technical remediation steps for internal audit logging, and closed the incident within service-level expectations.

---

## 🔄 Documentation Maintenance & Version Control Workflow

When updating or maintaining this deployment guide within the technical knowledge base repo, execute the following command sequences to push revisions live:

1. Save the changes locally within the command-line editor (`Ctrl + S` then `Ctrl + Q` in Micro).
2. Commit and sync the master rewrite directly to the remote repository baseline:
   ```bash
   git add internal-guides/meshcentral-deployment/README.md
   git commit -m "Docs: Complete rewrite and unification of UEM deployment guide"
   git push origin main
   ```
