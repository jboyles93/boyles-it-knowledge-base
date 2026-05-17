# BOYLES IT SOLUTIONS | INTERNAL KNOWLEDGE BASE

## 📄 KB-1004: Workspace Account Sync & Password Re-Authentication Guide
**Category:** Account Access & Security  
**Target Audience:** All Internal End-Users  
**Last Updated:** May 2026  

---

### Overview
If your workspace applications (Email, Dashboard, File Shares) are looping, prompting for credentials repeatedly, or displaying a **"Session Expired"** alert, your local machine needs to re-authenticate with the central Boyles IT active directory relay. 

This quick guide will walk you through verifying a legitimate IT notification, performing a secure password sync, and resolving browser handshake loops in under 5 minutes.

---

### Step 1: Verify the Security of the Request
Before entering your credentials anywhere, always verify that the authentication prompt is an official Boyles IT Solutions request. 

* **Check the Sender Domain:** Official internal IT communications will only come from an `@boyles-it.local` or `@boylesitsolutions.com` address. 
* **Check the URL Bar:** The login page should always display the secure lock icon (`https://`) and point explicitly to a trusted internal portal address (e.g., `portal.boyles-it.local`).
* **The Golden Rule:** Boyles IT Support will **never** ask you to reply to an email with your cleartext password.

---

### Step 2: Clear Your Browser Handshake Cache
Sometimes, your web browser tries to use an old, expired authentication token instead of prompting for your new one, causing an infinite loading loop.

1. Open your web browser (e.g., Brave, Chrome, or Firefox).
2. Press `Ctrl` + `Shift` + `Delete` (Windows/Linux) or `Cmd` + `Shift` + `Delete` (Mac) to open the **Clear Browsing Data** menu.
3. Set the time range to **Last hour**.
4. Check the box next to **Cookies and other site data** and **Cached images and files**.
5. Click **Clear Data**, then close and reopen your browser window.

---

### Step 3: Execute the Workspace Sync
1. Navigate directly to your assigned workspace portal at: `http://portal.boyles-it.local/sync` *(or your team's designated local landing page)*.
2. In the **Username** field, enter your full corporate email address (e.g., `m.garcia@boyles-it.local`).
3. In the **Password** field, enter your current active network password.
4. Click the yellow **Sync Account** button.

> ⚠️ **Note:** Once you click sync, the screen will momentarily refresh and securely forward you back to your primary Google Workspace or company homepage. This confirms your active session token has been successfully regenerated.

---

### Still Having Trouble?
If you are still locked out or receiving an authentication error after following these steps, our technical team is ready to assist:
* **Open a Ticket:** Log into the **Boyles IT Service Desk** dashboard and select the **High Priority: Account Access** category.
* **Emergency Escalation:** If you cannot access the ticketing system, contact the Service Coordinator directly at `support@boylesitsolutions.com`.
