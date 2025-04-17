### **Understanding Broken Object Level Authorization (BOLA) - API1:2023**
# BOLA
##### [API1:2023 Broken Object Level Authorization](https://university.apisec.ai/products/owasp-api-security-top-10-and-beyond/categories/2152491878)
#### **What is BOLA?**
**Broken Object Level Authorization (BOLA)** is the most common and severe API vulnerability. It occurs when an API does not properly enforce authorization, allowing users to access data that doesn’t belong to them.
📌 **Example:**
- **Intended behavior**: A user should only access their own data.    
- **Vulnerable API**: A user manipulates an API request to access another user's data.    
---
### **How Do Attackers Exploit BOLA?**
Attackers manipulate **object identifiers** (IDs) in API requests. These identifiers could be:  
✅ **Sequential numbers** (e.g., `user_id=1234 → user_id=1235`)  
✅ **UUIDs** (e.g., `user_id=abcd-efgh-5678 → user_id=ijkl-mnop-1234`)  
✅ **Custom strings** (e.g., `/account/admin-settings/bman` → `/account/admin-settings/hdent`)
📌 **Example Attack:**
- A hospital API allows a user (Bruce) to retrieve their data:   
    `GET https://herohospital.com/api/v3/users?id=2727`
    ✅ Bruce gets:
```
{
  "id": "2727",
  "fname": "Bruce",
  "lname": "Wayne",
  "diagnosis": "Depression"
}
```    
- Bruce **changes the ID** to `2728`:
    `GET https://herohospital.com/api/v3/users?id=2728`
    🚨 **Unauthorized data leakage**:
```
{
  "id": "2728",
  "fname": "Harvey",
  "lname": "Dent",
  "diagnosis": "Dissociative Identity Disorder"
}
```

This shows that **no proper authorization checks exist**, allowing Bruce to access Harvey's sensitive medical data.
![[BOLA.png]]

---
### **Why is BOLA Dangerous?**
🚨 **Impacts of BOLA:**
1. **Data Breach** → Attackers can access sensitive personal or financial data.
2. **Data Manipulation** → Attackers can modify another user’s data.
3. **Account Takeover** → Attackers might gain full control of another user’s account.
---

### **How to Prevent BOLA?**
✅ **1. Implement Proper Authorization Mechanisms**
- Enforce **role-based access control (RBAC)** or **attribute-based access control (ABAC)**.    
- Validate **every request** to ensure a user is authorized to access a resource.    

✅ **2. Check Authorization in Every API Call**
- Never rely on just client-side checks.    
- Implement **server-side access control** for every API request.    

✅ **3. Use Secure and Random Object IDs**
- Instead of predictable IDs (`123, 124, 125`), use **random UUIDs** (`e.g., 5f4dcc3b5aa765d61d8327deb882cf99`).

✅ **4. Perform Security Testing**
- **Automated security tests** for authorization.    
- **Penetration testing** to check for ID manipulation attacks.    

✅ **5. Monitor API Logs for Unusual Activity**
- Detect repeated unauthorized access attempts.    
- Use **rate limiting** to prevent brute-force attacks.    

---
### **Key Takeaways**
🔹 **BOLA is the most common API security risk**.  
🔹 Attackers exploit **poor authorization controls** by modifying object IDs.  
🔹 Proper **authorization enforcement and security testing** can prevent it.

---
### **Question 1:**
**Which of the following is NOT a recommended preventative measure for limiting resource consumption in APIs?**  
✅ **Answer:** _Allow an unlimited number of elements in request arrays._

🔹 **Explanation:** Allowing unlimited elements in request arrays can lead to excessive memory consumption, slow API performance, or even denial of service (DoS) attacks. A recommended best practice is to enforce **limits on array sizes** to control resource usage.

---

### **Question 2:**
**Which of the following best describes the threat associated with the lack of rate limiting?**  
✅ **Answer:** _The API allows uncontrolled interactions or resource consumption which can lead to Denial of Service (DoS) or increased financial costs._

🔹 **Explanation:** Without rate limiting, an attacker or even an unintentional heavy user can overwhelm the API, causing **downtime, resource starvation, or high cloud costs** due to excessive API usage.

---

### **Question 3:**
**Why is rate limiting important for the monetization and availability of APIs?**  
✅ **Answer:** _Rate limiting allows API providers to control the flow of their data._

🔹 **Explanation:** By enforcing rate limits, API providers can **ensure service availability**, prevent abuse, and implement **tiered pricing models** (e.g., free users get 100 requests/day, paid users get 10,000 requests/day).

---

### **Question 4:**
**In regards to API rate limiting, what is indicated by an HTTP 429 response status code?**  
✅ **Answer:** _The consumer has made too many requests._

🔹 **Explanation:** An HTTP **429 Too Many Requests** response informs the client that **they have exceeded the allowed number of API requests** within a given timeframe.

---

### **Question 5:**
**According to OWASP, what is the primary consequence of not implementing API rate limiting?**  
✅ **Answer:** _DoS due to resource starvation or a negative impact to the service provider's billing._

🔹 **Explanation:** Without rate limiting, APIs can be **overloaded with excessive requests**, leading to **denial of service (DoS)** or **high infrastructure costs** from cloud auto-scaling.

---
## Additional Resources
- [CWE-284: Improper Access Control](https://cwe.mitre.org/data/definitions/284.html)
- [CWE-285: Improper Authorization](https://cwe.mitre.org/data/definitions/285.html)
- [CWE-639: Authorization Bypass Through User-Controlled Key](https://cwe.mitre.org/data/definitions/639.html)
- [Authorization Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Authorization_Cheat_Sheet.html)
- [Authorization Testing Automation Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Authorization_Testing_Automation_Cheat_Sheet.html)
- [Web Security Academy: Access Controls](https://portswigger.net/web-security/access-control)
- [APIsec What is BOLA?](https://www.apisec.ai/blog/broken-object-level-authorization)
- [BOLA Deep Dive by Inon Shkedy](https://inonst.medium.com/a-deep-dive-on-the-most-critical-api-vulnerability-bola-1342224ec3f2)