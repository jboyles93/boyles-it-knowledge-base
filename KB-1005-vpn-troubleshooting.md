# BOYLES IT SOLUTIONS | INTERNAL KNOWLEDGE BASE

## 📄 KB-1005: Remote Work VPN Disconnections & Network Conflicts
**Category:** Remote Infrastructure & Connectivity  
**Target Audience:** Remote and Hybrid Employees  
**Last Updated:** May 2026  

---

### Overview
When working remotely, maintaining a stable connection to the secure Boyles IT network is vital for accessing internal databases, file shares, and ticketing portals. 

If your VPN client (e.g., OpenVPN / WireGuard) is failing to connect, stuck in a "Connecting..." status, or frequently dropping out, follow this systematic troubleshooting guide to restore your workspace connection.

---

### Step 1: The Local Internet Validation Check
Before troubleshooting the secure corporate tunnel, we must ensure your local home internet routing path is healthy.

1. Disconnect from the secure VPN client completely.
2. Open a new web browser tab and attempt to load a reliable public site (like `google.com`).
3. If the page fails to load:
   * Unplug your home Wi-Fi router/modem from its power outlet.
   * Wait exactly **30 seconds**, then plug it back in.
   * Allow 2-3 minutes for the router lights to turn solid green, re-establish your local connection, and try the webpage again.

---

### Step 2: Resolve Local IP Subnet Conflicts
A common issue for remote workers occurs when their home router uses the exact same underlying local network identifier address (`192.168.1.X`) as the corporate subnet, causing data packets to get lost.

* **The Quick Fix:** If you are connected to your home network via Wi-Fi, try connecting your laptop directly to your internet router using a physical **Ethernet cable** if available. This prioritizes a direct routing handshake and bypasses standard wireless signal interference.

---

### Step 3: Clear Local Routing Handshakes & Flush DNS
If your network connection dropped abruptly, your operating system might still be trying to use a broken routing path. 

#### For Windows Machines:
1. Press the Windows Key, type `cmd`, and open the **Command Prompt**.
2. Type `ipconfig /flushdns` and press **Enter**.
3. Type `netsh winsock reset` and press **Enter**.
4. Restart your computer and attempt to open your VPN client again.

#### For Linux/Mac Machines:
1. Open your terminal application.
2. Restart your network manager service using your distribution's standard wrapper:
   * *Example:* `sudo systemctl restart NetworkManager`

---

### Sticking Points & Next Steps
If your client still refuses to clear the authentication check or secure a handshake after completing these steps, the issue may stem from an expired security certificate or an upstream ISP block.

* **Submit an Issue:** Open the **Boyles IT Service Desk** and file a ticket under **Network/Connectivity -> VPN Issue**. 
* **Crucial Info to Include:** Please note if you are using home Wi-Fi or cellular hotspot data, and take a quick screenshot of any explicit error codes displayed inside your VPN client logs so our team can escalate it immediately.
