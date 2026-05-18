# 📖 Internal Knowledge Base | Boyles IT Solutions

## 📄 KB-1007: Standard Operating Procedure (SOP) for User Account Provisioning
**Category:** User Onboarding & Identity  
**Target Audience:** Help Desk Tier 1 Technicians / Service Coordinators  
**Prerequisites:** Approved HR Ticket in Jira Service Desk  

---

### 1. Overview
This standard operating procedure ensures that all new user accounts created within the **Boyles IT Solutions** Identity Provider (Google Workspace) are provisioned securely, accurately, and in absolute compliance with our internal **Principle of Least Privilege (PoLP)** guidelines.

---

### 2. Step-by-Step Provisioning Procedure

#### Phase 1: Ticket Validation & Identity Creation
1. **Locate the HR Ticket:** Open the incoming Jira queue and verify the ticket has a status of *Approved by HR*. Note the legal name, department, manager, and start date.
2. **Access Google Workspace Admin Console:** Log into the admin dashboard and navigate to **Directory > Users > Add New User**.
3. **Name & Primary Email:** Input the first and last name. Generate the email address using the standardized format: `first.last@boylesitsolutions.com`.
4. **Organizational Unit (OU) Assignment:** This is a critical security boundary. **Do not** leave the user in the root directory. Click the edit icon next to *Organizational Unit* and assign them strictly to their department path (e.g., `/BITS/Support/HelpDesk` or `/BITS/Operations/Success`).

#### Phase 2: Security & Group Membership
1. **Temporary Password Generation:** Click *Create Temporary Password*. Ensure the checkbox **"Require password change on next sign-in"** is checked.
2. **Group Provisioning:** Based on their role, manually add the user to the correct communication groups:
   * **All Employees:** `all-hands@boylesitsolutions.com`
   * **Department Specific:** e.g., `support-team@boylesitsolutions.com` or `customer-success@boylesitsolutions.com`
3. **License Allocations:** Head to the user's *Licenses* dashboard and toggle active status for required core SaaS application layers (e.g., Google Workspace Enterprise, Jira Service Desk, or Salesforce).

#### Phase 3: Hand-Off & Credential Delivery
1. **Secure Credential Sharing:** Copy the temporary password. **Never** email this password to the user's personal email account in plaintext. 
2. **Secure Note Generation:** Put the initial credentials and login link into a secure, end-to-end encrypted link share tool (e.g., 1Password Secure Sharing or Bitwarden Send) configured to expire automatically after **1 click or 24 hours**.
3. **Manager Delivery:** Send the encrypted link directly to the hiring manager via Slack or internal ticket note so they can deliver it securely to the employee during their morning Day 1 call.
