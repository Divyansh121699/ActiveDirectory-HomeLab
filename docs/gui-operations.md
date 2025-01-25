# GUI Operations for Active Directory Home Lab

This document provides step-by-step instructions for setting up and managing your Active Directory (AD) lab using the Windows Server GUI. Screenshots are included for clarity.

---

## **1. Setting Up Active Directory**

### **Step 1: Install Active Directory Domain Services (AD DS)**
1. Open **Server Manager**.
2. Click **Manage** > **Add Roles and Features**.
3. In the wizard:
   - **Installation Type**: Select **Role-based or feature-based installation**.
   - **Server Selection**: Choose your server.
   - **Server Roles**: Check **Active Directory Domain Services** and click **Add Features**.
4. Click **Next** and then **Install**.
5. After installation, click **Promote this server to a domain controller**.

### **Step 2: Promote to a Domain Controller**
1. In the **Active Directory Domain Services Configuration Wizard**:
   - **Deployment Configuration**: Choose **Add a new forest** and specify a root domain name (e.g., `example.local`).
   - **Domain Controller Options**: Set the **Forest functional level** and **Domain functional level** (e.g., Windows Server 2022). Enable **DNS server**.
   - Provide a Directory Services Restore Mode (DSRM) password.
2. Complete the wizard and restart the server.

---

## **2. Creating Users and Groups**

### **Step 1: Open Active Directory Users and Computers**
1. Open **Server Manager**.
2. Click **Tools** > **Active Directory Users and Computers**.

### **Step 2: Create Organizational Units (OUs)**
1. In the left pane, right-click your domain (e.g., `example.local`) and select **New** > **Organizational Unit**.
2. Name the OU (e.g., `IT Department`) and click **OK**.

### **Step 3: Create a User**
1. Right-click the OU (e.g., `IT Department`) and select **New** > **User**.
2. Fill in the user's details (e.g., First Name: John, Last Name: Doe, User logon name: `jdoe`).
3. Set a password and configure account options (e.g., require password change on first login).

### **Step 4: Create a Group**
1. Right-click the OU (e.g., `IT Department`) and select **New** > **Group**.
2. Name the group (e.g., `IT_Admins`) and select a group scope (e.g., **Global**) and type (e.g., **Security**).
3. Click **OK**.

---

## **3. Configuring Group Policy**

### **Step 1: Open Group Policy Management**
1. Open **Server Manager**.
2. Click **Tools** > **Group Policy Management**.

### **Step 2: Create a Group Policy Object (GPO)**
1. Right-click your domain (e.g., `example.local`) or an OU, and select **Create a GPO in this domain, and Link it here...**.
2. Name the GPO (e.g., `Password Policy`) and click **OK**.

### **Step 3: Edit the GPO**
1. Right-click the GPO and select **Edit**.
2. Navigate to the desired policy path (e.g., `Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Password Policy`).
3. Configure the settings (e.g., set minimum password length to 8 characters).

---

## **4. Joining a Windows 10 Client to the Domain**

1. On the Windows 10 client machine:
   - Right-click **This PC** and select **Properties**.
   - Click **Change settings** under **Computer name, domain, and workgroup settings**.
2. In the **System Properties** window, click **Change**.
3. Select **Domain**, enter your domain name (e.g., `example.local`), and click **OK**.
4. Provide domain admin credentials when prompted.
5. Restart the machine to apply changes.

---

## **5. Monitoring with Splunk**

### **Step 1: Install Splunk**
1. On the Ubuntu server, follow the Splunk installation steps (refer to the `setup-guide.md` for CLI details).
2. Access the Splunk web interface via `http://<server-ip>:8000`.

### **Step 2: Configure Data Inputs**
1. In the Splunk GUI, go to **Settings** > **Data Inputs**.
2. Add a new data input for **Windows Event Logs**.
3. Specify the event types to monitor (e.g., Security, System, Application).

---

## **6. Simulating an Attack with Kali Linux**

### **Step 1: Launch Kali Linux**
1. Boot up the Kali Linux VM.
2. Open a terminal.

### **Step 2: Perform a Brute Force Attack**
1. Use a tool like `hydra` or `medusa` to simulate a brute force attack:
   ```bash
   hydra -l admin -P /usr/share/wordlists/rockyou.txt rdp://<target-ip>
