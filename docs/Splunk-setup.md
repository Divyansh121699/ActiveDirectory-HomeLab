# Splunk Setup Guide on Ubuntu Server

This guide walks you through the steps to set up Splunk on an Ubuntu Server for monitoring and analyzing telemetry data.

---

## **1. Prerequisites**
Before you begin, ensure the following:
- Ubuntu Server (20.04 or newer) installed and running.
- Access to a terminal with sudo privileges.
- Internet connection to download Splunk.

---

## **2. Step-by-Step Setup**

### **Step 1: Update System Packages**
Update the package repository and upgrade existing packages:
```bash
sudo apt update && sudo apt upgrade -y
```
### **Step 2: Edit the netplan configuration**
```bash
sudo nano /etc/netplan/50-cloud-init.yaml
```
1. Replace the content of 50-cloud-init.yaml with:
```
network:
  ethernets:
    eth0:
      dhcp4: false
      addresses: [192.168.1.190/24]
      gateway4: 192.168.1.1
      nameservers:
        addresses: [8.8.8.8]
  version: 2
```
2. Apply changes:
```bash
sudo netplan apply
```
3. Verify the IP:
```bash
ip a
```
4. Test connectivity:
```bash
ping google.com
```
### **Step 3: Install Splunk on Ubuntu**
Download Splunk
1. Log in to [Splunk](https://www.splunk.com/).
2. Download the `.deb` package for Splunk Enterprise.

Install Splunk
1. Transfer the `.deb` file to the Splunk VM using **Shared Folders**.
2. Install Splunk:
```bash
sudo dpkg -i splunk*.deb
```
Start Splunk
1. Navigate to the Splunk directory:
```bash
cd /opt/splunk/bin
```
2. Start Splunk:
```bash
sudo ./splunk start --accept-license
```
3. Enable Splunk on boot:
```bash
sudo ./splunk enable boot-start
```
### **Step 4: Configure Splunk Server**
Access Splunk Web:
- Navigate to `http://192.168.1.190:8000`.
