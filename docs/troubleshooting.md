# Troubleshooting Guide for Active Directory Home Lab

This guide provides solutions to common issues you may encounter while setting up your Active Directory (AD) Home Lab. Follow the steps below to resolve problems efficiently.

---

## **1. VirtualBox Issues**

### **1.1 Virtual Machine Not Starting**
- **Cause**: Virtualization is not enabled on the host machine.
- **Solution**:
  1. Check if virtualization is enabled in the BIOS/UEFI.
  2. Restart your computer, enter the BIOS/UEFI setup, and enable **Intel VT-x** or **AMD-V**.
  3. Save changes and restart.

### **1.2 Network Issues in Virtual Machines**
- **Cause**: Incorrect network adapter settings.
- **Solution**:
  1. Open VirtualBox, select the VM, and go to **Settings > Network**.
  2. Ensure the adapter is set to **Bridged Adapter**.
  3. Restart the VM after making changes.

---

## **2. Active Directory Setup Issues**

### **2.1 Cannot Promote Server to Domain Controller**
- **Cause**: Incorrect DNS settings or missing roles/features.
- **Solution**:
  1. Ensure the **Active Directory Domain Services** role is installed.
  2. Set the **Preferred DNS Server** to the server’s own IP address.
  3. Reboot the server and retry the promotion.
     
---

## **3. Splunk Issues**

### **4.1 Splunk Web Interface Not Loading**
- **Cause**: Splunk service is not running or incorrect firewall rules.
- **Solution**:
  1. Ensure the Splunk service is running:
     ```bash
     sudo systemctl start splunk
     ```
  2. Check if the firewall allows the default port (8000):
     ```bash
     sudo ufw allow 8000
     ```

### **3.2 Logs Not Ingesting into Splunk**
- **Cause**: Incorrect configuration in [inputs.conf](https://github.com/Divyansh121699/ActiveDirectory-HomeLab/blob/main/configs/splunk-inputs.md) or [outputs.conf](https://github.com/Divyansh121699/ActiveDirectory-HomeLab/blob/main/configs/splunk-outputs.md).
- **Solution**:
  1. Verify the file paths in `inputs.conf`.
  2. Restart Splunk to apply changes:
     ```bash
     sudo systemctl restart splunk
     ```

---

## **4. Kali Linux Issues**

### **5.1 Cannot Connect to Target Machines**
- **Cause**: Firewall or network misconfiguration.
- **Solution**:
  1. Ensure the target machine is reachable by pinging its IP address.
  2. Check if the target machine’s firewall allows the required ports.

### **5.2 Brute Force Attack Failing**
- **Cause**: Incorrect username or password list.
- **Solution**:
  1. Verify the username used in the attack matches an existing domain user.
  2. Use a comprehensive password list, such as `rockyou.txt`.

---

## **5. Telemetry and Logging Issues**

### **5.1 Telemetry Not Generating in Sysmon**
- **Cause**: Sysmon is not properly configured or running.
- **Solution**:
  1. Verify Sysmon is installed:
     ```bash
     sysmon -c
     ```
  2. Reapply the Sysmon configuration:
     ```bash
     sysmon -accepteula -i sysmon-config.xml
     ```

### **5.2 Logs Missing in Splunk**
- **Cause**: Incorrect log forwarding or indexing configuration.
- **Solution**:
  1. Verify the Universal Forwarder is configured correctly on the client machines.
  2. Check Splunk’s index settings for errors.

---

## **6. General Tips**
- **Check Logs**: Review logs for error messages:
  - AD logs: `Event Viewer > Windows Logs > System`.
  - Splunk logs: `/opt/splunk/var/log/splunk/`.
- **Google It**: Many common issues have solutions on forums like Stack Overflow or Reddit.
- **Ask for Help**: If you’re stuck, leave a comment in the project repository or related forums.

---
