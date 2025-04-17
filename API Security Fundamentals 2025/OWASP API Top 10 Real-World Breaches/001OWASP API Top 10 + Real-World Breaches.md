# Introduction - OWASP API Security Top 10
##### [OWASP API Top 10 + Real-World Breaches](https://university.apisec.ai/products/api-security-fundamentals-2025/categories/2157142220)

### API Attack Examples




### ✅ **Question 1: What do "BOLA" attacks (OWASP #1) target?**
> **Correct Answer:** **Inadequate/missing data access controls**
**Explanation:**  

BOLA = **Broken Object Level Authorization**  
Attackers exploit **weak or missing authorization checks** to access **objects (data)** they shouldn’t, like user profiles, documents, etc.

---

### ✅ **Question 2: Which OWASP category addresses out-of-date API versions?**
> **Correct Answer:** **#9 - Improper Inventory Management**

**Explanation:**  
Improper Inventory Management refers to poor tracking and management of APIs, including:
- Deprecated versions still active    
- Shadow APIs (undocumented)    
- Inactive endpoints accessible    

---

### ✅ **Question 3: What real-world example illustrates BOLA in the OWASP Top 10?**
> **Correct Answer:** **Peloton’s API exposing user data**

**Explanation:**  
Peloton's API allowed unauthenticated users to change the ID in a request and **access data of any other user** – a classic case of BOLA.

---

### ✅ **Question 4: What does “Excessive Data Exposure” typically involve?**
> **Correct Answer:** **Returning unnecessary or sensitive data via APIs**

**Explanation:**  
APIs often return more data than needed, trusting the client/UI to filter it. Attackers can inspect responses and get sensitive data.

---

### ✅ **Question 5: Which best practice addresses Excessive Data Exposure?**
> **Correct Answer:** **Use data minimization techniques**

**Explanation:**  
Only send data **necessary for the request**. Don’t rely on frontend/UI to restrict what the user can access.

---

### ✅ **Question 6: What vulnerability does rate limiting primarily help prevent?**
> **Correct Answer:** **Unrestricted Resource Consumption**

**Explanation:**  
Rate limiting prevents **API abuse** like DoS attacks, brute force, and bot overuse by **limiting how often endpoints can be hit**.

---

### ✅ **Question 7: What real-world example demonstrated Broken Function Level Authorization?**
> **Correct Answer:** **Bumble allowing free-to-premium account upgrades**

**Explanation:**  
In the Bumble case, **regular users could call premium-only functions**, due to **missing function-level access controls** – OWASP #5.

---

### ✅ **Question 8: How does SSRF typically exploit APIs?**
> **Correct Answer:** **Manipulating user input to access unauthorized resources**

**Explanation:**  
SSRF (Server-Side Request Forgery) tricks the server into making **requests to internal systems** using crafted URLs.

---

### ✅ **Question 9: What general best practice applies to all OWASP API vulnerabilities?**
> **Correct Answer:** **Test APIs continuously**

**Explanation:**  
Regular and continuous testing (security scans, pen testing, fuzzing, etc.) helps catch API vulnerabilities early.

---