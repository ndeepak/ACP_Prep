# Unrestricted Access to Sensitive Business Flows
##### [API6:2023 Unrestricted Access to Sensitive Business Flows](https://university.apisec.ai/products/owasp-api-security-top-10-and-beyond/categories/2152492181)

---
### **API6:2023 - Unrestricted Access to Sensitive Business Flows**
#### **Introduction**
This vulnerability occurs when an API exposes critical business processes without proper restrictions, allowing attackers to **automate** and **exploit** those workflows. If an attacker understands the structure of API requests, they can:
- **Spam** other users    
- **Drain inventory** of high-demand products    
- **Prevent legitimate users** from accessing key functionalities
This is a **new addition** to OWASP’s **2023 API Security Top 10** list.

---
### **Attack Vector**
🔍 **How Attackers Exploit This Vulnerability:**
1. **Analyze API Requests:** Attackers observe API calls made by users and identify key workflows.    
2. **Automate API Requests:** Using tools like **Burp Suite**, **Postman**, or **cURL**, attackers automate these workflows.    
3. **Exploit Business Logic:**    
    - **Scalping Bots**: Purchase high-demand products before real customers (e.g., PlayStation 5 bots).        
    - **Denial of Inventory**: Continuously add items to a cart, preventing others from purchasing.
    - **Service Disruption**: Overload an API workflow to disrupt business operations.

---
### **Security Weakness**
❌ **Why Does This Happen?**
- Lack of **rate limiting** and **CAPTCHA protections**    
- No **monitoring** of unusual activity patterns    
- **Weak access controls** on sensitive API endpoints    
- Business logic **not considered** during API security design    

---
### **Impacts**
📉 **Business-Level Consequences:**
- **Lost revenue** due to product scalping or service abuse    
- **User dissatisfaction** when genuine customers can't access services    
- **Economic inflation** in gaming environments (e.g., unlimited in-game currency exploits)
---
### **Real-World Example: PlayStation 5 Scalping**
**Scenario:**
- A bot continuously monitors the Best Buy API for **PS5 stock updates**.
- As soon as stock is available, it **automatically purchases all units** within seconds.
- Legitimate customers cannot buy the product.
![[Pasted image 20250402133234.png]]
🔧 **Fix:** Implement **rate limiting, CAPTCHA, and bot detection** to slow down automated purchases.

---
### **Prevention Measures**
🔐 **Mitigation Strategies (Two-Layer Approach)**
#### **1️⃣ Business-Level Controls:**
- Identify **critical business flows** that could be abused    
- Restrict **excessive use** of key workflows    
#### **2️⃣ Engineering-Level Protections:**
✅ **Device Fingerprinting:**
- Block unexpected client devices (e.g., headless browsers, automation scripts)    
✅ **Human Detection:**
- Implement **CAPTCHA** or advanced biometric verification   
✅ **Non-Human Behavior Detection:**
- Monitor user actions and block **unrealistic workflows** (e.g., checkout completed in less than 1 second)  
✅ **IP-Based Blocking:**
- Block **Tor exit nodes**, **VPNs**, and known proxies used for automation
✅ **Secure Machine-to-Machine (M2M) APIs:**
- Require **authentication and authorization** for all B2B and developer APIs
---
### **Unrestricted Access to Sensitive Business Flows - Quiz Answers & Explanations**
#### **Question 1: What is Unrestricted Access to Sensitive Business Flows about?**
✅ **Correct Answer:**  
✔️ **"It's about the risk of an attacker identifying and exploiting API-driven workflows."**
🔍 **Explanation:**  
This vulnerability is not just about accessing sensitive data; it's about manipulating business logic through API requests. Attackers automate **legitimate API flows** to disrupt normal operations, such as scalping products or preventing real users from completing transactions.

---

#### **Question 2: What is a possible way to detect non-human patterns during the exploitation of Unrestricted Access to Sensitive Business Flows?**
✅ **Correct Answer:**  
✔️ **"Analyze the user flow to detect actions that happen too quickly for a human user."**
🔍 **Explanation:**  
Attackers use bots to **automate API workflows**, making them much faster than humans. Detecting **unrealistic user behavior**—such as completing a checkout in **milliseconds**—can help stop automated abuse.

---
#### **Question 3: Which of the following is NOT a recommended preventative measure against Unrestricted Access to Sensitive Business Flows?**
✅ **Correct Answer:**  
✔️ **"Allow unlimited access to APIs that are consumed directly by machines."**
🔍 **Explanation:**  
APIs **used by machines (B2B, developer APIs, etc.)** should still have **access control, rate limiting, and monitoring**. Leaving them unrestricted makes them a prime target for abuse.

---
#### **Question 4: Which of the following is an impact of an attacker exploiting an API with Unrestricted Access to Sensitive Business Flows?**
✅ **Correct Answer:**  
✔️ **"It can hurt the business by preventing legitimate users from purchasing a product."**
🔍 **Explanation:**  
The main impact of this vulnerability is **business disruption**, not direct data breaches. Attackers can **buy out inventory**, **spam registrations**, or **prevent normal users from accessing services**.

---
#### **Question 5: What kind of requests does an attack under Unrestricted Access to Sensitive Business Flows usually involve?**
✅ **Correct Answer:**  
✔️ **"Requests that are individually legitimate and unidentifiable as an attack."**
🔍 **Explanation:**  
Unlike DDoS attacks that send **huge volumes of traffic**, this attack involves **normal API calls made at high speed** to manipulate business logic. Since each request is valid, **traditional security measures may not detect them**.

---
## Additional Resources
- [OWASP Automated Threats to Web Applications](https://owasp.org/www-project-automated-threats-to-web-applications/)
- [API10:2019 Insufficient Logging & Monitoring](https://github.com/OWASP/API-Security/blob/master/2019/en/src/0xaa-insufficient-logging-monitoring.md)