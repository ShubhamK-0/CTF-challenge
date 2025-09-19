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

# Mapping against OWASP TOP 10
<img width="1905" height="892" alt="image" src="https://github.com/user-attachments/assets/290bd3cc-26f6-45d4-a133-3d9d075f26bb" />

# Graph (Pie chart): 
<img width="822" height="467" alt="image" src="https://github.com/user-attachments/assets/90418fac-dfad-4f4c-8770-881597bd2e8f" />

# Reconnaissance & Scanning
# Ifconfig:
Identify our own IP address and network interface before starting the attack.
<img width="865" height="307" alt="image" src="https://github.com/user-attachments/assets/5d5ca892-cb1e-4b83-85cd-ad5a4425b386" />

# Netdiscover: 
We scanned the local devices around us to find our target.
<img width="861" height="268" alt="image" src="https://github.com/user-attachments/assets/97205d08-156a-44c3-b781-189c01dfe781" />


Upon locating the target device, we did a port scanning to see available services; using aggressive scan to identify potential exposed vulnerabilities, service versions, and the underlying operating system.

# Nmap:
    nmap -sS -sV --version-all -O --osscan-guess -A -sC -Pn --script vuln -T5 -p 21,22,80 192.168.139.143 -oA /root/Desktop 
<img width="877" height="382" alt="image" src="https://github.com/user-attachments/assets/e4165d1b-26df-4a7f-8aae-7219e367b9cc" />
<img width="768" height="402" alt="image" src="https://github.com/user-attachments/assets/86e17182-90ae-4f0e-a2e3-07285cb86b9f" />

  aggressive scan results 2

We found that port 80 (HTTP) was open and running Apache HTTP Server 2.4.41 on Ubuntu. The scan revealed a web application at /login.php with a potential CSRF vulnerability in a form using the email field.

<img width="768" height="426" alt="image" src="https://github.com/user-attachments/assets/b0b2e8ea-c03a-4beb-9f98-8a8a29315c4d" />

  aggressive scan results 3

One of the most critical discoveries was the presence of a publicly accessible Git repository at /.git/, which is a serious misconfiguration. This Git repo included a commit message indicating changes to login.php, hinting at manual modification and possibly weak development practices.

<img width="867" height="481" alt="image" src="https://github.com/user-attachments/assets/ae3b4dd0-fbab-4b44-b6e1-8799ece9530b" />

  target website 

<img width="867" height="476" alt="image" src="https://github.com/user-attachments/assets/22e3cf1f-186f-480e-95df-106be4b645a1" />

  target website login page

<img width="595" height="502" alt="image" src="https://github.com/user-attachments/assets/e5e4c4c8-0c1e-46d5-93db-684eeadaf94e" />

  git repository on the webpage

Now to target the webpage, we had the login page. Unfortunately, this login page didn’t suffer from SQL injection commands we tried (most probably there was input sanitization) and the source code did not yield any clues. So, we went back to the ‘.git’ repository we found earlier during the nmap scan.
