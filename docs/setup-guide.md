# Setup Guide for Active Directory Home Lab

This guide will walk you through the process of setting up a home lab environment using **Active Directory**, **Splunk**, **Kali Linux**, and other tools. Follow these steps to configure your lab and begin practicing both blue team and red team scenarios.

---

## **1. Prerequisites**
Before starting, ensure you have the following:
- **Virtualization Software**: VirtualBox or VMware Workstation.
- **Operating System ISOs**:
  - Windows Server 2022
  - Windows 10
  - Ubuntu Server (for Splunk)
  - Kali Linux
- **Hardware Requirements**:
  - At least 16GB RAM and 100GB storage space.
  - A system capable of running multiple virtual machines simultaneously.

---

## **2. Setting Up the Virtual Machines**
### **Step 1: Create the Virtual Machines**
1. Open VirtualBox/VMware.
2. Create the following VMs:
   - **Windows Server 2022**: Assign 4GB RAM, 50GB storage.
   - **Windows 10**: Assign 2GB RAM, 30GB storage.
   - **Ubuntu Server**: Assign 2GB RAM, 20GB storage.
   - **Kali Linux**: Assign 2GB RAM, 30GB storage.

3. Attach the respective ISO files to each VM and boot them up.

### **Step 2: Network Configuration**
- Set all VMs to use the **NAT Network** or a **Host-Only Adapter** for isolated communication within the lab.

---

## **3. Configuring Active Directory**
### **Step 1: Install Active Directory**
1. Boot into the **Windows Server 2022** VM.
2. Open **Server Manager** and click **Add roles and features**.
3. Follow the wizard:
   - **Role-Based or Feature-Based Installation**.
   - Select **Active Directory Domain Services (AD DS)**.
   - Confirm and install.

### **Step 2: Promote to Domain Controller**
1. After installation, click the notification flag in Server Manager and select **Promote this server to a domain controller**.
2. Choose:
   - **Add a new forest** and name the root domain (e.g., `lab.local`).
3. Configure the following:
   - **Domain Functional Level**: Windows Server 2022.
   - **DNS**: Check the box to install the DNS server role.
   - **Password**: Set a strong password for Directory Services Restore Mode (DSRM).
4. Complete the wizard and restart the server.

---

## **4. Creating Domain Users and Groups**
1. Open **Active Directory Users and Computers**.
2. Navigate to your domain (e.g., `lab.local`).
3. Right-click on **Users** and select **New > User**.
   - Create test users (e.g., `testuser1`, `testuser2`).
4. Right-click on **Users** and select **New > Group**.
   - Create test groups (e.g., `IT_Admins`, `Finance_Team`).

---

## **5. Joining Windows 10 to the Domain**
1. Boot into the **Windows 10** VM.
2. Open **Settings > System > About > Rename this PC (Advanced)**.
3. Click **Change** under **Computer Name/Domain Changes**.
4. Enter the domain name (e.g., `lab.local`) and click **OK**.
5. Enter the domain administrator credentials when prompted.
6. Restart the machine to apply the changes.

---

## **6. Setting Up Splunk**
### **Step 1: Install Splunk on Ubuntu Server**
1. Download Splunk:
   ```bash
   wget -O splunk.deb https://www.splunk.com/path-to-deb
