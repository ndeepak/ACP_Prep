## 🔐 Best Practices for API Security
> These practices are designed to help **reduce risk**, **improve visibility**, and **build secure APIs** throughout their lifecycle.
---
### ⚠️ Common Sources of API Security Problems
---
### 1. **Unknown APIs**
Also called **Shadow** or **Zombie APIs**:
- **Shadow APIs**: APIs deployed by teams without formal review or registration.    
- **Zombie APIs**: Old or deprecated APIs that are still active or accessible.    

🧠 **Why it's risky**:  
If you don’t know an API exists, you can’t secure it or monitor it.
✅ **Best practices**:
- Maintain a **central API inventory**    
- Use **automated API discovery tools** (e.g., from API gateways or security scanners)    
- Regularly audit your API environment    

---

### 2. **Vulnerable APIs**
APIs with **code-level** or **design-level** flaws:
- **Cross-account access**: One user accessing data of another (BOLA)    
- **Logic flaws**: Broken business logic (e.g., bypassing payment with manipulated requests)    
- **Data exposure**: APIs returning sensitive data (e.g., full user profiles, payment data)    

🧠 **Why it's risky**: Attackers abuse these flaws to steal data, commit fraud, or gain unauthorized access.

✅ **Best practices**:
- Use **automated API-specific security tests**    
- Perform **code reviews** with a focus on **auth/authorization**    
- Use **data minimization** – only return what’s necessary

---
### 3. **Weak Runtime Defenses**
APIs deployed without proper runtime protection:
- **WAFs** are misconfigured or not updated    
- **Rate limiting** is missing or too generous    

🧠 **Why it's risky**:
- Allows **brute-force**, **credential stuffing**, and **DoS** attacks    
- Can overwhelm infrastructure and expose sensitive data

✅ **Best practices**:
- Implement **rate limiting** per IP/user/token    
- Configure **WAF rules for APIs** (not just web traffic)    
- Enable **runtime anomaly detection** (via API Gateway or SIEM)

---

### 4. **3rd Party APIs**
APIs provided by external vendors or services:
- May be **vulnerable or poorly maintained**    
- Often **don’t validate input** properly    

🧠 **Why it's risky**:
- You’re trusting someone else’s code and security    
- Vulnerabilities in 3rd-party APIs become **your risk**    

✅ **Best practices**:
- Vet third-party APIs for **security practices**    
- Apply **input validation** even on trusted sources    
- Use **API gateways** to mediate access to 3rd parties    

---

### 5. **Weak Governance**
Lack of centralized control or standards:
- No consistent way to build or secure APIs    
- Patchy or outdated documentation    

🧠 **Why it's risky**: Developers may build APIs **inconsistently**, causing **security gaps** or **compliance failures**.
✅ **Best practices**:
- Enforce **API governance policies** (naming, auth, versioning, documentation)    
- Create and follow **secure API design standards**    
- Ensure **full lifecycle documentation** is maintained    

---
### 6. **Poor Collaboration**
Security and Dev teams operate in **silos**:
- Little communication or shared responsibility    
- Security only comes in **late** (often at deployment)    

🧠 **Why it's risky**: Security bugs slip through or are caught too late, causing delays or breaches.
✅ **Best practices**:
- Promote **DevSecOps** culture    
- Use **shared tools** for testing and reporting    
- Set up **regular syncs** between Security and Engineering    

---

## ✅ Final Takeaways

|Risk Area|Impact|Best Practice|
|---|---|---|
|Unknown APIs|Invisible attack surface|API discovery, inventory|
|Vulnerable APIs|Unauthorized access, data leaks|Secure coding, API security testing|
|Weak Runtime Defenses|High-volume attacks, DoS|WAFs, rate limiting|
|3rd Party APIs|External risk exposure|Vetting, input validation|
|Weak Governance|Inconsistent security posture|Standards, secure SDLC|
|Poor Collaboration|Gaps in security implementation|DevSecOps, early engagement|

---
Top 10 API Do's and Don'ts
1. Don't trust anything (inputs/network)
2. Do validate all inputs (not just user)
3. Don't reveal useful info in error messages
4. Do expect attackers to find your APIs
5. Don't have hidden/unadvertised features
6. Don't filter data in UI - control at app level
7. Do use Gateways to control access, traffic
8. Don't forget authentication & authorization
9. Do require API documentation
10. Do continuously test, pre-production


