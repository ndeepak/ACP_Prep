# API Attack Analysis
##### [API Attack Analysis](https://university.apisec.ai/products/api-security-fundamentals-2025/categories/2157142250)

![[Pasted image 20250415165337.png]]
# Why API Security
##### [API Attack Analysis](https://university.apisec.ai/products/api-security-fundamentals-2025/categories/2157142250)
**Why bother with API Security at all?**
APIs (Application Programming Interfaces) are **core to modern apps**—they connect:
- Web and mobile frontends to backend services    
- 3rd party services (e.g., payment gateways, maps)    
- Internal microservices
* Its the right thing to do?
* Reduce risk and harm
* We have to - compliance
#### 🔹 Reasons API Security is **critical**:
- **The right thing to do:** Ethical responsibility to protect user data.    
- **Risk reduction:** Avoid data breaches, fraud, and legal liabilities.    
- **Compliance:** Meet laws like GDPR, HIPAA, PCI-DSS.    
- **Business Reputation:** Security incidents = **loss of trust**.


#### 💬 Questions to Reflect On:
* Is API security a priority?
* Is the business investing in it?
* Why now?
- Is **API security** considered a **top priority** in your org?    
- Is the business investing in **tools, testing, and training**?    
- Why is it important **now** (not later)?

# Threat Modeling

| Step           | Description                                        |
| -------------- | -------------------------------------------------- |
| 🔍 Identify    | APIs, endpoints, data flows, 3rd parties           |
| 🔎 Assess      | Vulnerabilities, logic flaws, access controls      |
| 📊 Probability | Estimate how likely an attack is                   |
| 💣 Impact      | Understand potential damage                        |
| 🛡️ Mitigate   | Design protections (rate limits, auth, validation) |

> Formula:  
> **Risk = Threat × Vulnerability × Likelihood × Impact**

#### 🧭 What do attackers want?
- **Personal data** (name, phone, address)    
- **Financial info** (cards, banking)    
- **Corporate secrets** (espionage)    
- **Free service abuse** (fraud)    
- **Critical infrastructure** (sabotage, terrorism)

What do you have that attackers want?
* Personal information: consumer data
* Financial information: banking data, credit cards
* Corporate data: espionage, IP, corporate data
* Fraud: financial profit, free use
* Critical infrastructure: activism, mayhem, terrorism

How are APIs used in your business?
* Web site functionality 
* Mobile application 
* Customer/partner API access 
* Internal microservices 
* 3rd party data and services


Threat Modeling
* Core of every cybersecurity framework
* Risk = Threat * Vulnerability * Likelihood * Impact
* Access the overall risk of each threat and prioritize mitigation
![[ThreatModelingRISK.png]]



### ✅ **Question 1: Why is rate limiting not a perfect defense against high-volume attacks?**
> **Correct Answer:** **All of the above**

**Explanation:**  
Attackers bypass rate limiting by:
- Sending requests **under the threshold**    
- Using **thousands of IPs (botnets)**    
- Employing **residential proxies** to look legitimate  
    ➡️ Thus, **rate limiting alone** is **not sufficient**.
    

---

### ✅ **Question 2: What percentage of API breaches are attributed to OWASP 1, 2, and 3 vulnerabilities?**
> **Correct Answer:** **90%**

**Explanation:**  
The **top 3 OWASP API vulnerabilities**—BOLA (#1), Broken Authentication (#2), and Excessive Data Exposure (#3)—are responsible for the **vast majority of real-world API breaches**.

---

### ✅ **Question 3: During a threat modeling exercise, which question should you ask first?**
> **Correct Answer:** **What do we have that attackers want?**

**Explanation:**  
This is the **first and most critical** question in threat modeling—it helps identify **assets** that need protection.

---

### ✅ **Question 4: Why do attackers often target APIs?**
> **Correct Answer:** **To access sensitive data like PII or corporate information**

**Explanation:**  
APIs often expose **sensitive backend data**. Attackers exploit vulnerabilities to **harvest data** such as:
- PII (Personally Identifiable Information)    
- Financial records    
- Internal documents    

---
### ✅ **Question 5: Which defense mechanism is most associated with preventing high-volume attacks, but is not perfectly effective?**
> **Correct Answer:** **Rate limiting**

**Explanation:**  
Rate limiting helps control **abuse and DoS attacks**, but it's not foolproof due to:
- IP rotation    
- Throttling techniques    
- Distributed bot attacks    

---
### ✅ **Question 6: In API security, why is “Broken Authorization” a critical issue?**
> **Correct Answer:** **It allows unauthorized users to access other users’ data**

**Explanation:**  
Broken authorization issues (like BOLA or function-level flaws) can **expose sensitive resources** to users who **shouldn’t have access**.


## Teaching Tips
1. **Visualize APIs**: Show real JSON API response examples.    
2. **Hands-on**: Use tools like Postman or Burp to test endpoints.    
3. **Threat Modeling Exercise**:    
    - Let interns map a fake API system.        
    - Ask them: "Where are the valuable targets?"

## 🚦 Summary Table

|Topic|Risk|Defense|
|---|---|---|
|BOLA|Unauthorized data access|Strong access checks|
|Excessive Exposure|Data leakage|Minimize data returned|
|Broken Auth|Account takeover|Token/session management|
|DoS|App downtime|Rate limiting, IP filtering|
|SSRF|Backend access|Input validation, metadata protection|
