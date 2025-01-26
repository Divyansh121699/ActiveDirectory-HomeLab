# Active Directory Home Lab Setup Guide

This guide walks you through installing and configuring a home lab environment using **Active Directory**, **Splunk**, **Kali Linux**, and other tools in Virtual Machines (VMs).

---

## **1. Prerequisites**

### **Hardware Requirements**
- **Processor**: 4 cores or higher
- **RAM**: At least 16GB
- **Disk Space**: At least 100GB free
- **Network**: Internet access for downloading software

### **Software Requirements**
- **Virtualization Software**: [VirtualBox](https://www.virtualbox.org/)
- **Operating System ISOs**:
  - [Windows Server 2022](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server)
  - [Windows 10](https://www.microsoft.com/software-download/windows10ISO)
  - [Ubuntu Server](https://ubuntu.com/download/server)
  - [Kali Linux](https://www.kali.org/get-kali/)

---

## **2. Installing Virtual Machines**

### **Step 1: Set Up VirtualBox**
1. Download and install VirtualBox.
2. Launch the software and add **Bridged Adapter** to each machine for VM communication:

### **Step 2: Install Windows Server 2022**
1. Open VirtualBox and click **New**.
2. Configure the VM:
   - **Name**: `Windows Server 2022`
   - **Type**: Microsoft Windows
   - **Version**: Windows 2022 (64-bit)
   - **Memory**: 4GB
   - **Storage**: 50GB dynamically allocated
3. Attach the Windows Server 2022 ISO.
4. Start the VM and follow the installation steps:
   - Choose **Custom Installation**.
   - Select the 50GB disk and proceed.
   - Set an **Administrator password** during setup.
5. Once installed, log in with the Administrator account.

### **Step 3: Install Windows 10**
1. Create a new VM with the following settings:
   - **Name**: `Windows 10`
   - **Type**: Microsoft Windows
   - **Version**: Windows 10 (64-bit)
   - **Memory**: 4GB
   - **Storage**: 30GB dynamically allocated
2. Attach the Windows 10 ISO.
3. Start the VM and follow the installation steps:
   - Set up a local user account with a password.
4. Once installed, update the VM via **Windows Update**.

### **Step 4: Install Ubuntu Server (for Splunk)**
1. Create a new VM with the following settings:
   - **Name**: `Ubuntu Server`
   - **Type**: Linux
   - **Version**: Ubuntu (64-bit)
   - **Memory**: 2GB
   - **Storage**: 20GB dynamically allocated
2. Attach the Ubuntu Server ISO.
3. Start the VM and follow the installation steps:
   - Choose minimal installation.
   - Set up a username and password for the server.
   - Enable SSH during setup.
4. After installation, update the system:
   ```bash
   sudo apt update && sudo apt upgrade -y

### **Step 5: Install Kali Linux**
1. Create a new VM with the following settings:
   - **Name**: `Kali Linux`
   - **Type**: Linux
   - **Version**: Debian (64-bit)
   - **Memory**: 4GB
   - **Storage**: 20GB dynamically allocated
2. Attach the Kali Linux ISO.
3. Start the VM and follow the installation steps:
   - Set up a root password.
   - Choose default tools during setup.
4. After installation, update the system:
   ```bash
   sudo apt update && sudo apt upgrade -y
