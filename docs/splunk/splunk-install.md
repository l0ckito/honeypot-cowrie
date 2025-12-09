# 📊 Splunk Enterprise Installation and Configuration on Azure VM

This document details the step-by-step process for installing Splunk Enterprise on the Azure VM (honeypot) and configuring the necessary network security rules to enable centralized log monitoring for Cowrie, Snort, and Suricata.

---

## 1. Prerequisites and Network Security Configuration (Azure Portal)

Before installing Splunk, access to the Splunk Web interface (port 8000) must be enabled securely.

| Task | Detail |
| :--- | :--- |
| **VM IP** | `20.168.117.173` |
| **Splunk Web Port** | `TCP 8000` |
| **Access PC IP** | `185.195.236.205` (Parrot PC) |

### 1.1 Azure Network Security Group (NSG) Rule

A highly restrictive inbound security rule was created to allow access to the Splunk web interface only from the designated monitoring machine.

| NSG Field | Setting |
| :--- | :--- |
| **Source** | `IP Addresses` |
| **Source IP addresses/CIDR ranges** | `185.195.236.205/32` |
| **Service** | `Custom` |
| **Destination port ranges** | `8000` |
| **Protocol** | `TCP` |
| **Action** | `Allow` |
| **Name** | `Allow_Splunk_Web_8000` |

---

## 2. Splunk Enterprise Installation (VM Commands)

The following commands were executed on the Azure VM to download and install Splunk Enterprise 10.0.2.

### 2.1 Download the Splunk Debian Package

The direct download link was used to obtain the Debian package, saving it as `splunk-10.0.2-e2d18b4767e9-linux-amd64.deb`.

```bash
wget -O splunk-10.0.2-e2d18b4767e9-linux-amd64.deb "[https://download.splunk.com/products/splunk/releases/10.0.2/linux/splunk-10.0.2-e2d18b4767e9-linux-amd64.deb](https://download.splunk.com/products/splunk/releases/10.0.2/linux/splunk-10.0.2-e2d18b4767e9-linux-amd64.deb)"
2.2 Install the Package
The dpkg command was used to install the downloaded package into the default location (/opt/splunk).

Bash

sudo dpkg -i splunk-10.0.2-e2d18b4767e9-linux-amd64.deb
2.3 Start Splunk and Create Admin Credentials
The service was started for the first time, requiring immediate acceptance of the license and the creation of the administrative login (username and password). The --accept-license flag bypasses the license prompt.

Bash

sudo /opt/splunk/bin/splunk start --accept-license
Note: Ensure the chosen administrator username and password are saved securely.

3. Access Verification
3.1 Access URL
The Splunk Web interface is now accessible from the Parrot PC (185.195.236.205) by navigating to:

[http://20.168.117.173:8000](http://20.168.117.173:8000)
