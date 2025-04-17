# SSRF
##### [API7:2023 Server Side Request Forgery](https://university.apisec.ai/products/owasp-api-security-top-10-and-beyond/categories/2152492172)
### **Detailed Explanation of API7:2023 - Server-Side Request Forgery (SSRF)**
Server-Side Request Forgery (SSRF) is a vulnerability where an attacker can manipulate an API to send unintended requests to remote or internal resources. If an API allows a user to input a URL and fetch data from that URL without proper validation, attackers can exploit it to access sensitive internal systems, scan networks, or even achieve remote code execution.

---
## **1️⃣ Understanding SSRF**
- **What happens?**  
    An application fetches remote resources based on user input but does not properly validate the URL.
- **Impact:**    
    - Internal network reconnaissance (port scanning, discovering internal services)        
    - Exfiltrating sensitive data (cloud metadata, credentials)        
    - Bypassing firewalls and accessing private APIs        
    - Using the server as a proxy to perform malicious actions        
📌 **Example of SSRF Exploitation:**  
Consider an API that allows users to check the availability of a product by providing a URL:
🔹 **Legitimate request:**
```json
{
  "inventory": "http://store.com/api/v3/inventory/item/12345"
}
```
🔹 **Malicious SSRF request:**
```json
{
  "inventory": "http://localhost/admin/secrets"
}
```
If the server responds with sensitive data from `http://localhost/admin/secrets`, it confirms the SSRF vulnerability.

---
## **2️⃣ Types of SSRF**
### **A) In-Band SSRF**
- The attacker receives a direct response from the target server.    
- **Easy to detect and exploit.**    
🔹 **Example:**
```json
{
  "inventory": "http://localhost/secrets"
}
```
**Response:**
```json
{
  "secret_token": "SecretAdminToken123"
}
```
This confirms that the attacker can access internal data.

---
### **B) Out-of-Band (Blind) SSRF**
- The attacker forces the server to make a request but does not receive a direct response.
- **Harder to detect.**    
- Attackers use external services like **Burp Collaborator** or **Webhook.site** to detect these requests.    
🔹 **Example:**
```json
{
  "inventory": "https://webhook.site/306b30f8-2c9e-4e5d-934d-48426d03f5c0"
}
```
If the webhook logs a request from the server's IP, it confirms the SSRF vulnerability.

---
## **3️⃣ Real-World Attack Scenarios**
### **Scenario 1: Accessing Internal Cloud Metadata**
Many cloud providers have a metadata service at `http://169.254.169.254/latest/meta-data/`.  
An attacker could exploit SSRF to steal instance credentials.
🔹 **Payload:**
```json
{
  "inventory": "http://169.254.169.254/latest/meta-data/"
}
```
If the response contains sensitive cloud credentials, the attacker can escalate access.

---
### **Scenario 2: Port Scanning and Internal Reconnaissance**
Attackers can scan internal services by sending requests to different ports.
🔹 **Payload:**
```json
{
  "inventory": "http://192.168.1.1:22"
}
```
- If the API returns **an error**, port 22 (SSH) might be closed.    
- If the API **takes longer to respond**, the port might be open.
---
### **Scenario 3: Bypassing Firewalls**
Many APIs restrict external access but allow internal access. Attackers can use SSRF to bypass these restrictions.
🔹 **Payload:**
```json
{
  "inventory": "http://internal-api.bank.com/admin"
}
```
- If the request is successful, the attacker gains unauthorized access.
---
## **4️⃣ Preventing SSRF Attacks**
✅ **Whitelist Allowed URLs**  
Only allow requests to pre-approved domains.
`"allowed_origins": ["https://store.com", "https://trusted-service.com"]`
✅ **Deny Requests to Private IP Ranges**  
Block requests to `localhost`, `127.0.0.1`, `169.254.169.254`, and internal IPs (`192.168.x.x`, `10.x.x.x`).
✅ **Use URL Parsers to Prevent Manipulation**  
Attackers may attempt URL obfuscation like:
`http://127.0.0.1@evil.com`
Ensure proper URL parsing to detect such tricks.
✅ **Disable HTTP Redirections**  
Avoid allowing requests that redirect to attacker-controlled domains.
✅ **Monitor API Logs and Rate Limit Requests**  
Use logging and anomaly detection to spot SSRF patterns.
✅ **Use Web Application Firewalls (WAFs)**  
Deploy WAF rules that detect SSRF attempts.

---
## **5️⃣ Tools for Detecting SSRF**
🔹 **Burp Suite** - **Repeater & Collaborator**  
🔹 **Webhook.site** - Detect Blind SSRF  
🔹 **OWASP ZAP** - Fuzzing API inputs  
🔹 **Nmap** - Detect internal port scanning

---
## **6️⃣ Conclusion**
SSRF is a **severe API vulnerability** that allows attackers to manipulate requests and access internal systems. Understanding how SSRF works and implementing **proper input validation and network restrictions** is crucial for API security.

---
SSRF quiz:

**Question 1:**  
✅ **All of the above.**  
SSRF allows attackers to control remote resources retrieved by a server, expose private data, scan internal networks, and use the server as a proxy for malicious activities.

**Question 2:**  
✅ **All of the above.**  
SSRF can be used to bypass security mechanisms, disclose sensitive information, and even cause a Denial-of-Service (DoS) attack.

**Question 3:**  
✅ **Enable X-SSRF Headers**  
There is no such security mechanism as "X-SSRF Headers." The other options are valid preventive measures against SSRF.

**Question 4:**  
✅ **Requires the attacker to find an API endpoint that receives a URI as a parameter and then accesses the provided URI.**  
SSRF occurs when an attacker can manipulate an API to make unauthorized requests to internal or external resources.

**Question 5:**  
✅ **All of the above.**  
A successful SSRF attack can result in internal service enumeration, unauthorized access, firewall bypassing, and turning the server into a proxy for further attacks.

---
## Additional Resources
- [Server Side Request Forgery](https://owasp.org/www-community/attacks/Server_Side_Request_Forgery)
- [Server-Side Request Forgery Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Server_Side_Request_Forgery_Prevention_Cheat_Sheet.html)
- [CWE-918: Server-Side Request Forgery (SSRF)](https://cwe.mitre.org/data/definitions/918.html)
- [URL confusion vulnerabilities in the wild: Exploring parser inconsistencies, Snyk](https://snyk.io/blog/url-confusion-vulnerabilities/)
- [Web Security Academy: SSRF](https://portswigger.net/web-security/ssrf)