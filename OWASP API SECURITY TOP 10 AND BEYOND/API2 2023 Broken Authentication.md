# Broken Authentication
##### [API2:2023 Broken Authentication](https://university.apisec.ai/products/owasp-api-security-top-10-and-beyond/categories/2152491879)
### **API2:2023 - Broken Authentication** 🚨
#### **🔍 What is Broken Authentication?**
Broken authentication occurs when an API **fails to properly secure the authentication process**, leading to unauthorized access, credential theft, or account takeover.
APIs that handle **sensitive user data** must have strong authentication mechanisms in place, such as:  
✅ Usernames and passwords  combinations
✅ Tokens (e.g., JWTs, OAuth)  
✅ Multi-Factor Authentication (MFA)

When these mechanisms are weak or misconfigured, **attackers can exploit authentication flaws** to access or manipulate user accounts.

---
### **⚠️ How Do Attackers Exploit Broken Authentication?**
### 1️⃣ **Weak Password Policy**
🚨 **Problem:** Weak password enforcement allows users to set simple passwords that can be easily guessed.  
📌 **Example:**
- Allows weak passwords (`123456`, `password`, `qwerty`).    
- No password complexity rules (uppercase, numbers, special characters).    
- Allows unlimited login attempts (brute force attack).    
- No re-authentication required when changing credentials.    

🔒 **Solution:**  
✔ Enforce **strong password policies** (min. 12 characters, mixed-case, numbers, special symbols).  
✔ **Rate-limit** authentication attempts.  
✔ Require **password confirmation** when changing email or resetting credentials.

---
### 2️⃣ **Credential Stuffing**
🚨 **Problem:** Attackers use stolen username-password combinations from previous **data breaches** to log in to an API.  
📌 **Example:**
- Attacker gets a list of leaked credentials (`email@example.com:Password123`) and **automates login attempts**.    
- API does **not detect unusual login patterns**.    

🔒 **Solution:**  
✔ Use **multi-factor authentication (MFA)**.  
✔ Implement **rate limiting** and **IP-based throttling** for login attempts.  
✔ Monitor **suspicious login patterns** (e.g., multiple failed logins from different locations).

---

### 3️⃣ **Predictable Tokens**
🚨 **Problem:** Weak token generation allows attackers to **guess or predict** authentication tokens.  
📌 **Example:**
- API issues **incremental session tokens** (`token=1001`, `token=1002`).    
- Attacker cycles through token numbers to **access active sessions**.    

🔒 **Solution:**  
✔ Use **cryptographically secure random tokens**.  
✔ Set **short token expiration times**.  
✔ Implement **token revocation mechanisms** (invalidate tokens when users log out).

---

### 4️⃣ **Misconfigured JSON Web Tokens (JWTs)**
🚨 **Problem:** JWT authentication is commonly misconfigured, leading to **token forgery or hijacking**.  
**Provide flexibility to customize algorithms used for signing the token, the key/secret that is used, and the information used in the payload.**
📌 **Example:**
- API or API providers **accepts unsigned JWTs** (allows attackers to modify tokens).    
- API does **not check JWT expiration** (old tokens remain valid).    
- JWT **contains sensitive user data** in plaintext.    
- JWT is **signed with a weak key** (`HS256` instead of `RS256`).    

🔒 **Solution:**  
✔ **Always verify JWT signatures** using a **strong cryptographic key**.  
✔ **Expire tokens** after short durations (e.g., 15 minutes).  
✔ Avoid **storing sensitive data** inside JWT payloads.

#### API Authentication
* REST requires APIs to be stateless
* APIs, therefore require users to register to acquire tokens
* Token is used for future requests

##### Issues with Authentications
* Insufficient token randomness (entropy)
* Vulnerabilities in registration process
* Password reset process
* Multi-factor authentication features
![[BrokenAuthentication.png]]
---

### 5️⃣ **Weak Password Reset & Recovery Mechanisms**
🚨 **Problem:** Poorly implemented **password reset processes** allow attackers to take over accounts.  📌 **Example:**
- API allows unlimited guesses for **password reset tokens** (e.g., 6-digit codes).    
- Attackers brute-force the reset token (`000000` - `999999`).    
- No re-authentication when changing the **email or phone number** linked to an account.
    
🔒 **Solution:**  
✔ **Limit password reset attempts** per user/IP.  
✔ Use **rate limiting** for password reset token validation.  
✔ Require users to **re-enter passwords** when changing account details.  
✔ Implement **MFA on password resets**.

---
### **🔥 How to Prevent Broken Authentication?**
✅ **Enforce Strong Authentication**
- Use **OAuth2, OpenID Connect, or other secure authentication protocols**.    
- Require **Multi-Factor Authentication (MFA)**.    

✅ **Implement Secure Password Handling**
- Use **bcrypt, PBKDF2, or Argon2** for password hashing.    
- Enforce **strong password policies**.    
- Prevent **credential stuffing** with **login attempt limits**.    

✅ **Secure Token Management**
- Use **random, non-predictable session tokens**.    
- Store **tokens securely** (e.g., HTTP-only cookies instead of local storage).    
- **Invalidate tokens** after logout or account changes.    

✅ **Protect Authentication Endpoints**
- Apply **rate limiting and brute-force protection**.    
- Require **CAPTCHAs** for excessive login attempts.    
- Implement **account lockout after multiple failed logins**.    

---
Here are the correct answers:

**Question 1:**  
✅ **API authentication is any weakness within the API authentication process.**  
(API2:2023 defines Broken Authentication as any flaw in the authentication process that can be exploited.)

**Question 2:**  
✅ **Excessive data exposure through the API.**  
(While excessive data exposure is a security issue, it is not directly related to authentication.)

**Question 3:**  
✅ **Attackers can gain control of other users' accounts, read their personal data, and perform sensitive actions on their behalf.**  
(This is the primary impact of Broken Authentication, as stated in OWASP API Security documentation.)

**Question 4:**  
✅ **A token obtained through a weak token generation process that can easily be guessed, deduced, or calculated by an attacker.**  
(Predictable tokens make it easier for attackers to hijack user sessions.)

**Question 5:**  
✅ **Use API keys for user authentication as well as client authentication.**  
(API keys should only be used for client authentication, not user authentication, as per OWASP guidelines.)

---
## Additional Resources
- [CWE-204: Observable Response Discrepancy](https://cwe.mitre.org/data/definitions/204.html)
- [CWE-307: Improper Restriction of Excessive Authentication Attempts](https://cwe.mitre.org/data/definitions/307.html)
- [CWE-798: Use of Hard-coded Credentials](https://cwe.mitre.org/data/definitions/798.html)
- [Authentication Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Authentication_Cheat_Sheet.html)
- [Key Management Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Key_Management_Cheat_Sheet.html)
- [Credential Stuffing](https://owasp.org/www-community/attacks/Credential_stuffing)
- [Web Security Academy: Authentication](https://portswigger.net/web-security/authentication)
- [Web Security Academy: JWT Attacks](https://portswigger.net/web-security/jwt)