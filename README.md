# Pentest Lab

This repository documents my work and findings from penetration testing, incident response practice, and honeypot setups. The goal is to demonstrate my skills as a cybersecurity analyst and to showcase various security tools and configurations.

## Projects

### 1. **Cowrie Honeypot Setup**

In this project, I set up a **Cowrie Honeypot** on Azure using Docker. The honeypot listens for SSH brute-force attempts and logs malicious activities. The goal is to capture attack patterns and gain insights into the methods used by attackers.

#### Steps for Cowrie Honeypot Setup:
1. **Install Docker** on the VM.
2. **Pull the official Cowrie Docker image** and run it in a container.
3. **Configure Azure Network Security Group (NSG)** to allow inbound traffic on port `2222` for SSH.
4. **Test the honeypot** by SSHing into the VM.

[Read the detailed setup guide](docs/cowrie-setup.md).

#### Screenshots of Cowrie Logs and Activity:
Here are some screenshots capturing the logs and activity of the Cowrie honeypot.
- **[Cowrie Logs](screenshots/cowrie-setup-logs/)**: View the logs of SSH login attempts.

### 2. **Incident Response Practice**
This section will contain a series of incident response exercises, including handling data breaches, logging, and analyzing attacks. As the project progresses, I will document the steps I take to handle and mitigate security incidents.

#### NIST 800-61 Guidelines for Incident Handling:
I will use the **NIST 800-61** guidelines for handling and documenting incidents in this section. It includes strategies for detecting, analyzing, and responding to security breaches.

## Folder Structure

pentest-lab/
│
├── docs/ # General documentation
│ ├── cowrie-setup.md # Documentation for setting up Cowrie
│ └── incidents.md # (Future) Document incidents observed on Cowrie
│
├── screenshots/ # Screenshots related to the setup
│ └── cowrie-setup-logs/ # Screenshots of the Cowrie honeypot logs
│
├── cowrie/ # Any configuration files or additional resources for Cowrie
└── README.md # Overview and links to all documentation

yaml
Copy code

## Technologies Used
- **Docker** for running the Cowrie honeypot in a container.
- **Azure** for hosting the virtual machine.
- **Cowrie** for SSH honeypot functionality.
- **NIST 800-61** for incident response practice guidelines.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

### Future Plans:
- Add more honeypots or intrusion detection systems for practice.
- Document incidents and responses for better incident handling practice.
- Simulate and analyze more attack vectors like SQL injection, XSS, etc., and showcase defense mechanisms.

---

**Contact Information**:  
For any questions or feedback, feel free to reach out via my GitHub profile or email.
