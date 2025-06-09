# Configuring-On-premises-Active-Directory-within-Azure-VM
# Configuring On-Premises Active Directory within Azure VMs

<p align="center">
  <img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

## Overview

This tutorial demonstrates how to deploy and configure an **on-premises-style Active Directory** environment using **Azure Virtual Machines**.

---

## 📺 Video Demonstration

- [YouTube: How to Deploy On-Premises Active Directory within Azure Compute](https://www.youtube.com)

---

## 🧰 Technologies Used

- Microsoft Azure (Virtual Machines)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

---

## 💻 Operating Systems Used

- Windows Server 2022 (DC)
- Windows 10 (21H2)

---

## 🔧 Steps

### 1. Configure DNS on Client-1

Change Client-1's DNS settings to use DC-1's private IP address and restart the VM.

**Verification:** Ping DC-1 to ensure connectivity.

![DNS Setup](https://i.imgur.com/A2kRBvU.png)

---

### 2. Install Active Directory on DC-1

1. Open **Server Manager**
2. Select **Add roles and features**

![Server Manager - Add Roles](https://i.imgur.com/DQz8fMX.png)

3. Choose **Role-based or feature-based installation**

![Role-Based Installation](https://i.imgur.com/ZVZtscY.png)

4. Select the local server (DC-1)

![Select Server](https://i.imgur.com/2REXkce.png)

5. Choose **Active Directory Domain Services**

![Add AD DS](https://i.imgur.com/JR07V9d.png)

6. Add features as prompted

![Add Features](https://i.imgur.com/Fl19UPW.png)

7. Continue and install

![Install Roles](https://i.imgur.com/tTh69vE.png)

---

### 3. Promote Server to Domain Controller

Click the flag icon → **Promote this server to a domain controller**

![Promote to DC](https://i.imgur.com/oKmAzf6.png)

- Choose **Add a new forest**
- Set root domain name (e.g., `mydomain.com`)

![Domain Configuration](https://i.imgur.com/Gpi0qXD.png)

- Set DSRM password

![Directory Services Restore Mode](https://i.imgur.com/w2WwTPO.png)

- Complete installation and restart

---

### 4. Log In to Domain

Log in using the domain:

---

### 5. Active Directory Configuration

- Open **Active Directory Users and Computers (ADUC)**

![ADUC](https://i.imgur.com/f0wzFT9.png)

- Create two OUs:
  - `_EMPLOYEES`
  - `_ADMINS`

![Create OUs](https://i.imgur.com/vRJQ96Z.png)

- Create user `jane_admin` and add to **Domain Admins**

![Jane Admin](https://i.imgur.com/IKNaIFM.png)

- Log out and log back in as:

---

### 6. Join Client-1 to Domain

- Log in to **Client-1** as local admin
- Join domain `mydomain.com`
- Log in with domain credentials

---

### 7. Move Client-1 to an OU

- In ADUC, create a new OU: `_CLIENTS`
- Move Client-1 into `_CLIENTS`

![Client OU](https://i.imgur.com/gFDTsM4.png)

---

### 8. Enable RDP for Domain Users

- On Client-1, go to **System Properties** → **Remote**
- Allow **Domain Users** access to RDP

---

### 9. Create Bulk Users via PowerShell

- Log in to DC-1
- Open **PowerShell ISE as Administrator**
- Run script to generate test users

![PowerShell Script](https://i.imgur.com/fPbrh6w.png)

- Verify new users are created in `_EMPLOYEES`

---

### 10. Log In with a Test User

- Log in to Client-1 with a test account
- Verify domain login with `whoami`

---

## ✅ Summary

You now have an on-premises style Active Directory set up in Azure. You configured DNS, installed and promoted AD, joined a client machine, and tested login with bulk users.

---
© 2025 | Tutorial by YC
