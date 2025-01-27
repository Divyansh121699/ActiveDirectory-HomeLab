# Active Directory Home Lab Project

This repository contains resources, guides, and configuration files to set up an Active Directory-based home lab environment. The project simulates real-world scenarios for both Blue Team (defensive security) and Red Team (offensive security) practices using tools like Splunk, Sysmon, Kali Linux, and Atomic Red Team.

---

## **1. Overview**

The project covers:
- Setting up Active Directory on a Windows Server and promoting it to a domain controller.
- Configuring Splunk for monitoring and telemetry.
- Installing and configuring Sysmon for detailed event logging.
- Simulating attacks with Kali Linux and Atomic Red Team.
- Troubleshooting common issues.

---

## **2. Folder Structure**

### **Configuration Files**
- **[Sysmon Configuration File](configs/sysmon-config.xml)**: Sysmon rules for monitoring malicious behaviors.
- **[Splunk Outputs.conf](configs/splunk-outputs.md)**: Configuration for Splunk forwarding.
- **[Splunk Inputs.conf](configs/splunk-inputs.md)**: Configuration for event log ingestion.

### **Guides and Documentation**
- **[Setup Guide](docs/setup-guide.md)**: Step-by-step instructions for setting up the home lab environment.
- **[Splunk Setup](docs/Splunk-setup.md)**: Detailed guide to configuring Splunk on an Ubuntu server.
- **[Splunk Universal Forwarder & Sysmon Setup](docs/Splunk%20Universal%20Forwarder%20&%20Sysmon%20Setup.md)**: Guide for installing and configuring Sysmon and Splunk Universal Forwarder.
- **[Kali Linux Attacks & Atomic Red Team Guide](docs/Kali%20Linux%20attacks%20%26%20Atomic%20Red%20Team%20guide.md)**: Steps for simulating attacks and analyzing telemetry.
- **[Active Directory Setup Guide](docs/AD-Setup.md)**: Instructions for configuring Active Directory and joining client machines to the domain.
- **[Troubleshooting Guide](docs/troubleshooting.md)**: Solutions to common issues encountered during the setup process.

### **Network Diagram**
**![Active Directory Network Diagram](https://github.com/Divyansh121699/ActiveDirectory-HomeLab/blob/main/docs/Active%20Directory%20Network%20Diagram.png)**

---

## **3. Key Features**
- **Blue Team Focus**:
  - Configure Splunk and Sysmon for monitoring.
  - Analyze telemetry from simulated attacks.
- **Red Team Focus**:
  - Simulate brute force attacks and persistence techniques using Kali Linux and Atomic Red Team.
- **Hands-On Learning**:
  - Experiment in a safe, controlled lab environment.
  - Practice troubleshooting real-world issues.

---

## **4. Setup Instructions**
1. Follow the **[Setup Guide](docs/setup-guide.md)** to install virtual machines and configure the network.
2. Install and configure Splunk by referencing the **[Splunk Setup Guide](docs/Splunk-setup.md)**.
3. Configure Sysmon and Splunk Universal Forwarder using the **[Sysmon Setup Guide](docs/Splunk%20Universal%20Forwarder%20%26%20Sysmon%20Setup.md)**.
4. Set up and use Kali Linux for attack simulations as described in the **[Kali Linux Guide](docs/Kali%20Linux%20attacks%20%26%20Atomic%20Red%20Team%20guide.md)**.
5. Configure Active Directory and join client machines using the **[AD Setup Guide](docs/AD-Setup.md)**.

---

## **5. Troubleshooting**
If you encounter issues during setup or operation, consult the **[Troubleshooting Guide](docs/troubleshooting.md)** for solutions to common problems.

---

## **6. References**
- [Splunk Documentation](https://docs.splunk.com)
- [Sysinternals Sysmon](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon)
- [Kali Linux](https://www.kali.org/docs/)
- [Atomic Red Team](https://github.com/redcanaryco/atomic-red-team)
