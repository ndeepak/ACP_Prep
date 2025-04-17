### **Understanding the OWASP API Security Top 10 in Detail**

The **OWASP API Security Top 10** is a project from the **Open Web Application Security Project (OWASP)**, which highlights the most critical security risks in **Application Programming Interfaces (APIs)**. APIs are crucial for modern applications but introduce unique security challenges. This list, first released in **2019** and updated in **2023**, helps organizations identify and mitigate security vulnerabilities in their APIs.

---
## **📌 Why Was OWASP API Security Top 10 Created?*

1. **Rapid Growth of APIs**    
    - APIs have become the backbone of modern applications, enabling easy communication between different services.        
    - Instead of building everything from scratch, businesses integrate APIs (e.g., for payments, maps, authentication, etc.).        
    - This widespread adoption increases the **attack surface** for malicious actors.        
2. **Security Gaps in API Development**    
    - Traditional **network security tools, web vulnerability scanners, and firewalls** were **not designed** for APIs.        
    - Many APIs expose **sensitive data** without proper security controls.        
    - Attackers **bypass traditional security** and directly target exposed APIs.        
3. **APIs as a Primary Attack Vector**    
    - Hackers no longer need to **hack into networks**—they can directly interact with APIs to **extract data, manipulate systems, or disrupt services** rather than following traditional Kill chain.
    - Security controls such as **firewalls and intrusion detection systems** are often **bypassed** in API attacks.        
    - As a result, **API attacks have become one of the biggest security threats**.

---
## **📌 How Is the OWASP API Security Top 10 Compiled?**
The **2023 version** of the list was compiled using:
- **Bug bounty reports** from platforms like HackerOne & Bugcrowd.    
- **Publicly available security incident reports.**    
- **News about API security breaches** (e.g., LinkedIn, Venmo, Peloton leaks).    
- **Internal research** by OWASP members.

🛑 **Challenges in compiling data:**
- **Bug bounties** focus on specific security weaknesses on certain types of findings only.
- Lack of full details
- **Not all API security incidents are reported publicly.**    
- **Incomplete technical details** from security news reports.    
Sources:
https://github.com/devanshbatham/Awesome-Bugbounty-Writeups
https://pentester.land/writeups/
https://hackerone.com/hacktivity/

---
# **🛠️ OWASP API Security Top 10 (2023) - Detailed Breakdown**

![[2019-2023owaspapi.png]]
### **🚨 API1:2023 - Broken Object Level Authorization (BOLA)**
- **What is it?**
    - API does not properly check **user permissions**, allowing unauthorized access to data.
- **Example:**    
    - A hacker changes `user_id=1234` in an API request to `user_id=5678` and retrieves another user’s data.
- **Mitigation:**    
    - **Enforce object-level access control** for every request.        
    - Implement **strong authentication and authorization checks**.
---
### **🚨 API2:2023 - Broken Authentication**
- **What is it?**    
    - Weak API authentication allows attackers to impersonate users.        
- **Example:**    
    - Missing **rate limiting** allows brute force attacks on API login endpoints.        
    - API tokens **never expire**, making them easy to steal and use.        
- **Mitigation:**    
    - Use **OAuth 2.0** and secure **JWT tokens**.        
    - **Rotate API keys periodically**.        
    - Enable **multi-factor authentication (MFA)**.        
---
### **🚨 API3:2023 - Broken Object Property Level Authorization**
- **What is it?**    
    - API allows users to **read or modify** object properties they shouldn’t have access to.        
- **Example:**    
    - A user sends an API request to change their **account type from "basic" to "admin"**, gaining admin privileges.        
- **Mitigation:**    
    - Implement **strict access control** at the property level.        
    - Validate **user input** to prevent modification of restricted fields.
---
### **🚨 API4:2023 - Unrestricted Resource Consumption**
- **What is it?**
    - Attackers overload the API by sending too many requests, causing a **denial of service (DoS)**.        
- **Example:**    
    - API allows unlimited **file uploads**, leading to **server crashes**.        
    - **No rate limiting** allows spamming of API endpoints.        
- **Mitigation:**    
    - Implement **rate limiting and quotas** (e.g., **1000 requests per hour per user**).        
    - Set **file size limits** on uploads.       

---
### **🚨 API5:2023 - Broken Function Level Authorization**
- **What is it?**    
    - Unauthorized users can access **privileged API functions**.        
- **Example:**    
    - An attacker calls an admin-only API endpoint (`/api/deleteUser`) and deletes another user's account.        
- **Mitigation:**    
    - Implement **role-based access control (RBAC)**.        
    - Secure **admin and privileged APIs** separately.        
---
### **🚨 API6:2023 - Unrestricted Access to Sensitive Business Flows**
- **What is it?**    
    - APIs expose **critical business processes** without security controls.        
- **Example:**    
    - An attacker **automates thousands of API requests** to **bulk-purchase** limited-edition products before real users can.
        
- **Mitigation:**    
    - Add **CAPTCHAs** and **transaction limits** for sensitive operations.
---
### **🚨 API7:2023 - Server-Side Request Forgery (SSRF)**
- **What is it?**    
    - API fetches data from an **untrusted user input URL**, allowing access to **internal services**.    
- **Example:**    
    - API accepts **arbitrary URLs** and forwards requests to **internal company systems**.
- **Mitigation:**    
    - Validate **all user-supplied URLs**.        
    - Use **allowlists** instead of blocklists.

---
### **🚨 API8:2023 - Security Misconfiguration**
- **What is it?**    
    - API uses **default settings, debug modes, or exposes sensitive information**.
- **Example:**    
    - API response contains **detailed error messages** with database credentials.
- **Mitigation:**    
    - Disable **verbose error messages** in production.        
    - Regularly **audit API configurations**.
---
### **🚨 API9:2023 - Improper Inventory Management**
- **What is it?**
    - Organizations **fail to track API versions, endpoints, and exposed data**.
- **Example:**    
    - A deprecated **API version** remains active and vulnerable.
- **Mitigation:**    
    - Maintain an **up-to-date API inventory**.        
    - Decommission **old and unused APIs**.
---
### **🚨 API10:2023 - Unsafe Consumption of APIs**
- **What is it?**    
    - API **trusts data** from external sources without verification.        
- **Example:**    
    - API **relies on a third-party API** without validating responses, leading to **data injection attacks**.        
- **Mitigation:**
    - Validate **all incoming API data**.
    - Use **secure API integration** techniques.
---
## **🛡️ How to Secure Your APIs?**
1. **Use Authentication & Authorization:**
    - Implement **OAuth 2.0, JWT, and API keys securely**.        
2. **Apply Rate Limiting:**    
    - Prevent brute-force and **denial-of-service (DoS) attacks**.        
3. **Secure API Endpoints:**    
    - Disable unnecessary **public endpoints**.        
4. **Implement Logging & Monitoring:**    
    - Detect attacks in **real time**.        
5. **Use API Gateways & Firewalls:**    
    - **Filter, authenticate, and monitor** API traffic.
---
## **🚀 Real-World API Breaches**
📌 **LinkedIn API Data Leak (2021)**
- Exposed **700 million user records** due to improper API access.

📌 **Peloton API Security Flaw (2021)**
- Allowed attackers to access **user profile data** without authentication.

📌 **Toyota API Exposure (2022)**
- A misconfigured API **exposed customer personal information**.
---

## Mapped to External Sources
The OWASP API Security risks are associated with references to external sources. These sources include Common Weakness Enumeration (CWE), other OWASP projects, and National Institute of Standards and Technology (NIST) guidance. Most of the references involve CWEs. CWEs are a list of common software and hardware vulnerabilities developed by the community and hosted by MITRE. Each CWE is identified by a unique identifier or CWE-ID. This identifier can be used to refer back to a specific vulnerability.

|   |   |
|---|---|
|**OWASP Top 10**|**External Reference**|
|API1:2023 Broken Object Level Authorization|- [CWE-285: Improper Authorization](https://cwe.mitre.org/data/definitions/285.html)<br>- [CWE-639: Authorization Bypass Through User-Controlled Key](https://cwe.mitre.org/data/definitions/639.html)|
|API2:2023 Broken Authentication|- [CWE-204: Observable Response Discrepancy](https://cwe.mitre.org/data/definitions/204.html)<br>- [CWE-307: Improper Restriction of Excessive Authentication Attempts](https://cwe.mitre.org/data/definitions/307.html)|
|API3:2023 Broken Object Property Level Authorization|- [CWE-213: Exposure of Sensitive Information Due to Incompatible Policies](https://cwe.mitre.org/data/definitions/213.html)<br>- [CWE-915: Improperly Controlled Modification of Dynamically-Determined Object Attributes](https://cwe.mitre.org/data/definitions/915.html)<br>- [API3:2019 Excessive Data Exposure - OWASP API Security Top 10 2019](https://github.com/OWASP/API-Security/blob/master/2019/en/src/0xa3-excessive-data-exposure.md)<br>- [API6:2019 - Mass Assignment - OWASP API Security Top 10 2019](https://github.com/OWASP/API-Security/blob/master/2019/en/src/0xa6-mass-assignment.md)|
|API4:2023 Unrestricted Resource Consumption|- [CWE-770: Allocation of Resources Without Limits or Throttling](https://cwe.mitre.org/data/definitions/770.html)<br>- [CWE-400: Uncontrolled Resource Consumption](https://cwe.mitre.org/data/definitions/400.html)<br>- [CWE-799: Improper Control of Interaction Frequency](https://cwe.mitre.org/data/definitions/799.html)<br>- [NIST Security Strategies for Microservices-based Application Systems](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-204.pdf)|
|API5:2023 Broken Function Level Authorization|- [CWE-285: Improper Authorization](https://cwe.mitre.org/data/definitions/285.html)<br>- [OWASP Top 10 2013: A7: Missing Function Level Access Control](https://github.com/OWASP/Top10/raw/master/2013/OWASP%20Top%2010%20-%202013.pdf)<br>- [OWASP Guidance: Forced Browsing](https://owasp.org/www-community/attacks/Forced_browsing)<br>- [OWASP Guidance: Access Control](https://owasp.org/www-community/Access_Control)|
|API6:2023 Unrestricted Access to Sensitive Business Flows|- [API10:2019 Insufficient Logging & Monitoring](https://owasp.org/API-Security/editions/2019/en/0xaa-insufficient-logging-monitoring/)<br>- [OWASP Automated Threats to Web Applications](https://owasp.org/www-project-automated-threats-to-web-applications/)|
|API6:2023 Server Side Request Forgery|- [CWE-918: Server-Side Request Forgery (SSRF)](https://cwe.mitre.org/data/definitions/918.html)<br>- [URL confusion vulnerabilities in the wild: Exploring parser inconsistencies, Snyk](https://snyk.io/blog/url-confusion-vulnerabilities/)<br>- [Server Side Request Forgery](https://owasp.org/www-community/attacks/Server_Side_Request_Forgery)<br>- [Server-Side Request Forgery Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Server_Side_Request_Forgery_Prevention_Cheat_Sheet.html)|
|API8:2023 Security Misconfiguration|- [CWE-2: Environmental Security Flaws](https://cwe.mitre.org/data/definitions/2.html)<br>- [CWE-16: Configuration](https://cwe.mitre.org/data/definitions/16.html)<br>- [CWE-209: Generation of Error Message Containing Sensitive Information](https://cwe.mitre.org/data/definitions/209.html)<br>- [CWE-319: Cleartext Transmission of Sensitive Information](https://cwe.mitre.org/data/definitions/319.html)<br>- [CWE-388: Error Handling](https://cwe.mitre.org/data/definitions/388.html)<br>- [CWE-444: Inconsistent Interpretation of HTTP Requests ('HTTP Request/Response Smuggling')](https://cwe.mitre.org/data/definitions/444.html)<br>- [CWE-942: Permissive Cross-domain Policy with Untrusted Domains](https://cwe.mitre.org/data/definitions/942.html)<br>- [NIST Guide to General Server Security](https://csrc.nist.gov/publications/detail/sp/800-123/final)<br>- [Let's Encrypt: a free, automated, and open Certificate Authority](https://letsencrypt.org/)<br>- [OWASP Secure Headers Project](https://owasp.org/www-project-secure-headers/)<br>- [Configuration and Deployment Management Testing - Web Security Testing Guide](https://owasp.org/www-project-web-security-testing-guide/latest/4-Web_Application_Security_Testing/02-Configuration_and_Deployment_Management_Testing/README)<br>- [Testing for Error Handling - Web Securi](https://owasp.org/www-project-web-security-testing-guide/latest/4-Web_Application_Security_Testing/08-Testing_for_Error_Handling/README)|
|API9:2023 Improper Inventory Management|- [CWE-1059: Incomplete Documentation](https://cwe.mitre.org/data/definitions/1059.html)|
|API10:2023 Unsafe Consumption of APIs|- [CWE-285: Improper Authorization](https://cwe.mitre.org/data/definitions/285.html)<br>- [CWE-639: Authorization Bypass Through User-Controlled Key](https://cwe.mitre.org/data/definitions/639.html)|

---
## 🔥 **Why Was the List Updated?**
- **API usage has skyrocketed**: More APIs are being developed, increasing the attack surface.    
- **API attacks are increasing**: Akamai reported **114 million API attacks in a single day** in 2021.    
- **New API technologies have emerged**: The way APIs are designed and used has changed.    
- **Financial impact is higher**: The global API market is projected to grow **20x in 10 years**.
---
## 🔄 **Key Changes from 2019 to 2023**
### **❌ Two Risks Were Removed**
1. **Injection (API8:2019)**    
    - Still relevant, but **mitigation techniques** like Web Application Firewalls (WAFs) have reduced major attacks.        
2. **Insufficient Logging & Monitoring (API10:2019)**    
    - Important for security but **not a major direct attack vector** in API breaches.
### **✅ Three Risks Remained Unchanged**
1. **Broken Object Level Authorization (BOLA) – API1**
    - Most **common API vulnerability** and responsible for many breaches.
2. **Broken Function Level Authorization (BFLA) – API5**    
    - APIs still **fail to differentiate permissions properly** at function levels.        
3. **Security Misconfiguration – API8**    
    - APIs are often **deployed with default or weak security settings**.
### **🔄 Four Risks Were Renamed**
1. **Broken User Authentication → Broken Authentication (API2)**
    - Now **covers authentication failures for APIs beyond just users** (e.g., service-to-service authentication).
2. **Improper Assets Management → Improper Inventory Management (API9)**    
    - Broader term covering **all API components**, including endpoints and dependencies.        
3. **Excessive Data Exposure & Mass Assignment → Broken Object Property Level Authorization (API3)**
    - **Combines two risks** into one category that deals with unauthorized access to object properties.        
4. **Lack of Resources & Rate Limiting → Unrestricted Resource Consumption (API4)**    
    - Expands to cover **all resource consumption issues**, not just rate limiting.
### **🆕 Five New Risks Added**
1. **Server-Side Request Forgery (SSRF) – API7**    
    - **APIs making requests to internal services can be exploited** (e.g., attackers force APIs to request sensitive internal URLs).        
2. **Unsafe Consumption of APIs – API10**    
    - APIs consuming **untrusted third-party APIs** without validation can introduce security risks.   
3. **Broken Object Property Level Authorization (BOPLA) – API3**    
    - **A more granular version of BOLA**, focusing on unauthorized access to specific object properties.        
4. **Unrestricted Access to Sensitive Business Flows – API6**    
    - Attackers can **abuse business logic flaws** (e.g., bypassing payment verification in e-commerce APIs).        
5. **Unrestricted Resource Consumption – API4**    
    - APIs **lacking limits** on requests, CPU, or memory usage can be exploited for **DoS (Denial of Service) attacks**.
        

---

## 📊 **Risk Scores Comparison (2019 vs. 2023)**
![[riskratingapi.png]]
Each risk is evaluated based on:
- **Exploitability** (How easy is it to attack?)    
- **Prevalence** (How common is the vulnerability?)    
- **Detectability** (How easy is it for an attacker to find?)    
- **Technical Impact** (How severe is the impact?)

#### RISK = Likelihood * Impact
### **2019 Top Risks**

|Risk|Exploitability|Prevalence|Detectability|Technical Impact|Overall Score|
|---|---|---|---|---|---|
|**API1: Broken Object Level Authorization**|3|3|2|3|**11**|
|**API2: Broken User Authentication**|3|2|2|3|**10**|
|**API3: Excessive Data Exposure**|3|2|2|2|**9**|
|**API4: Lack of Resources & Rate Limiting**|2|3|3|2|**10**|
|**API5: Broken Function Level Authorization**|3|2|1|2|**8**|
|**API6: Mass Assignment**|2|2|2|2|**8**|
|**API7: Security Misconfiguration**|3|3|3|2|**11**|
|**API8: Injection**|3|2|3|3|**11**|
|**API9: Improper Assets Management**|3|3|2|2|**10**|
|**API10: Insufficient Logging & Monitoring**|2|3|1|2|**8**|

---

### **2023 Top Risks**

|Risk|Exploitability|Prevalence|Detectability|Technical Impact|Overall Score|
|---|---|---|---|---|---|
|**API1: Broken Object Level Authorization (BOLA)**|3|3|3|2|**11**|
|**API2: Broken Authentication**|3|2|3|3|**11**|
|**API3: Broken Object Property Level Authorization (BOPLA)**|3|2|3|2|**10**|
|**API4: Unrestricted Resource Consumption**|2|3|3|3|**11**|
|**API5: Broken Function Level Authorization (BFLA)**|3|2|3|3|**11**|
|**API6: Unrestricted Access to Sensitive Business Flows**|3|3|2|2|**10**|
|**API7: Server Side Request Forgery (SSRF)**|3|2|3|2|**10**|
|**API8: Security Misconfiguration**|3|3|3|3|**12**|
|**API9: Improper Inventory Management**|3|3|2|2|**10**|
|**API10: Unsafe Consumption of APIs**|3|2|2|3|**10**|

---

## 🏆 **Key Takeaways**
1. **Authorization issues (BOLA, BOPLA, BFLA) remain the biggest risks.**    
    - They continue to **account for the most API breaches**.        
2. **New risks focus on API-to-API interactions (SSRF, Unsafe Consumption).**    
    - Many modern apps rely on **third-party APIs**, which can introduce new vulnerabilities.        
3. **Unrestricted resource consumption (API4) is now a priority.**    
    - APIs without limits can **be exploited for denial-of-service (DoS) attacks**.        
4. **Security misconfigurations remain a major issue.**    
    - **Misconfigured authentication, missing rate limits, and exposed APIs** continue to be exploited.        
---
## 🚀 **What’s Next?**
- Understand **how attackers exploit these vulnerabilities**.    
- Implement **secure authentication and authorization** for APIs.    
- Enforce **rate limits and resource restrictions**.    
- Monitor **API logs for anomalies**.    
- Secure **API-to-API communication** and **validate third-party APIs**.