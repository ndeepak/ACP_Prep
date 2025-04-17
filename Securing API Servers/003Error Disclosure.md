## 🛑 What is **Error Disclosure**?

> **Error Disclosure** is when a system exposes too much technical information through its error messages, which could be used by an attacker to compromise the system.
Examples of exposed information:
- File paths (`/var/www/html/index.php`)    
- Stack traces    
- Internal APIs or endpoints    
- Database names    
- Technology stack (e.g., "Spring Boot", "Node.js", "MySQL")    
- Detailed authentication failure messages    

---
## 🔍 Why Error Messages Matter
### 💡 Legitimate Need:
- **Developers** need detailed errors to fix issues.    
- **System engineers** need logs to monitor and troubleshoot.    
- **Hackers**—if errors are too verbose—can use them for **reconnaissance**.

> 💥 Example: If an attacker enters an email to reset password and gets:
- "Email not found" → Email **doesn’t exist**    
- "Check your email for reset link" → Email **exists**    

This allows **email enumeration** – a common information disclosure flaw.

---
## 🔧 Error Handling in Different Languages
### 🐍 Python – `try` and `except`
```python
try:
    file = open("important.txt", "r")
    print(file.read())
except FileNotFoundError as e:
    print("File not found.")  # For user
    print(f"Log: {e}")        # For logs
```
✔️ Catch specific error  
✔️ Show generic user error  
✔️ Log developer details

---
### 🟩 Node.js – `try` / `catch` + Async/Await
```javascript
const fs = require('fs/promises');

async function readFile() {
  try {
    const data = await fs.readFile("important.txt", "utf8");
    console.log(data);
  } catch (err) {
    console.log("Something went wrong."); // Generic for user
    console.error("Log:", err); // Internal log
  }
}
readFile();
```

✔️ Use async/await properly  
✔️ Don’t send internal stack trace to clients in API responses

---

### ⚠️ Why Is Bad Error Disclosure Dangerous?
#### 📌 CVE-2021-22047
> A bug in Spring Data REST allowed attackers to **bypass security** and access unauthorized URIs due to overly descriptive error messages.
**Problem:** Errors leaked internal URI structures  
**Impact:** Attackers could explore endpoints not meant to be public  
**Fix:** Generic error messages + hardened resource mapping
🔗 [CVE Details](https://spring.io/security/cve-2021-22047)
---
## 🛡️ **Being Defensive**: How Can This Be Exploited?

|Situation|Exploit|
|---|---|
|Login error says: "User not found"|✅ Email/User enumeration|
|API returns stack trace on error|✅ Find framework and version|
|Error mentions DB error|✅ SQL Injection hint|
|Path disclosure: `E:\webapp\secret.txt`|✅ Directory structure exposure|

---

## 🧪 **Best Approach to Error Handling**
### ❌ Wrong Way (Insecure):
```json
{
  "error": "SQLSyntaxErrorException: unknown column 'password1'"
}
```

### ✅ Secure Way:
```json
{
  "error": "Something went wrong. Please try again later."
}
```
- Internally, log the detailed error.    
- For users, keep it **vague and generic**.

---
## 🖥️ **UI vs API Error Handling**
### ✅ UI (Frontend)
- Use friendly, branded messages.    
- Example: GitHub    
    > _"This is not the web page you are looking for."_    
### ✅ API (Backend)
- Respond with:
    `{ "message": "Unauthorized request." }`
- Use proper HTTP status codes:    
    - `401 Unauthorized`        
    - `403 Forbidden`        
    - `404 Not Found`        
    - `500 Internal Server Error`        

---
## 📜 Error Handling Best Practices (Summary)
### ✅ **DO**
- Error early (fail fast)    
- Log detailed errors internally    
- Customize user-facing messages    
- Test how error messages behave under attack conditions    
- Sanitize and structure log output    

### ❌ **DO NOT**
- Leak stack traces    
- Show usernames, emails, internal files    
- Ignore or bypass errors (silent failures)    
- Allow detailed dev exceptions in production    

---
## 📘 Reference:
- [OWASP Error Handling Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Error_Handling_Cheat_Sheet.html)
---
