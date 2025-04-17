# Improper Inventory Management
##### [API9:2023 Improper Inventory Management](https://university.apisec.ai/products/owasp-api-security-top-10-and-beyond/categories/2152492227)
---
## **📌 Introduction**
**What is API9:2023 - Improper Inventory Management?**  
Improper inventory management occurs when organizations expose **non-production and unsupported API versions** without the same security controls as production APIs. These APIs may contain vulnerabilities due to:
- Outdated security practices    
- Insufficient patching    
- Lack of documentation    
This vulnerability is a gateway for attackers to **exploit other API security weaknesses** and gain unauthorized access to sensitive data.
---
## **📌 OWASP Attack Vector Description**
### **How Do Attackers Exploit Improper Inventory Management?**
Threat actors exploit **older API versions or unprotected endpoints** left exposed due to improper asset tracking. Attackers may also gain access to sensitive data through **third-party integrations** that shouldn’t have access.
### **Common Attack Techniques**
1. **Accessing Deprecated API Versions**    
    - Older APIs may **lack modern security** features like OAuth, JWT authentication, or input validation.        
    - Example: An old API at `/v1/admin` may allow unrestricted administrative access.        
2. **Scanning for Exposed Endpoints**    
    - **Google Dorking**, **DNS enumeration**, and **search engines** (like Shodan) help attackers locate vulnerable APIs.        
    - Example: Searching `"site:api.target.com" inurl:dev` might expose development APIs.       
3. **Exploiting Weak API Security Policies**    
    - Non-production APIs may have **debugging features enabled** or **default credentials** configured.        
    - Example: An attacker finds `api.test.target.com` with **no authentication** and extracts data.        
---
## **📌 OWASP Security Weakness Description**
### **Why Does This Happen?**
- **Lack of API documentation**: Without up-to-date records, teams may **forget to secure or retire old APIs**.    
- **No proper API lifecycle management**: Some organizations **fail to track and decommission old APIs**, leaving them vulnerable.    
- **Unsecured microservices**: Modern applications deploy microservices dynamically (e.g., **Kubernetes, cloud environments**) but often **lack visibility** on API endpoints.    
### **Real-World Example**
A fintech company launches API v3 but **forgets to decommission API v1**, which still connects to the production database. Attackers **reverse-engineer API v1** to gain admin privileges.

---
## **📌 OWASP Impacts Description**
### **What Happens If Improper Inventory Management Exists?**
1. **Data Breaches** 📂    
    - Attackers exploit **old API versions** that **lack authentication, rate limiting, or encryption**, leading to data leaks.        
2. **Server Takeover** 🖥️    
    - Some outdated APIs share **the same backend database** as production APIs.        
    - An attacker exploits API v1, gaining **admin access** to API v3’s data.        
3. **Exploitation of Deprecated Endpoints** 🛠️    
    - Example:        
        - API v1 → `/v1/admin/deleteAllUsers`            
        - API v3 → `/v3/admin/deleteAllUsers` (more secure)            
        - **If API v1 still exists**, an attacker may use it to delete user accounts.            
---
## **📌 Detection Techniques**
### **How Do Attackers Find Improper Inventory Management?**
Attackers use multiple methods to **detect outdated or non-production APIs**:
### **1️⃣ API Documentation & Changelogs**
- Searching **old API documentation** and **version history** can reveal deprecated endpoints.    
- Example:    
    - The organization’s **changelog** states:
```rust
API v1 -> Deprecated due to security vulnerabilities.
API v2 -> Fixed rate-limiting issues.
API v3 -> Improved authentication.
```        
    - Attackers now **test API v1 for vulnerabilities**.        
### **2️⃣ Brute-Forcing API Endpoints**
- Attackers guess API versions using common naming conventions like:
```bash
/api/v1/
/api/v2/
/api/test/
/api/dev/
/alpha/,/beta/,/test/,/uat/,/demo/
```    
- Example:
    `curl -X GET https://api.target.com/v1/admin`    
    If API v1 is still **accessible**, an attacker can **exploit it**.    
### **3️⃣ Inspecting API Requests and Headers**
- API versioning **can be hidden in headers**:
```makefile
Accept: version=2.0
Accept: api-version=3
```    
- **If older versions are still active**, they can be exploited.    
### **4️⃣ Searching for Public APIs Using Google Dorking**
- Attackers can search for exposed APIs with queries like:
```makefile
site:target.com inurl:/api
site:api.target.com filetype:json
```    
- This helps them find **publicly exposed API endpoints**.

### **5️⃣ Non-production API versions examples:**
* api.test.target.com
* api.uat.target.com
* beta.api.com
* /api/private
* /api/partner
* /api/test
---
## **📌 OWASP Preventative Measures**
### **How Can Organizations Secure Their APIs?**
✅ **1️⃣ Inventory All API Hosts**
- Maintain a **complete list of API hosts** and classify them as:    
    - **Production**        
    - **Staging**        
    - **Test/Development**        
    - **Internal/Partner APIs**        
- Document API versions and access control policies.    
✅ **2️⃣ Secure Non-Production APIs**
- Restrict access to **development/staging APIs** (`api.test.target.com`).    
- Use **authentication and rate-limiting** for all API versions.    
- Apply the **same security policies to all API environments**.    
✅ **3️⃣ Document API Changes and Updates**
- Automate API documentation using tools like **OpenAPI/Swagger**.    
- Include API documentation in **CI/CD pipelines** to ensure updates remain **consistent**.    
✅ **4️⃣ Implement API Security Firewalls**
- Deploy **API gateways and WAFs** (Web Application Firewalls) to filter requests.    
- Example: **Cloudflare API Shield**, **AWS API Gateway**, **NGINX App Protect**.    
✅ **5️⃣ Retire Old APIs and Backport Security Fixes**
- If an older API version **cannot be removed**, **backport security improvements**.    
- If necessary, **force users to migrate** to the latest version.   
✅ **6️⃣ Avoid Using Production Data in Non-Production APIs**
- If test APIs require real data, **mask or encrypt sensitive fields**.    
✅ **7️⃣ Enforce Strict API Versioning Policies**
- Use **clear versioning** to **phase out** older API versions.    
- Example of a **structured API deprecation process**:
```rust
API v1 -> Deprecated on Jan 2024
API v2 -> Maintenance support until Dec 2025
API v3 -> Active development
```
- This ensures **no old APIs remain unpatched**.
---
## **📌 Additional Resources**
- [CWE-1059: Incomplete Documentation](https://cwe.mitre.org/data/definitions/1059.html)
- [OpenAPI Initiative](https://www.openapis.org/)
- OWASP API Security Top 10
---
## **📌 Summary**
🔹 **API9:2023 - Improper Inventory Management** occurs when organizations **expose outdated or non-production API versions** that lack security updates.  
🔹 Attackers exploit **deprecated APIs, undocumented endpoints, and misconfigured services** to gain access to sensitive data.  
🔹 **Proper inventory management, API documentation, and access control** are crucial in **preventing this vulnerability**.

----
#### QUIZ
### **Question 1**
**When running multiple versions of an API, what risk does this pose?**  
✅ **Increased management resources and expanded attack surface**
- Running multiple versions requires additional maintenance and security patches. Older or deprecated versions may introduce vulnerabilities.
---
### **Question 2**
**Which of the following can aid an attacker in identifying improperly managed APIs?**  
✅ **Outdated API documentation**
- Attackers can use outdated documentation to find old, vulnerable API endpoints that are still active but no longer properly maintained.
---
### **Question 3**
**Which of the following is the most severe impact related to API inventory management?**  
✅ **Enables an attacker to exploit other known vulnerabilities**
- Improper inventory management can expose unpatched and outdated APIs, allowing attackers to exploit known vulnerabilities and gain access to sensitive systems.
---
### **Question 4**
**Which of the following is an indication that an API has a "data flow blindspot"?**  
✅ **There is no visibility of which type of sensitive data is shared**
- A **data flow blindspot** occurs when organizations lack insight into what sensitive data is being processed, shared, or exposed by their APIs.  

---

### **Question 5**
**Which of the following practices can help mitigate risks associated with improper API inventory management?**  
✅ **Automatically generate documentation with open standards and including it in the CI/CD pipeline**
- Automating documentation ensures it stays up to date and reduces the risk of outdated or incorrect API references leading to security gaps.
- --- 
## Additional Resources
- [CWE-1059: Incomplete Documentation](https://cwe.mitre.org/data/definitions/1059.html)
- [OpenAPI Initiative](https://www.openapis.org/)