# Three Pillars of API Security
##### [Three Pillars of API Security](https://university.apisec.ai/products/api-security-fundamentals-2025/categories/2157142278)

1. Governance: Developing secure APIs
2. Monitoring: Detecting threats in production
3. Testing: Ensuring APIs are free of flaws


## Governance 
Goal: to provide consistency and standard

Two sides:
#### 1. Awareness
* Know your APIs
	* Get full inventory APIs
	* Know your infrastructures
	* Standardize API deployment process
	* Mandate API documentation
* Know your data
	* 	
* Know your risks

##### Documentations: OpenAPI Specification (Swagger)
* Industry standard for REST APIs
* Defines API capability (contract)
	* Title, description, version
	* Base-URL
	* Endpoints, paths
	* Request, response payloads
	* Authentication requirements
	* Parameters, data types
	* Methods
* Machine-readable (YAML, JSON)
* Aids development, 3d party integration
* Also aids security testing
* Manually or auto-generated
* Control what's public vs private
* Retire old documentation
https://swagger.io/

##### Style Guides: Promote Governance, Consistency
* Authentication: type (basic, token, certificate), implementation
* Authorization: who has access to what, where enforced
* Naming Conventions: URIs as nouns, Methods as verbs, pluralization, hierarchy, case, language, no jargon/ abbreviations
* Error Codes: status codes, reference ID, human readable messages
* Versioning: when to increment, when not, types of versions
* Units, Formats, Standards: date/time formats, timezones

#### 2. Policy & Process
* API Development process
* API documentation
* Design and Style guides

Benefits
* Consistency
* Setting expectations
* Establishing standard processes
* Enforcing security


## Monitoring
1. Runtime Protection
* Policy enforcement
* Authentication
* Traffic filtering

1. Threat Detection
* Fraudulent traffic
* Volumetric attacks
* Incident response

3. Control Validation
* Verify API controls
* Uncover anomalies
#### Proactive: Block
* API Gateway
* Web App Firewall
#### Reactive: Alerting
* Logging, SIEM
* Runtime API Threat
* Management

#### API Discovery
* Monitoring can aid API inventory efforts
	* Identify API endpoints in use
	* Discover undocumented/unknown APIs
* Comprehensive discovery requires more sources:
	* API Gateway, Web Application Firewall
	* Code repository
	* Application testing, crawling
* Reliance on traffic based-discovery misses:
	* Internal API traffic not seen by traffic analysis tool
	* Pre-production APIs
	* Unexercised endpoints

**Challenge**: API attacks pass through defenses because they look legitimate traffic.
```
GET /api/user?id=' OR 1=1--
```

```
USER ID 10: DELETE /api/transfer?id=123
```
Which is valid? and Good?


## Testing
Its challenges:
1. Security
* Unsecured Endpoints
* Incremental IDs
* Injection, XSS
* Fuzzing, input validation
* Error handling

2. Data
* Excessive data exposure
* Sensitive data exposure
* Personal, health, bank data
* File, directory exposure
* Data exfiltration

3. Logic
* Object ID manipulation
* Cross-account access
* API function abuse
* Role-based access control
* Authorization gaps

API Testing approaches:
Option1: Do Nothing
Option2: Do it yourself, Postman, Burp, ZAP, Simulations Attacks
Option3: Pay someone else to do it. Pentesting, Ethical Hackers, WhiteBox Testing
**Option4:** Automate it to test, https://www.apisec.ai/sign-up


---

### ✅ **Question 1**
**Q:** What is the primary goal of API governance?  
**A:** _Enforcing consistent processes for API development and deployment_  
**Reasoning:**  
API governance ensures APIs are **developed, tested, deployed, and maintained** using standardized practices. It focuses on **consistency**, **compliance**, and **quality**, not directly on threat detection (which is a runtime or security tool's job).

---

### ✅ **Question 2**
**Q:** Which of the following is NOT a key component of API documentation?  
**A:** _User activity logs_  
**Reasoning:**  
API documentation typically includes:
- **Base URLs**, endpoints    
- **Authentication requirements**    
- **Data formats, methods (GET, POST, etc.)**  
    User activity logs are part of **monitoring and logging**, not documentation. They help in runtime analytics, not in API interface documentation.
---
### ✅ **Question 3**
**Q:** What is a limitation of API security monitoring tools?  
**A:** _They often lack context to distinguish malicious from legitimate requests_  
**Reasoning:**  
Monitoring tools can **log traffic**, detect patterns, and even flag anomalies. However, without **context** (user intent, business logic, session state), it's hard to know if a request is genuinely malicious. This is a common limitation—they’re **blind to logic flaws** or **business-layer abuse**.

---
### ✅ **Question 4**
**Q:** What is the most common API documentation format?  
**A:** _OpenAPI Specification (OAS)_  
**Reasoning:**  
OAS (formerly Swagger) is the **industry standard** for API documentation. It describes:
- Endpoints    
- Request/response format    
- Parameters    
- Authentication  
It's widely supported in **tools, gateways, and testing frameworks**. YAML and JSON are _formats_ used **inside OAS**, but not documentation formats themselves.   

---
### ✅ **Question 5**
**Q:** Why should API testing be continuous and automated?  
**A:** _To detect vulnerabilities before deployment_  
**Reasoning:**  
Modern APIs are **frequently updated**. Continuous and automated testing ensures:
- Vulnerabilities are caught **early**    
- It's **scalable** and efficient    
- Prevents release of vulnerable APIs   
This is **Shift Left Security** – test **before** deployment, not just after.   

---
### ✅ **Question 6**
**Q:** Which approach allows for comprehensive and frequent API testing?  
**A:** _Automated API security scanning_  
**Reasoning:**  
Automated scanners:
- Run **regularly and frequently**    
- Are **integrated in CI/CD pipelines**    
- Help with **early vulnerability detection**  
Manual reviews and annual pentests are important but **not scalable** or frequent enough for modern agile API environments.    

---
### 🧠 Summary of Key Takeaways:

|Concept|Insight|
|---|---|
|**Governance**|Ensures consistency in development/deployment|
|**Documentation**|Should include endpoints, auth, methods—not logs|
|**Monitoring Limitation**|Lacks deep context for intent-based attacks|
|**OAS**|Standard format for describing APIs|
|**Continuous Testing**|Helps find bugs **before** going live|
|**Automation**|Critical for frequent, large-scale testing|

---

