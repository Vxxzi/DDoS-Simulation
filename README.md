# DDoS-Simulation
## Objective

Distributed Denial of Service (DDoS) attacks pose a significant threat to online services by overwhelming them with traffic from multiple sources, leading to downtime and disruption. This project will explore effective methods for detecting and responding to DDoS attacks using various tools and techniques. Through practical demonstrations and in-depth analysis, this project aims to equip you with the knowledge and skills necessary to safeguard systems against these malicious threats.


### Pre-requisites
- Basic understanding of networking concepts
- Familiarity with the Linux command line
- Knowledge of common network protocols (HTTP, TCP/IP, etc.)
- A computer with at least 8GB of RAM and 20GB of free disk space
- Virtualization software (VirtualBox, VMware, etc.)

### Lab Set-up and Tools Used
1. **Virtual Machines**:
   - **VM1**: Attacker Machine (Kali Linux)
   - **VM2**: Victim Machine (Ubuntu Server)
   - **VM3**: Monitoring and Response Machine (Ubuntu Desktop with DDoS detection tools)

2. **Network Configuration**:
   - Create a virtual network with all VMs connected.
   - Assign static IPs to each VM for easy identification.

  
### Tools
- **Wireshark**: Network protocol analyzer.
- **tcpdump**: Command-line packet analyzer.
- **DDoSify**: DDoS attack simulation tool.
- **snort**: Network Intrusion Detection System (IDS).
- **fail2ban**: Tool to ban IPs that show malicious signs.
- **netstat**: Network statistics tool.

## Tasks

### Task 1 Simulate a DDoS attack from the attacker machine

**Step 1**: Install DDoSify on the Attacker Machine 
   ```bash
   sudo apt-get update
   sudo apt-get install ddosify
   ```
**Step 2**: Launch a DDoS attack against the Victim Machine.
  ```
  ddosify -t http://<Victim-IP> -n 1000 -c 100
  ```
**Expected Output**
The Victim Machine's web server becomes unresponsive due to high traffic.

### Task 2: Capture Network Traffic
**Step 1***: Install Wireshark and tcpdump on the Monitoring Machine.
```bash
Copy code
sudo apt-get update
sudo apt-get install wireshark tcpdump
```
**Step 2**: Capture traffic using tcpdump.
```bash
Copy code
sudo tcpdump -i eth0 -w ddos-attack.pcap
```
Expected Output: A pcap file (ddos-attack.pcap) is created with the captured network traffic.

### Task 3: Analyze Traffic with Wireshark

**Step 1**: Open the captured pcap file in Wireshark.
```bash
wireshark ddos-attack.pcap
```
**Step 2**: Identify the IP addresses with the most traffic.

Expected Output: A list of IP addresses generating excessive traffic.

### Task 4: Detect DDoS Attack with Snort

**Step 1**: Install Snort on the Monitoring Machine.
```bash
Copy code
sudo apt-get update
sudo apt-get install snort
```
**Step 2**: Configure Snort to detect DDoS attacks.
Edit the Snort configuration file /etc/snort/snort.conf to include DDoS detection rules.

**Step 3**: Run Snort in IDS mode.
```bash
sudo snort -A console -q -c /etc/snort/snort.conf -i eth0
```
Expected Output: Snort alerts for potential DDoS attack patterns.

### Task 5: Mitigate DDoS Attack with fail2ban

**Step 1**: Install fail2ban on the Victim Machine.
```bash
sudo apt-get update
sudo apt-get install fail2ban
```
**Step 2**: Configure fail2ban to detect and ban IPs causing a DDoS attack.
Edit the configuration file /etc/fail2ban/jail.local to include rules for banning IPs with excessive connections.
```ini
[http-get-dos]
enabled = true
port = http,https
filter = http-get-dos
logpath = /var/log/apache2/access.log
maxretry = 300
findtime = 300
bantime = 3600
```
**Step 3**: Restart fail2ban.
```bash
sudo systemctl restart fail2ban
```

Expected Output: IPs generating excessive requests are banned, mitigating the DDoS attack.


drag & drop screenshots here or use imgur and reference them using imgsrc

Every screenshot should have some text explaining what the screenshot is about.

Example below.

*Ref 1: Network Diagram*

### Skills Learned

- Understanding the fundamentals of DDoS attacks and their impact on online services.
- Proficiency in using various tools for monitoring and detecting unusual traffic patterns.
- Implementing effective strategies for incident response during a DDoS attack.
- Analysing attack vectors and identifying potential vulnerabilities in systems.
- Developing and configuring protective measures, such as rate limiting and traffic filtering.
- Gaining hands-on experience in real-time threat assessment and mitigation techniques.

