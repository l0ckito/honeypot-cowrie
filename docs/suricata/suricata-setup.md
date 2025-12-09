# Suricata Setup and Configuration

## 1. Install Suricata

Suricata is an open-source intrusion detection and prevention system. It is used to monitor and analyze network traffic.

### Command:
```bash
sudo apt install suricata


sudo nano /etc/suricata/suricata.yaml

app-layer:
  protocols:
    ssh:
      enabled: yes
      detection-ports:
        - 22
        - 2222

sudo systemctl restart suricata

sudo tail -f /var/log/suricata/suricata.log

