# Broken Function Level Authorization (BFLA)
##### [API5:2023 Broken Function Level Authorization](https://university.apisec.ai/products/owasp-api-security-top-10-and-beyond/categories/2152492169)

---
### **1️⃣ Introduction**
Broken Function Level Authorization (BFLA) occurs when **API functions lack proper access controls**, allowing unauthorized users to perform actions beyond their intended privilege level.
- **BOLA (Broken Object Level Authorization)** allows an attacker to **view** data they shouldn't.    
- **BFLA (Broken Function Level Authorization)** allows an attacker to **modify** or **delete** data they shouldn't.    
![[Pasted image 20250402124112.png]]
**Example:**  
A **fintech API** vulnerable to BOLA would let an attacker **see** another user’s bank balance, while a **BFLA vulnerability** would let an attacker **transfer funds** from other users' accounts.

---
### **2️⃣ OWASP Attack Vector**
- **How it works:**  
    Attackers make **legitimate API requests** to endpoints they shouldn’t have access to.
- **Who is at risk?**  
    APIs that don’t properly restrict access for:    
    - **Anonymous users** (unauthenticated users)        
    - **Regular users** trying to perform admin-level actions        
    - **Lower-privileged roles** attempting to execute privileged functions
🔴 **Exploitable if:**
- APIs expose **separate admin endpoints** without proper authorization.    
- APIs allow **unauthorized HTTP methods** (e.g., using DELETE instead of GET).

---
### **3️⃣ OWASP Security Weakness**
Authorization checks can be **misconfigured** because:
- APIs have **complex role structures** (e.g., admins, vendors, partners).    
- APIs use **multiple endpoints** for different roles.    
- Developers fail to **enforce proper access control** for each function.    

🚨 **APIs are more vulnerable than web apps** because their structure is more predictable, making it easier for attackers to **find and exploit weak access controls**.

---
##### Testing for BFLA
* Identify endpoints an attacker could use to their advantage e.g.
	* Altering user accounts
	* Deleting user resources
	* Gaining access to restricted endpoints

---
### **4️⃣ OWASP Impacts**
- **Privilege escalation:** Regular users gain admin privileges.    
- **Unauthorized actions:** Attackers modify/delete data they shouldn't.    
- **Data exposure:** Attackers gain access to sensitive admin functionality.    
- **Service disruption:** Unauthorized modifications lead to system failures.

---
### **5️⃣ Examples of BFLA Exploits**
🔹 **1. Bypassing Role Checks**
```pgsql
GET /user/{userid}/profile → Allowed ✅
GET /admin/users/ → Allowed for Admins only ❌
```
If the API does not validate roles correctly, an attacker might access admin functionality by **changing the endpoint manually**.

🔹 **2. Exploiting HTTP Methods**
```pgsql
PUT /identity/api/v2/videos/758 → Regular user can edit videos ✅
DELETE /identity/api/v2/admin/videos/758 → Only admins should delete videos ❌
```
If an attacker **switches from PUT to DELETE**, they might delete content they shouldn’t have access to.

🔹 **3. Misusing Functionality**
`POST /partners/add_user → Adds users to a partner group ✅`
If this is not restricted to partners, **anyone could add themselves** to privileged roles and gain access to restricted resources.

---

### **6️⃣ OWASP Preventative Measures**
✔ **1. Default Deny Policy**
- By default, **deny all access** and require **explicit permissions**.    
✔ **2. Centralized Authorization Mechanism**
- Implement a **single, consistent authorization module** for **all** API functions.    
✔ **3. Role-Based Access Controls (RBAC)**
- Ensure each function **verifies** the user's role before executing privileged actions.
✔ **4. Secure HTTP Methods**
- Restrict API functions based on **HTTP methods** (e.g., block DELETE requests for non-admins).    
✔ **5. API Endpoint Review**
- **Manually review** all API endpoints for **authorization flaws**.    
✔ **6. Secure Admin Functions**
- Place **all admin functions** inside a **separate admin controller** that enforces strict **authorization checks**.    
✔ **7. Logging & Monitoring**
- Log **all failed authorization attempts** and implement **rate limiting** to prevent brute-force attacks.
---
 Summary
🔹 **BFLA** occurs when an API fails to **restrict access** to sensitive functions.  
🔹 Attackers **abuse API endpoints** to perform **privileged actions** they shouldn't have access to.  
🔹 Fix it by **enforcing strict role-based access controls (RBAC)** and **securely handling API endpoints**.

---
### **BFLA Quiz Answers**
#### **Question 1**
**Which of the following is NOT a recommended preventative measure for Broken Function Level Authorization?**
✅ **Correct Answer:**  
**"Make sure that all administrative functions inside a regular controller do not implement authorization checks based on the user's group and role."**
🔹 **Explanation:** This statement contradicts OWASP best practices.  
🔹 Instead, **ALL** administrative functions must enforce authorization checks based on user roles.

---

#### **Question 2**
**When testing for BFLA vulnerabilities, what functionality should you look for that could be exploited?**
✅ **Correct Answer:**  
**"Functionality that allows a user to add themselves to any user group."**
🔹 **Explanation:** If users can add themselves to **higher-privileged roles**, they can escalate privileges and access restricted functions.  
🔹 The other options (unlimited API requests, username/password changes) are **not specific** to BFLA vulnerabilities.

---

#### **Question 3**
**What is the primary impact of exploiting a Broken Function Level Authorization vulnerability according to OWASP?**
✅ **Correct Answer:**  
**"An attacker could access unauthorized functionality, with administrative functions being key targets."**
🔹 **Explanation:**
- BFLA allows attackers to **perform actions reserved for privileged users**, such as **deleting accounts, modifying settings, or accessing admin panels**.    
- **DoS attacks, script injection, or domain admin escalation** are NOT the primary impacts of BFLA.
---
#### **Question 4**
**According to OWASP, what makes implementing proper authorization checks challenging in modern applications?**
✅ **Correct Answer:**  
**"Modern applications have complex user hierarchies and many types of roles or groups."**
🔹 **Explanation:**
- APIs handle multiple user roles (e.g., **admins, partners, vendors, public users**), making access control **complicated**.    
- APIs are **structured and predictable**, which makes them easier to exploit—not harder to secure.

---
#### **Question 5**
**What is the primary threat associated with Broken Function Level Authorization in API Security?**
✅ **Correct Answer:**  
**"An attacker could gain unauthorized access to certain endpoints they should not have access to."**
🔹 **Explanation:**
- BFLA occurs when **privileged API functions** are accessible to **unauthorized users**.    
- Attackers can **modify, delete, or escalate privileges** via misconfigured access controls.
---
## Additional Resources
- [CWE-285: Improper Authorization](https://cwe.mitre.org/data/definitions/285.html)
- [Forced Browsing](https://owasp.org/www-community/attacks/Forced_browsing)
- "A7: Missing Function Level Access Control", [OWASP Top 10 2013](https://github.com/OWASP/Top10/raw/master/2013/OWASP%20Top%2010%20-%202013.pdf)
- [OWASP Community Guide for Access Control](https://owasp.org/www-community/Access_Control)