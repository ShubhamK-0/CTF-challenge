# CTF-Challenge
CTF Exploitation Breakdown form Recon to Root Shell.

This project involved conducting a complete penetration test on the Darkhole 2 virtual machine downloaded from VulnHub, simulating a real-world offensive security engagement. The objective was to identify, exploit, and document various security flaws in the target system.

We began with thorough network and service enumeration using tools like nmap. From there, multiple vulnerabilities were discovered and exploited—ranging from Git repository leakage, SQL injection to privilege escalation. Each flaw was carefully analyzed with supporting proof-of-concept and risk assessment.

The exploited vulnerabilities were mapped to OWASP Top 10 (Web/API) standards and assigned CVSS scores. The findings were consolidated into a professional vulnerability report that includes mitigation strategies for each issue.

Throughout the project, tools such as Kali Linux and Burp Suite were used for exploitation and post-exploitation. The end result was complete system compromise, from initial foothold to root shell.

This assessment not only validated technical skills across the cyber kill chain but also emphasized the importance of secure development, access control, and configuration management.

# Vulnerability Summery
<img width="1939" height="875" alt="image" src="https://github.com/user-attachments/assets/ff987004-7dac-426a-880a-11ee0d34a683" />
<img width="1954" height="387" alt="image" src="https://github.com/user-attachments/assets/3a3b1ad8-3b9c-4cb4-acdd-225eb208ff81" />

# OWASP Top 10
<img width="1768" height="442" alt="image" src="https://github.com/user-attachments/assets/bb9968d7-7d6f-4c4e-8634-62340d4a8f0b" />

# Open SSH Port (22) Without Restriction

Vulnerability Name: Unrestricted SSH Access (Port 22)
Vulnerability Description: The SSH service running on port 22 is openly accessible from any external IP address without any firewall restrictions. This allows to attempt connections over the network, making the system susceptible to brute-force attacks, enumeration, and exploitation of known vulnerabilities if the SSH service is outdated or misconfigured.
Affected Machine/URL: Darkhole2 – Machine IP: 192.168.139.143 Service: SSH (Port 22)
Severity: High, due to the real exploitation of SSH access using recovered credentials, the lack of IP restriction, and chaining with privilege escalation.
Risk/Impact: The unrestricted exposure of SSH (port 22) on the target machine (192.168.139.143) poses a serious risk. The service is publicly accessible, with no IP-based filtering or firewall protection, allowing any attacker to attempt brute-force login or credential stuffing.
    Access user-level shell through SSH (ssh jehad@192.168.139.143).
    Escalate privileges to root using a misconfigured ‘sudo’ Python binary.
    Create an SSH tunnel to access an internal web service on port.
    Execute a remote reverse shell, leading to full system compromise.
    Capture the final flag, indicating complete attacker control.
<img width="6089" height="628" alt="image" src="https://github.com/user-attachments/assets/fd4743d4-f5d4-4f37-bf47-146bd545a151" />



