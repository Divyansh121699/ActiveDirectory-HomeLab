# GUI Operations for Active Directory Home Lab

This guide outlines the steps to install and configure Active Directory on a Windows Server, promote the server to a Domain Controller, and join a Windows target machine to the newly created domain.

---

## **1. Prerequisites**
Ensure the following before starting:
- A Windows Server (e.g., Server 2019 or 2022) installed and running.
- A Windows 10 target machine to join the domain.
- Both systems are running in the same network, preferably virtualized (e.g., VirtualBox or VMware).
- Access to administrative accounts on both machines.

---
## **1. Setting Up Active Directory**

### **Step 1: Set a Static IP Address for the Server**
1. **Open Network Settings**:
   - Right-click the network icon in the system tray and select **Open Network and Internet Settings**.
2. **Change Adapter Options**:
   - Click **Change Adapter Options** > Right-click the network interface > **Properties**.
3. **Set Static IP**:
   - Double-click **Internet Protocol Version 4 (TCP/IPv4)**.
   - Select **Use the following IP address** and enter:
     - **IP Address**: `192.168.10.7`
     - **Subnet Mask**: `255.255.255.0`
     - **Default Gateway**: `192.168.10.1`
     - **Preferred DNS Server**: `8.8.8.8` (Google DNS)
4. Save changes and verify using `ipconfig` in Command Prompt:
   ```cmd
   ipconfig

### **Step 2: Verify Network Connectivity**
- Ping Google to check external connectivity:
  ```cmd
  ping google.com
  ```
- Ping your Splunk server:
  ```cmd
  ping 192.168.1.190
  ```
  
### **Step 3: Install Active Directory Domain Services (AD DS)**
1. Open **Server Manager**.
2. Click **Manage** > **Add Roles and Features**.
3. In the wizard:
   - **Installation Type**: Select **Role-based or feature-based installation**.
   - **Server Selection**: Choose your server.
   - **Server Roles**: Check **Active Directory Domain Services** and click **Add Features**.
4. Click **Next** and then **Install**.
5. After installation, click **Promote this server to a domain controller**.

### **Step 4: Promote to a Domain Controller**
1. In the **Active Directory Domain Services Configuration Wizard**:
   - **Deployment Configuration**: Choose **Add a new forest** and specify a root domain name (e.g., `Project.local`).
   - **Domain Controller Options**: Set the **Forest functional level** and **Domain functional level** (e.g., Windows Server 2022). Enable **DNS server**.
   - Provide a Directory Services Restore Mode (DSRM) password.
2. Complete the wizard and restart the server.

---

## **2. Creating Users and Groups**

### **Step 1: Open Active Directory Users and Computers**
1. Open **Server Manager**.
2. Click **Tools** > **Active Directory Users and Computers**.

### **Step 2: Create Organizational Units (OUs)**
1. Right-click your domain (e.g., `Project.local`) in the left pane and select **New** > **Organizational Unit**.
2. Name the OU (e.g., `IT Department` and `HR Department`) and click **OK**.

### **Step 3: Create a User**
1. Right-click the OU (e.g., `IT Department`) and select **New** > **User**.
2. Fill in the user's details (e.g., First Name: Aditya, Last Name: Prakash, User logon name: `AP`).
3. Set a password and configure account options (e.g., require password change on the first login).

## **3. Joining a Windows 10 Client to the Domain**

1. On the Windows 10 client machine:
   - Right-click **This PC** and select **Properties**.
   - Click **Change settings** under **Computer name, domain, and workgroup settings**.
2. In the **System Properties** window, click **Change**.
3. Select **Domain**, enter your domain name (e.g., `Project.local`), and click **OK**.
4. Provide domain admin credentials when prompted.
5. Restart the machine to apply changes.

---

## **4. Log In as a Domain User**

1. On the Windows 10 login screen, select **Other User**.
2. Enter the domain and username:
   - **Username**: `Project\AP`.
   - **Password**: The user's password was set earlier.
3. Log in and verify successful domain authentication.
