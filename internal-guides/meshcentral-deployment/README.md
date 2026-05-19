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
