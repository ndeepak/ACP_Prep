## 🔐 **API Security Landscape – Full Lifecycle Approach**

The security of an API is not just about firewalls or encryption—it starts from design and continues all the way to retirement.

---
### 1️⃣ **API Definition Phase**
This is where API planning and design happen.
#### ✅ **Secure Design**
- Apply **threat modeling** (e.g., STRIDE) to anticipate risks.    
- Use **least privilege**, proper **authentication and authorization**.    
- Avoid exposing sensitive objects or operations unintentionally.    
- Design with **rate limits**, **input validation**, **error handling**, and **data minimization**.    

#### ✅ **Governance**
- Define how APIs should be **documented, deployed, and maintained**.    
- Enforce **naming conventions**, **versioning policies**, and **access control standards**.    

#### ✅ **Policies**
- Create policies for:    
    - **Authentication (OAuth2, JWT)**        
    - **Rate limiting and throttling**        
    - **Encryption (HTTPS, TLS)**        
    - **Data exposure rules**        
- Can be applied via **API Gateways** or **DevSecOps pipelines**.
    
---
### 2️⃣ **Development Phase**
#### ✅ **Code Reviews**
- Peer reviews ensure no **insecure logic**, **leaked credentials**, or **poor error handling**.    
- Focus on **authorization** and **input validation** in code.    

#### ✅ **Static Code Analysis (SAST)**
- Analyze source code for:    
    - **Hardcoded secrets*        
    - **Insecure libraries**        
    - **Unvalidated inputs**        
- Tools: SonarQube, Checkmarx, Semgrep
    
#### ✅ **Composition Analysis (SCA)**
- Check dependencies (open source libs) for known vulnerabilities (e.g., CVEs).    
- Tools: Snyk, OWASP Dependency-Check    

---
### 3️⃣ **Testing Phase**
#### ✅ **Legacy DAST (Dynamic Analysis)**
- Scan the running app/API for:    
    - SQL injection        
    - XSS        
    - Broken Auth        
- Tools: OWASP ZAP, Burp Suite    

#### ✅ **Pen-Testing**
- Manual tests performed by ethical hackers.    
- Validate:    
    - Authorization flaws (BOLA)        
    - Business logic errors        
    - Sensitive data leaks       

#### ✅ **Bug Bounty**
- Invite **external researchers** to find bugs.    
- Platform examples: HackerOne, Bugcrowd    

---

### 4️⃣ **Deployment Phase**
#### ✅ **Web Server**
- Ensure it's **hardened** (disable directory listings, proper TLS certs).    
- Minimize info leakage (headers, verbose error pages).    

#### ✅ **API Gateway**
- Acts as a **security enforcement point**.    
- Handles:    
    - **Authentication*        
    - **Authorization**        
    - **Rate limiting**        
    - **IP whitelisting/blacklisting**        
    - **Logging**        

#### ✅ **WAF / SIEM**
- **Web Application Firewall (WAF)**: Blocks known attack patterns (e.g., SQLi, XSS).    
- **SIEM (Security Info & Event Management)**: Correlates logs and alerts for threat detection (e.g., Splunk, QRadar).    

---
### 5️⃣ **Retirement Phase**
#### ✅ **Governance**
- Ensure deprecated APIs are not used in production.    
- Document and review APIs regularly for relevance.    

#### ✅ **Versioning**
- Use proper version control (e.g., `/v1/`, `/v2/`) to avoid breaking clients.    
- Helps plan smooth transitions.    

#### ✅ **Deprecation**
- Notify consumers about upcoming retirement.    
- Provide timelines, migration paths, and alternatives.    
- Avoid “zombie APIs” (abandoned but still accessible).    

---
## 🧠 Summary Table

| Phase           | Key Security Focuses                         |
| --------------- | -------------------------------------------- |
| **Definition**  | Secure design, governance, policy            |
| **Development** | Code review, SAST, dependency analysis       |
| **Testing**     | DAST, pen-testing, bug bounty                |
| **Deployment**  | Secure server config, API gateway, WAF, SIEM |
| **Retirement**  | Governance, versioning, safe deprecation     |

---
## 🚀 Bonus: [[Three Pillars of API Security]] (Supporting Concept)
1. **Governance** – Policy enforcement, version control, and process standardization.    
2. **Testing** – Continuous, automated, and manual testing to catch flaws.    
3. **Monitoring** – Real-time detection, logging, and alerting via gateways and SIEM.


---
### ✅ **Question 1:**
**Which of the following technologies is NOT commonly associated with application security?**
🔘 **Correct Answer:** **Data Encryption technologies**
🧠 **Reasoning:**  
While data encryption (e.g., TLS, AES) is critical for data security and confidentiality, it is not **specific to application security**.  
On the other hand, **SAST, DAST**, and **API Gateways** are core tools/technologies **explicitly designed** to secure applications.

---

### ✅ **Question 2:**
**Why are APIs less commonly exploited via vulnerabilities like SQL injection or cross-site scripting?**
🔘 **Correct Answer:** **Such vulnerabilities are generally easily detected and fixed**
🧠 **Reasoning:**
- **SQLi and XSS** are classic web application vulnerabilities that are well-known and often mitigated by frameworks, libraries, and scanners.    
- APIs are more prone to **logic-based flaws** like **Broken Object Level Authorization (BOLA)** or **Broken Authentication** than traditional injection flaws.    

---

### ✅ **Question 3:**
**When should security considerations begin during the API lifecycle?**
🔘 **Correct Answer:** **At the API definition phase**
🧠 **Reasoning:**  
Security must be **“shifted left”**—meaning it should begin **as early as possible** in the lifecycle, during **design and planning (API definition)**. This ensures secure design, proper governance, and avoids costly rework later.

---

### ✅ **Question 4:**
**Which of the following is most effective for finding API-specific vulnerabilities during the testing phase?**
🔘 **Correct Answer:** **Automated API-specific security testing**
🧠 **Reasoning:**  
Traditional testing tools may **miss business logic flaws or authorization issues** unique to APIs.  
API-specific tools simulate real API requests and test for:
- BOLA    
- Excessive Data Exposure    
- Improper Rate Limiting  
    Examples: **APIsec, StackHawk, Postman tests with security plugins**
---

### ✅ **Question 5:**
**What is the recommended action when a new API version is published?**
🔘 **Correct Answer:** **Update the version and retire older versions**
🧠 **Reasoning:**  
Keeping outdated APIs alive introduces **technical debt and security risk**.  
Best practice:
- **Retire older APIs gracefully**    
- Notify clients    
- Encourage migration  
    This avoids "Zombie APIs"—unused but publicly accessible APIs.
    

---

### ✅ **Question 6:**
**What tool is commonly used during runtime to detect and block API attacks?**
🔘 **Correct Answer:** **Web Application Firewall (WAF)**
🧠 **Reasoning:**  
A **WAF** inspects HTTP/S traffic in real time and applies **rulesets** to detect:
- SQLi    
- XSS    
- Injection attacks    
- Rate-based anomalies  
    **API Gateways** can also help, but **WAFs are runtime-focused** tools that block payloads based on known attack signatures or behavior.

---
✅ **Recap of Correct Answers:**

|Q#|Answer|
|---|---|
|1|Data Encryption technologies|
|2|Such vulnerabilities are generally easily detected and fixed|
|3|At the API definition phase|
|4|Automated API-specific security testing|
|5|Update the version and retire older versions|
|6|Web application firewall|

---

