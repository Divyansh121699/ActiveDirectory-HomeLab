# Splunk Universal Forwarder & Sysmon setup guide on Windows Server & Windows Target Machine

This guide walks you through the steps to set up Splunk Universal Forwarder and Sysmon the Windows Server and Windows Target Machine.

---
## **Step-by-Step Setup**

### **Step 1: Install Splunk Universal Forwarder**
1. Download Universal Forwarder MSI from [Splunk](https://www.splunk.com/en_us/download.html).
2. Install the forwarder
   - Choose On-Premise Splunk Enterprise.
   - Set:
       - Splunk Server IP: `192.168.1.190`
       - Receiving Port: `9997`
3. Restart the forwarder:
   - Open Services (`services.msc`).
   - Find SplunkForwarder, set Log On As to Local System Account, and restart the service.

### **Step 2: Install Sysmon**
1. Download Sysmon from [Sysinternals](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon).
2. Get the Sysmon configuration file:
   - Download [sysmon-config.xml](https://github.com/Divyansh121699/ActiveDirectory-HomeLab/blob/main/configs/sysmon-config.xml).
3. Install Sysmon:
   - Open PowerShell as Administrator:
     ```powershell
     cd C:\Users\nigam\Downloads\Sysmon
     .\Sysmon64.exe -i ..\sysmonconfig.xml
     ```
   - **Agree** the System Monitor License Agreement

### **Step 3: Configure Splunk Inputs**
1. Navigate to: `C:\Program Files\SplunkUniversalForwarder\etc\system\local`
2. Create a new file named [inputs.conf](https://github.com/Divyansh121699/ActiveDirectory-HomeLab/blob/main/configs/splunk-inputs.md)
3. Open Services and restart **SplunkForwarder**.

### **Step 4: Configure Splunk Server**
**Create Index**
  1. Access Splunk Web:
     - Navigate to `http://192.168.1.190:8000`
  2. Create an index:
     - Go to **Settings > Indexes > New Index**.
     - Name: `endpoint`
**Enable Data Receiving**
  1. Go to **Settings > Forwarding and Receiving > Configure Receiving**.
  2. Add a new receiving port: `9997`.

### **Step 5: Verify Data**
1. Verify data ingestion:
   - Access Splunk's **Search & Reporting**.
   - Search for: **index=endpoint**
2. Check for Sysmon telemetry:
   - Logs for process creation, registry changes, etc., should appear.
