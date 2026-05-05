<h1>Windows Server Active Directory Home Lab</h1>


<h2>Description</h2>
This project is a Windows Server Active Directory home lab that simulates a real-world enterprise IT environment. It includes the setup of Active Directory Domain Services (AD DS), user and group management, Organizational Units (OUs), and domain-joined client machines.

The lab also implements Group Policy Objects (GPOs) for system policy enforcement, along with file sharing and NTFS permissions for access control. Advanced Windows Server concepts such as security policies, password policies, and access-based permissions are also configured to demonstrate enterprise-level administration.
<br />


## 📌 1 — Installing Active Directory on Windows Server on Virtual Machine


### Implementation Steps

- Set up Windows Server 2022 in VMware Workstation Pro 17 and completed OS installation  
- Installed and configured Active Directory Domain Services (AD DS)  
- Promoted server to Domain Controller and created basic domain structure  
- Created Organizational Units (OUs), users, and security groups  
- Configured group scopes and assigned users for access management

## Lab Resources & Tools

- Windows Server 2022 ISO:  
https://www.microsoft.com/en-us/evalcenter/download-windows-server-2022

- VMware Workstation Pro 17:  
https://knowledge.broadcom.com/external/article?articleNumber=368667

## Installing and Configuring Active Directory Tools and Promote as DC

To install Active Directory Domain Services (AD DS) on Windows Server 2022, the installation is performed through Server Manager using the Add Roles and Features wizard.

Open **Server Manager → Manage → Add Roles and Features**

![Select Installation Type](screenshots/select-installation-type.png)
Select **Role-based or feature-based installation** to proceed with AD DS setup.

---

![Select Destination Server](screenshots/Select-Destination-Server.png)
Choose the local server where Active Directory will be installed.

---

![Select Server Roles](screenshots/Select-Server-Role.png)
Select **Active Directory Domain Services (AD DS)/DNS server/Remote Access/** from the list of roles.

---

![Select Features](screenshots/Select-Features.png)
Keep default features and proceed with installation requirements.

---

![Installation Completed](screenshots/Installation-Completed.png)
The AD DS role installation completes successfully and is ready for promotion to Domain Controller.

---

## Promoting Server to Domain Controller

After installing Active Directory Domain Services (AD DS), the server is promoted to a Domain Controller to create a new domain environment.

Clicked on **“Promote this server to a domain controller”** to configure the system as part of a domain environment.

> **Note:** This option appears in **Server Manager → Notifications (flag icon)** after the Active Directory Domain Services (AD DS) installation is completed.

A new forest was created by defining the domain name "master.local", followed by configuring essential Domain Controller settings such as DNS and Global Catalog. A secure DSRM password was set, prerequisites were validated, and the installation was completed successfully with an automatic system restart.

---

![Deployment Configuration](screenshots/deployment-configuration.png)
Configured a new forest and defined the domain name: master.local.

---

![NETBIOS Domain Name](screenshots/NETBIOS-domain-name.png)
System automatically generated and verified the NetBIOS domain name.

---

![Login with Domain](screenshots/login-page-with-domain.png)
Server successfully restarted and domain login is now available.

## Active Directory Basic Configuration

After promoting the server to a Domain Controller, the Active Directory environment was structured by organizing resources using Organizational Units (OUs), groups, and user accounts.

Organizational Units were created to logically separate departments, followed by nested OUs for better hierarchy. Security/Distribution groups were then created within OUs, and user accounts were added and assigned to appropriate groups for access management.

![Active Directory Users and Computers View](screenshots/users-computers-view.png)
In this view, all Organizational Units, Groups, and Users are organized under the **master.local** domain.

> **Note:** Active Directory Users and Computers can be opened by running `dsa.msc` or through **Server Manager → Tools → Active Directory Users and Computers**.

---

### Organizational Unit (OU) Creation

> **Note:** Organizational Units are created in **Active Directory Users and Computers** by right-clicking the domain → New → Organizational Unit.

![Creating OU 1](screenshots/creating-ou-1.png)
![Creating OU 2](screenshots/creating-ou-2.png)
![Creating OU 3](screenshots/creating-ou-3.png)

---

### Group Creation

> **Note:** Groups are created inside an OU by right-clicking → New → Group, then selecting group type (Security or Distribution).

![Creating Group 1](screenshots/creating-group-1.png)
![Creating Group 2](screenshots/creating-group-2.png)
![Creating Group 3](screenshots/creating-group-3.png)
![Creating Group 4](screenshots/creating-group-4.png)

> **Note:** Active Directory groups are defined by **Group Type** and **Group Scope**.  
> 
> **Group Type:**  
> - Security Groups → Used for assigning permissions to resources  
> - Distribution Groups → Used only for grouping users (no permissions)  
> 
> **Group Scope:**  
> - Domain Local → Used for assigning permissions within the same domain  
> - Global → Used to group users from the same domain for broader access  
> - Universal → Used across multiple domains within a forest

### User Account Creation

> **Note:** User accounts are created inside an OU by right-clicking → New → User and entering required details.

![Creating User 1](screenshots/creating-user-1.png)
![Creating User 2](screenshots/creating-user-2.png)
![Creating User 3](screenshots/creating-user-3.png)

### User Assignment to Groups

> **Note:** Users can then be assigned to groups by opening user properties → Member Of → Add.

![Add user to group](screenshots/users-to-group.png)


![Add user to group](screenshots/users-to-group.png)

<br>

## 📌 2 — Group Policy Management (GPO) Setup

### Prerequisites

1. **Windows Server Installation:** Windows Server 2022 is installed and running on a virtual machine.  
2. **Active Directory Domain Services (AD DS):** Domain Controller is configured with a working domain environment.  
3. **Group Policy Management Console (GPMC):** GPMC is available through Server Manager → Tools for managing Group Policy Objects (GPOs).


![Group Policy Management Console](screenshots/group-policy-management-console.png)
Group Policy Management Console (GPMC)

> **Note:** Group Policy Management Console (GPMC) can be accessed from **Server Manager → Tools → Group Policy Management**.  
> If not available, it can be installed by going to **Server Manager → Add Roles and Features → Features → Group Policy Management**.
---

### 📌 Types of Group Policy Settings

> **Note:** Group Policy settings are divided into two main categories based on how they are applied:

- **Computer Configuration**  
  These settings apply to the computer itself, regardless of which user logs in. Once applied, they affect the system as a whole.

- **User Configuration**  
  These settings apply to users. They are applied when a user logs in and affect user-specific environments such as desktop settings and preferences.

---

### 📊 Group Policy Structure Overview

```mermaid
flowchart TD

    A[🟦 Group Policy]

    A --> B[🖥️ Computer Configuration]
    A --> C[👤 User Configuration]

    B --> B1[📁 Policies]
    B --> B2[⚙️ Preferences]

    B1 --> B1a[🔒 Password Policy]
    B1 --> B1b[🚫 Account Lockout Policy]

    B2 --> B2a[🖧 System Settings]
    B2 --> B2b[📜 Startup Scripts]

    C --> C1[📁 Policies]
    C --> C2[⚙️ Preferences]

    C1 --> C1a[🔐 Security Policies]
    C1 --> C1b[🚷 User Restrictions]

    C2 --> C2a[📂 Mapped Drives]
    C2 --> C2b[🖨️ Printers]
    C2 --> C2c[🖥️ Desktop Shortcuts]
```
### GPO Configuration Demo Activities

### Demo 1: Password Policy

![Password Policy Configuration](screenshots/password-policy.png)

Password Policy was configured using Group Policy (Computer Configuration) to enforce domain-wide security standards. The policy ensures users follow strong password rules such as minimum length and complexity, improving overall account security across the domain.

---

> **📝 Note: How this GPO was created**

- Open **Group Policy Management Console (GPMC)**
- Right-click on **Group Policy Objects → New**
- Enter a name (e.g., Password Policy)
- Right-click the created GPO → **Edit**
- Navigate to:  
  `Computer Configuration → Policies → Windows Settings → Security Settings → Account Policies → Password Policy`
- Configure required password settings
- Link the GPO to the required **Organizational Unit (OU)**
- Run `gpupdate /force` to apply changes

### Demo 2:Control Panel Restriction

![Control Panel Restriction](screenshots/control-panel-restriction.png)

Control Panel access was restricted using Group Policy (User Configuration) to prevent users from changing system settings and maintaining system security and standardization across the domain.

---

> **📝 Note: How this GPO was created**

- Open **Group Policy Management Console (GPMC)**
- Right-click on **Group Policy Objects → New**
- Enter a name (e.g., Control Panel Restriction)
- Right-click the created GPO → **Edit**
- Navigate to:  
  `User Configuration → Policies → Administrative Templates → Control Panel`
- Enable the policy **"Prohibit access to Control Panel and PC settings"**
- Link the GPO to the required **Organizational Unit (OU)**
- Run `gpupdate /force` to apply changes
