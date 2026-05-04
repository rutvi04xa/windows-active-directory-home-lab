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



  
  
