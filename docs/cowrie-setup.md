# Cowrie Honeypot Setup

## Overview
In this section, we set up Cowrie, a popular SSH and Telnet honeypot designed to log interactions and gather intelligence on attackers. This is part of a larger cybersecurity lab to practice incident response and honeypot monitoring.

## Prerequisites
- Azure VM set up with Ubuntu 24.04
- Docker installed on the VM

## Step 1: Install Docker
We started by installing Docker on the VM:
```bash
sudo apt update
sudo apt install -y docker.io
Step 2: Pull Cowrie Docker Image
Next, we pulled the official Cowrie Docker image:

bash
Copy code
sudo docker pull cowrie/cowrie
Step 3: Set Up Cowrie Data Directory
A persistent storage directory for Cowrie data was created:

bash
Copy code
mkdir -p ~/cowrie_data
Step 4: Run Cowrie Using Docker
We ran Cowrie in a Docker container, mapping port 2222 for SSH access:

bash
Copy code
sudo docker run -d -p 2222:2222 -v ~/cowrie_data:/cowrie/data cowrie/cowrie
Step 5: Network Security Group Configuration
We updated the Azure Network Security Group (NSG) to allow inbound traffic on port 2222:

Go to Network Security Group > Inbound security rules.

Add a rule allowing TCP traffic on port 2222.

Step 6: Test SSH Access
To test the honeypot, we tried SSHing into the VM on port 2222 using the command:

bash
Copy code
ssh -p 2222 cowrie@20.168.117.173
