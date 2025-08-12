**Subdomain Takeover – Pentest Lab**

This project is a practical demonstration of a **critical Subdomain Takeover vulnerability**, discovered and exploited in a controlled environment.  



**Objective:**
Identify how an attacker could take over parts of the **futurevera.thm** infrastructure and assess the potential risks.



**TOOLS USED:**
Gobuster – Virtual host and subdomain enumeration



**Methodology:**

  1.Subdomain Enumeration with Gobuster

  Use :   gobuster vhost -u https://futurevera.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt -k --append-domain

  Results : -support.futurevera.thm 
            -blog.futurevera.thm
  
  2.Add the sub-domain in /etc/hosts
  
  10.10.XX.XX futurevera.thm  blog.futurevera.thm support.futurevera.thm
  
  3.Discovering the Hidden Subdomain
  
  Access https://support.futurevera.thm in a browser.

  4.Inspect the SSL certificate:

  Click the padlock → View Certificate.

  Check the Subject Alternative Names (SAN) field.

  DNS Name :
  secrethelpdesk934752.support.futurevera.thm

  5.Adding the Hidden Subdomain
  10.10.X.X secrethelpdesk934752.support.futurevera.thm

  6.Access the hidden subdomain in the browser

  
**Vulnerability Analysis:**

Type: Subdomain Takeover via SSL Certificate SAN
Root Cause:
A subdomain (secrethelpdesk934752.support.futurevera.thm) was still listed in the SSL certificate but no longer properly configured on the infrastructure.

**Potential Impact in a Real-World Attack:**

  -Website defacement

  -Phishing campaigns

  -Malware distribution

  -Data theft

**Attack Scenario:**
An attacker could register the abandoned subdomain on a cloud provider (e.g., AWS, GitHub Pages) and host malicious content that appears legitimate.


**Recommendations:**
Remove unused subdomains from SSL certificates.

Use separate certificates for internal services.

Monitor DNS and certificate transparency logs for exposed internal hostnames.

Restrict access to internal services through firewall rules.

**Key Takeaways:**
This lab demonstrates that with only two tools (Gobuster + text editor), it is possible to detect and exploit a high-impact vulnerability.
In cybersecurity, simplicity is often the most effective approach.

            
