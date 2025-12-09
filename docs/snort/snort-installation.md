# Snort Installation on Ubuntu 24.04

This document outlines the steps I followed to install and configure Snort on my Ubuntu 24.04 system for intrusion detection.

## Prerequisites

First, I made sure my system was up-to-date by running the following commands:
```bash
sudo apt update && sudo apt upgrade -y
Step 1: Install Dependencies
I installed the necessary dependencies required for Snort to run:

bash
Copy code
sudo apt install -y build-essential autotools-dev libpcap-dev libpcre3-dev libdumbnet-dev libluajit-5.1-dev libdaq-dev libssl-dev zlib1g-dev liblzma-dev
Step 2: Download and Install Snort
2.1: Download Snort
Next, I downloaded Snort from the official website using the following command:

bash
Copy code
wget https://www.snort.org/downloads/snort/snort-2.9.20.tar.gz
2.2: Extract and Build Snort
After the download was complete, I extracted the file and started building Snort:

bash
Copy code
tar -xvzf snort-2.9.20.tar.gz
cd snort-2.9.20
To configure and install Snort, I ran these commands:

bash
Copy code
./configure --enable-sourcefire
make
sudo make install
2.3: Verify the Installation
To verify that Snort was installed correctly, I checked its version:

bash
Copy code
snort -V
Step 3: Install Snort Rules
Snort needs rules to detect threats. I installed the default Snort rules with this command:

bash
Copy code
sudo apt install -y snort snort-common snort-rules-default
Step 4: Configure Snort
4.1: Define Network Variables
I edited the snort.conf file to define my network variables. Here's how I did it:

bash
Copy code
sudo nano /etc/snort/snort.conf
I found and set the following variables:

bash
Copy code
ipvar HOME_NET [Your Network Address]
ipvar EXTERNAL_NET !$HOME_NET
4.2: Create a Local Rule File
Next, I created a custom rule file to test Snort. I added the following ICMP test rule:

bash
Copy code
sudo bash -c 'cat > /etc/snort/rules/local.rules <<EOF
alert icmp any any -> \$HOME_NET any (msg:"ICMP test"; sid:1000001; rev:1;)
EOF'
4.3: Update snort.conf to Include Local Rules
I included the local rule file in the snort.conf file by appending the following line:

bash
Copy code
sudo bash -c 'echo "include \$RULE_PATH/local.rules" >> /etc/snort/snort.conf'
Step 5: Test Snort
5.1: Run Snort in Console Mode
To run Snort and monitor the traffic, I used the following command:

bash
Copy code
sudo snort -A console -q -c /etc/snort/snort.conf -i lo
5.2: Generate Traffic for Testing
I generated some test traffic using the ping command to make sure Snort would trigger an alert:

bash
Copy code
ping -c 2 127.0.0.1
If everything was set up correctly, Snort generated an alert for the ICMP traffic.

Step 6: Automate Snort to Start at Boot
To make sure Snort starts automatically when the system boots up, I enabled the Snort service:

bash
Copy code
sudo systemctl enable snort
Step 7: Review Snort Alerts
I can view Snort alerts by checking the log files in /var/log/snort/:

bash
Copy code
sudo tail -f /var/log/snort/snort.alert
Troubleshooting
If Snort fails to start, ensure that all configuration paths are correct and that all required files, such as classification.config and snort.conf, are present.

That's it! Snort is now installed and running on my Ubuntu system.
