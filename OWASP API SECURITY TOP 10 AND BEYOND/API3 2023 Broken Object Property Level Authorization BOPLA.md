# BOPLA
##### [API3:2023 Broken Object Property Level Authorization](https://university.apisec.ai/products/owasp-api-security-top-10-and-beyond/categories/2152491880)
### **API3:2023 – Broken Object Property Level Authorization (BOPLA)**
**Introduction:**  
BOPLA is a combination of two OWASP API vulnerabilities from 2019:
- **Excessive Data Exposure** – When an API returns too much data, including sensitive information, instead of only what’s needed.
- **Mass Assignment** – When an API allows users to modify object properties they shouldn’t be able to, leading to privilege escalation or data manipulation.
Both issues arise due to **weak authorization controls at the object property level**, meaning an API fails to restrict access to or modification of sensitive data.
---
## **Attack Vector (How Hackers Exploit BOPLA)**
1. **Excessive Data Exposure:**    
    - APIs often return all object properties by default.        
    - If sensitive information is exposed in API responses, attackers can harvest it.        
    - Example: A request for user profile data returns extra fields like email, SSN, or account balance.        
2. **Mass Assignment:**    
    - Attackers inject extra parameters into API requests to modify unauthorized properties.        
    - Example: Adding `isAdmin: true` to an account creation request and gaining admin privileges.        

**Exploiting BOPLA can result in:**
- **Data breaches** (exposing private information).    
- **Privilege escalation** (gaining unauthorized access).    
- **Account takeovers** (manipulating permissions).

---
## **Examples of BOPLA Exploits**
### **1. Excessive Data Exposure**
📌 **Scenario:** A banking API allows users to check their account balance.  
📌 **Attack:** Instead of just returning `balance`, the API response includes:
![[Pasted image 20250402121024.png]]
![[Pasted image 20250402121030.png]]
```json
{
  "account_id": "12345",
  "balance": 5000,
  "account_owner": "John Doe",
  "SSN": "123-45-6789",
  "credit_score": 750
}
```
📌 **Risk:** The API leaks sensitive data that an attacker can steal.

---
### **2. Mass Assignment**
📌 **Scenario:** A user updates their profile via API.  
📌 **Attack:** The API accepts an unexpected `isAdmin` field in the request:
![[Pasted image 20250402121039.png]]
```json
{
  "username": "hacker01",
  "password": "SuperSecure123",
  "isAdmin": true
}
```
📌 **Risk:** If the API lacks proper checks, the user becomes an admin.

---
## **How to Prevent BOPLA**
### ✅ **Excessive Data Exposure Prevention**
🔹 Always filter API responses to include only necessary fields.  
🔹 Avoid generic serialization methods like `.to_json()` that expose all properties.  
🔹 Use **whitelisting** instead of **blacklisting** sensitive data.  
🔹 Implement **schema-based validation** to define strict response structures.

---
### ✅ **Mass Assignment Prevention**
🔹 **Use allowlists** to specify which fields users can modify.  
🔹 **Disable automatic object binding** (e.g., avoid direct mapping of request data to internal objects).  
🔹 **Manually review API documentation** to ensure no unintended fields are exposed.  
🔹 **Monitor API logs** for unexpected parameters in user requests.

---
## **Key Takeaways**
🚀 **BOPLA combines two critical API flaws – excessive data exposure & mass assignment.**  
🚀 **APIs should only expose & allow changes to necessary properties.**  
🚀 **Strong input validation and schema enforcement help prevent these vulnerabilities.**

Here are the correct answers for the BOPLA quiz:
### **Question 1**
✅ **Correct Answer:** **The API responds with more information than needed to fulfill a request.**  
📌 **Explanation:** Excessive Data Exposure occurs when an API unnecessarily includes sensitive information in its responses instead of limiting the data to what the requester needs.

---

### **Question 2**
✅ **Correct Answer:** **It could allow a user to escalate privileges or edit object properties.**  
📌 **Explanation:** A Mass Assignment vulnerability allows unauthorized users to modify object properties, which can lead to privilege escalation or data manipulation.

---

### **Question 3**
✅ **Correct Answer:** **Use generic methods such as to_json() and to_string().**  
📌 **Explanation:** Using generic serialization methods like `.to_json()` can expose all object properties, including sensitive ones. Instead, **cherry-pick** only the necessary properties to return.

---

### **Question 4**
✅ **Correct Answer:** **Data disclosure to unauthorized parties, data loss, or data manipulation.**  
📌 **Explanation:** Unauthorized access to API properties can lead to sensitive information leaks, unauthorized modifications, or even account takeovers.

---
### **Question 5**
✅ **Correct Answer:** **By sending requests to the target API endpoints and reviewing the information sent in response.**  
📌 **Explanation:** Testing API responses helps identify excessive data exposure by revealing whether sensitive data is unnecessarily included.

## Additional Resources
- [API3:2019 Excessive Data Exposure - OWASP API Security Top 10 2019](https://github.com/OWASP/API-Security/blob/master/2019/en/src/0xa3-excessive-data-exposure.md)
- [API6:2019 - Mass Assignment - OWASP API Security Top 10 2019](https://github.com/OWASP/API-Security/blob/master/2019/en/src/0xa6-mass-assignment.md)
- [Mass Assignment Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Mass_Assignment_Cheat_Sheet.html)
- [CWE-213: Exposure of Sensitive Information Due to Incompatible Policies](https://cwe.mitre.org/data/definitions/213.html)
- [CWE-915: Improperly Controlled Modification of Dynamically-Determined Object Attributes](https://cwe.mitre.org/data/definitions/915.html)

