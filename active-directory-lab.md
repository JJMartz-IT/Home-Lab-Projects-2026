# Active Directory Domain Services Deployment

Deployed and configured a Windows Server 2022 domain controller from scratch in a virtualized lab, then built out an organizational unit structure, security groups, and user accounts to reflect a small multi-region company.

---

## Environment

- **Hypervisor:** VMware Workstation
- **Server OS:** Windows Server 2022 Standard (Evaluation)
- **Role deployed:** Active Directory Domain Services (AD DS)
- **Domain:** `HomeLab.local`

---

## Objective

Stand up a functioning Active Directory domain from a clean Windows Server install, then structure it the way a small organization with multiple regional offices would — separate Organizational Units (OUs) per region, each with its own Computers, Users, and Servers containers, plus a working security group and a test user account.

---

## Steps

### 1. Install the Active Directory Domain Services role
Opened Server Manager and launched the **Add Roles and Features Wizard**, selected role-based installation, and checked **Active Directory Domain Services**. Windows automatically flagged the required supporting features (Group Policy Management, Remote Server Administration Tools, DNS Server).

![Server Manager dashboard](./screenshots/01-server-manager-dashboard.png)
![Selecting installation type](./screenshots/02-add-roles-installation-type.png)
![Selecting the AD DS role](./screenshots/03-select-server-roles-adds.png)

### 2. Run the installation
Let the wizard install AD DS along with DNS Server, Group Policy Management, and the AD DS/LDS administrative tools.

![Installation in progress](./screenshots/04-installation-progress-start.png)
![Installation succeeded, prompting promotion](./screenshots/05-installation-succeeded-promote-prompt.png)

### 3. Promote the server to a domain controller
From the post-install notification, selected **Promote this server to a domain controller** and configured it as a **new forest** with the root domain name `HomeLab.local`.

![Deployment configuration - new forest](./screenshots/06-deployment-configuration-new-forest.png)

### 4. Prerequisites check and installation
Reviewed the prerequisites check (passed with only default informational warnings around cryptography compatibility and static IP recommendations) and proceeded with installation. The server rebooted automatically to complete domain controller promotion.

![Prerequisites check passed](./screenshots/07-prerequisites-check-passed.png)

### 5. Verify the domain in Active Directory Users and Computers
After reboot, opened **Active Directory Users and Computers** and confirmed the `HomeLab.local` domain was live with its default containers (Builtin, Computers, Domain Controllers, Users, etc.).

![Default AD containers under HomeLab.local](./screenshots/08-aduc-default-containers.png)

### 6. Build the OU structure
Created three top-level Organizational Units to represent regional offices — **USA**, **Europe**, and **Asia** — each with its own **Computers**, **Users**, and **Servers** sub-containers, to keep resources logically separated by region for delegated administration and Group Policy scoping.

![Regional OU structure](./screenshots/09-aduc-ou-structure-created.png)

### 7. Create a security group
Created a group named `DL - ITAdmins` inside `USA/Users` to hold IT administrator accounts for that region.

![Creating the ITAdmins group](./screenshots/10-new-group-object-itadmins.png)

### 8. Create a test user account
Created a new user object inside `USA/Users` to confirm accounts could be provisioned correctly within the new OU structure.

![Creating a new user object](./screenshots/11-new-user-object-creation.png)

---

## Troubleshooting

**Locating the AD DS role:** Wasn't immediately obvious where to begin the role installation from a fresh server install. Resolved by researching the Server Manager workflow — the role is added through **Manage → Add Roles and Features**, not a standalone installer.

**Domain name rejected:** The initial root domain name I tried wasn't accepted by the Domain Services Configuration Wizard. Root-caused it to Active Directory's requirement for a valid DNS-style suffix — switching to `HomeLab.local` resolved it and let the forest creation proceed.

---

## Skills demonstrated

- Windows Server role installation and configuration (AD DS, DNS)
- Active Directory forest and domain creation
- OU design for a multi-site organizational structure
- Security group and user account provisioning
- Reading and resolving prerequisite/configuration errors independently

---

## Resume / portfolio summary

> Deployed a Windows Server 2022 Active Directory domain in a VMware lab environment, including forest creation, a multi-region OU structure, security groups, and user provisioning.
