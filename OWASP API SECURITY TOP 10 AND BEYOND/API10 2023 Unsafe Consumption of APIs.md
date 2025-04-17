# Unsafe Consumption of APIs
##### [API10:2023 Unsafe Consumption of APIs](https://university.apisec.ai/products/owasp-api-security-top-10-and-beyond/categories/2152492264)
---
### **API10:2023 - Unsafe Consumption of APIs**
#### **Introduction**
**Unsafe Consumption of APIs** refers to the risk of blindly trusting third-party APIs when integrating them into applications. Many applications consume data from external APIs, but if these APIs are compromised, they can serve as a backdoor for attackers. Organizations that fail to validate, sanitize, and secure API interactions expose themselves to risks like **data leakage, injections, and denial of service (DoS) attacks**.

Unlike other API security concerns, which mostly focus on the **API provider**, this vulnerability is about **API consumers**—how they handle and process third-party API data.

---
## **OWASP Attack Vector Description**
Attackers exploit this vulnerability by targeting third-party services that an API relies on. If an attacker successfully **compromises a third-party API provider**, they can manipulate or inject malicious data into the APIs consuming it. Some examples of attack methods include:
- **Man-in-the-Middle (MitM) Attacks** – If an API consumer interacts with a third-party API over an **unencrypted connection**, attackers can intercept and modify API responses.    
- **Compromising Third-Party APIs** – Attackers can exploit vulnerabilities in a **trusted** API, making the **consumer application process malicious inputs**.    
- **Redirect Attacks** – If an API consumer blindly follows redirects from a third-party API, it may end up **sending data to an attacker-controlled server**.    

Since this information is **not always publicly available**, attackers may need to **enumerate API integrations** to find weaknesses.

---
## **OWASP Security Weakness Description**
The key weaknesses in API consumption include:
1. **Lack of Input Validation** – Developers **fail to sanitize and validate** API responses, allowing malicious payloads to enter the system.    
2. **Weak Transport Security** – APIs interacting over **HTTP instead of HTTPS** risk exposing sensitive data in plaintext.    
3. **Blind Trust in Third-Party APIs** – Developers assume **trusted APIs are always secure**, leading to data leaks or injection attacks.    
4. **Improper Authentication & Authorization** – Some APIs may **misuse authentication tokens** or lack proper access controls, exposing private data.
5. **Lack of Redirection Control** – APIs that **blindly follow redirects** from external sources could send data to malicious domains.    

These weaknesses provide **attackers a way to exploit API consumers**, making the API provider's security posture just as important as the consumer’s security practices.

---

## **OWASP Impacts Description**
The impact of **Unsafe API Consumption** depends on how the API **processes** the data it consumes. Some major risks include:
1. **Data Leakage** – If an attacker **compromises a third-party API**, they can manipulate responses to **expose sensitive user data**.    
2. **Injection Attacks** – If the API does **not sanitize incoming data**, attackers can exploit it for **SQL injection, XSS, or OS command injection**.    
3. **Denial of Service (DoS)** – An attacker could **send malformed or excessive API responses**, causing the API consumer to crash or become unresponsive.    
4. **Broken Authentication** – If a third-party API **leaks authentication tokens** or exposes API keys, attackers can use them to access sensitive systems.    
5. **Compromised Business Logic** – If an API relies on **external business logic**, a compromised API can **cause financial fraud or alter transactions**.    

---
## **Summary**
**Unsafe Consumption of APIs** occurs when applications **fail to validate, sanitize, and secure** interactions with **third-party APIs**. If a **third-party API is compromised**, it can act as an entry point for attacks, affecting all systems that rely on it.

⚠️ **Key risks include:**
- **Data leakage** through **insecure API connections**.    
- **Injection attacks** due to **lack of input validation**.    
- **DoS attacks** from malformed API responses.    
- **Trusting redirects** without validation.    

To test for **Unsafe Consumption of APIs**, security teams can:
- Monitor API requests/responses for **unexpected data or redirects**.    
- Simulate attacks by modifying API responses to check for **input validation weaknesses**.    
- Assess if the API follows redirects to **unknown or malicious destinations**.    

---

## **OWASP Preventative Measures**
Organizations can **mitigate risks** by following these best practices:
### **1. Secure Communication**
- Always **use HTTPS/TLS** for API communication to prevent **MitM attacks**.    
- Enforce **strict transport security policies (HSTS)**.   
### **2. Validate & Sanitize API Responses**
- Treat **API responses like user input**—sanitize **all incoming data**.    
- Use **allowlists** instead of **blacklists** for accepted API responses.    
- Implement **JSON/XML schema validation** to enforce data integrity.    
### **3. Authentication & Authorization**
- Ensure third-party API calls **require authentication** (OAuth2, API keys).    
- Use **role-based access controls (RBAC)** to restrict API interactions.    
### **4. Restrict API Redirects**
- Do **not blindly follow redirects**—maintain an allowlist of **trusted destinations**.    
- Use **Content Security Policy (CSP)** headers to **prevent open redirects**.    
### **5. Monitor & Log API Interactions**
- Enable **API logging** to detect **suspicious third-party API activity**.    
- Use **rate limiting** to prevent **abuse** from an external API.    
### **6. Regularly Assess Third-Party APIs**
- Periodically **review third-party API security policies**.    
- Use automated tools to **scan API integrations for vulnerabilities**.  
---
### **Conclusion**
API security isn’t just about **securing API providers**—**API consumers must also take responsibility**. Treat **all third-party API data as untrusted** and apply **strict validation, authentication, and encryption** to **minimize risks**. Otherwise, an insecure API integration could lead to **data breaches, DoS attacks, and unauthorized access**. 🚀

---
### **Question 1**
**How does OWASP describe the risk regarding Unsafe Consumption of APIs?**
✅ **Developers will tend to adopt weaker security standards**
🔍 **Explanation:**  
Developers often **trust third-party APIs** without enforcing **strict security controls**, leading to **weaker security requirements** in areas like **authentication, encryption, and input validation**.

---
### **Question 2**
**What is a potential risk when an API interacts with other APIs over an unencrypted channel?**
✅ **Exposure of sensitive information due to cleartext transmission**
🔍 **Explanation:**  
If an API communicates over **HTTP instead of HTTPS**, attackers can **intercept** API requests and **steal sensitive data** via **Man-in-the-Middle (MitM) attacks**.

---
### **Question 3**
**Why is it important to maintain an allow list of well-known locations integrated APIs may redirect to?**
✅ **To avoid blindly following redirects and potential security threats**
🔍 **Explanation:**  
If an API **blindly follows redirects**, attackers can **redirect requests to malicious sites** to steal data or execute further attacks. An **allowlist** ensures redirects only go to **trusted locations**.

---

### **Question 4**
**What is a crucial step to ensure the security of data received from integrated APIs?**
✅ **Validate and properly sanitize data before using it**
🔍 **Explanation:**  
Data from **external APIs should be treated as untrusted input**. Without proper validation and sanitization, APIs could be vulnerable to **SQL injection, XSS, and other attacks**.

---
### **Question 5**
**What could be a potential outcome of weaker security standards in API integrations?**
✅ **Exposure of sensitive information to unauthorized actors**
🔍 **Explanation:**  
Weak security in API integrations can **lead to data leaks**, allowing **attackers to access sensitive data** without proper authentication.

---
## Additional Resources
- [Web Service Security Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Web_Service_Security_Cheat_Sheet.html)
- [Injection Flaws](https://www.owasp.org/index.php/Injection_Flaws)
- [Input Validation Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Input_Validation_Cheat_Sheet.html)
- [Injection Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Injection_Prevention_Cheat_Sheet.html)
- [Transport Layer Protection Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Transport_Layer_Protection_Cheat_Sheet.html)
- [Unvalidated Redirects and Forwards Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Unvalidated_Redirects_and_Forwards_Cheat_Sheet.html)
- [CWE-20: Improper Input Validation](https://cwe.mitre.org/data/definitions/20.html)
- [CWE-200: Exposure of Sensitive Information to an Unauthorized Actor](https://cwe.mitre.org/data/definitions/200.html)
- [CWE-319: Cleartext Transmission of Sensitive Information](https://cwe.mitre.org/data/definitions/319.html