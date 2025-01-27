# Kali Linux attacks & Atomic Red Team guide

In this segment, we simulate a brute force attack using **Kali Linux**, analyze telemetry data with **Splunk**, and implement **Atomic Red Team** to generate attack simulations for detecting gaps in security visibility.

---

## **Segment Overview**

1. **Brute Force Attack Simulation**:
   - Use Kali Linux to perform an RDP brute force attack on a domain user.
   - Analyze attack telemetry in Splunk.

2. **Implement Atomic Red Team**:
   - Simulate real-world attacks using MITRE ATT&CK tactics and techniques.
   - Identify gaps in detection and visibility within your Splunk setup.

3. **Network Configuration**:
   - Configure static IPs for all machines.
   - Ensure network connectivity between machines for seamless telemetry analysis.

---

## **Step 1: Kali Linux Setup**

### **Configure Static IP**
1. Open the network settings in Kali Linux:
   - Right-click the Ethernet icon and select **Edit Connections**.
   - Choose your connection profile (e.g., `Wired Connection 1`).
   - Set the following:
     - **IP Address**: `192.168.1.153`
     - **Netmask**: `/24`
     - **Gateway**: `192.168.1.1`
     - **DNS Server**: `8.8.8.8`
2. Save changes, disconnect, and reconnect the network.

### **Update and Upgrade Kali Linux**
Run the following commands:
```bash
sudo apt-get update && sudo apt-get upgrade -y
```

## **Step 2: Brute Force Attack Using Crowbar**

### **1. Install Crowbar**
```bash
sudo apt-get install crowbar
```

### **2. Prepare Wordlist**
- Locate the RockYou wordlist:
  ```bash
  cd /usr/share/wordlists
  sudo gunzip rockyou.txt.gz
  ```
- Copy the wordlist to a project directory:
  ```bash
  mkdir ~/Desktop/ad-project
  cp rockyou.txt ~/Desktop/ad-project/
  ```

### **3. Create a Custom Password List**
- Use the first 20 lines of the RockYou wordlist:
  ```bash
  head -n 20 ~/Desktop/ad-project/rockyou.txt > ~/Desktop/ad-project/passwords.txt
  ```
- Edit the list to add a specific password
   ```bash
  nano ~/Desktop/ad-project/passwords.txt
  ```
  Add the password to the bottom and save.

### **4. Perform the Brute Force Attack**
- Use the following `crowbar` command to perform the attack:
  ```bash
  crowbar -b rdp -u AP -C ~/Desktop/ad-project/passwords.txt -s 192.168.1.194/32
  ```
- Replace `AP` with the target username.

## **Step 3: Analyzing Telemetry in Splunk**
1. Log in to Splunk and navigate to Search and Reporting.
2. Filter events:
    - Example query:
      ```spl
      index=endpoint "AP"
      ```
    - Focus on Event ID `4625` for failed logins and `4624` for successful logins.
3. Review timestamps to identify brute force activity (multiple failed login attempts followed by a successful one).

## **Step 4: Setting Up Atomic Red Team**

### **1. Prepare the Target Machine**
  - Enable Remote Desktop on the target machine:
      - Navigate to **System Properties > Remote Tab > Allow Remote Connections**.
      - Add domain users for RDP access.

### **2. Install Atomic Red Team**
  - Open PowerShell as Administrator:
    ```powershell
    Set-ExecutionPolicy Bypass CurrentUser
    ```
  - Add a Microsoft Defender exclusion for the C:\ drive:
      - Navigate to **Windows Security > Virus & Threat Protection > Manage Settings > Add Exclusion**
  - Install Atomic Red Team:
    ```powershell
    IEX (IWR 'https://raw.githubusercontent.com/redcanaryco/invoke-atomicredteam/master/install-atomicredteam.ps1' -UseBasicParsing);
    Install-AtomicRedTeam -getAtomics
    ```

### **3. Run a Test Attack**
  - Simulate a persistence attack:
    ```powershell
    Invoke-AtomicTest -TID T1136.001
    ```
### **4. Analyze in Splunk**
  - Search for the created user or activity:
    ```spl
    index=endpoint "new local user"
    ```
