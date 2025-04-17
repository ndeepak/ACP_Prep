# 🔐 Path Traversal Vulnerabilities – Notes

## 📌 What is a Path Traversal Vulnerability?
- A **path traversal vulnerability** occurs when a user can manipulate input to access **files or directories outside the intended scope** of an application.    
- Also known as: **Directory Traversal**.    
- The goal: Escape the web root directory and **access sensitive files** (e.g., `/etc/passwd` on Linux).
---

## ⚠️ Common Causes
1. **Improper Input Validation**    
    - Using user-supplied input (query params, cookies, headers, etc.) **directly in file paths** without sanitization.        
2. **Insecure Server Configuration**    
    - Allowing access **above the web root**.        
    - **Directory listing** enabled (especially common on Apache if misconfigured).        
3. **Loose API Specifications**    
    - Accepting arbitrary **string parameters** without strict definitions or max lengths.        
    - Lack of constraints leads to attack payloads slipping through.        

---
## 🧪 Common Exploitation Techniques
- Using `../` (dot-dot-slash) to traverse up directories.    
- Encodings:    
    - URL encoding: `%2e%2e/`        
    - Unicode: `%u2216`        
    - Double encoding to bypass weak filters.        
- Placing payloads in:    
    - **Cookies** (`template=../../../etc/passwd`)        
    - Query strings (`?file=../../../../etc/shadow`)        
    - Headers        
---
## 📉 Real-World Implications
- Allows access to:    
    - System files: `/etc/passwd`, `/etc/shadow`, `.env`        
    - Source code: `.git`, backup files        
    - Application configs        
- Can lead to:    
    - Information disclosure        
    - Further exploitation when chained with other vulnerabilities        

---
## 🧰 Tools and Testing
- Automated tools (e.g., **dirsearch**, **Burp Suite**, **crAPI tools**) can attempt thousands of traversal payloads.    
- Manual test:    
    - Change parameter values to `../../../secret.txt`        
    - Monitor behavior and responses        
---
## ✅ Mitigations and Best Practices
### 1. **Validate Input Properly**
- **Whitelist** acceptable input values.    
- Use IDs instead of raw file names.    
- Apply **length limits** to parameters.    
### 2. **Avoid Dynamic Includes**
- Avoid using user input in:    
    - `include()`        
    - `require()`        
    - `open()` with untrusted paths.        
### 3. **Server Hardening**
- Disable directory listing.    
- Restrict file access **below web root** only.    
- Ensure sensitive files aren’t stored in or under the web root.    
### 4. **Gateway/WAF-Level Filtering**
- Enforce **strong schema validation** at the API Gateway or WAF.    
- Block known traversal patterns before reaching the app server.    
### 5. **Isolate the Web Root**
- Place the web root on a **separate drive/volume** if possible.    
### 6. **Fail Securely**
- If input is invalid → **throw an error**, log it, and deny access.    

---
## 🔍 Example of Bad Code
```php
// Dangerous: includes user-controlled template value directly
include($_COOKIE['template']);
```
## 🛡️ Secure Pattern
```php
// Safe: use mapping ID to path from a controlled list
$templates = ['default' => 'templates/default.php'];
$templateID = $_COOKIE['template_id'];
include($templates[$templateID]);
```

---

## 📚 CVEs and Real-World Cases
- Thousands of path traversal-related **CVEs** exist.    
- Recent high-profile examples include:    
    - AutoGPT path traversal bug        
    - Exploits combining traversal + arbitrary file download        

---
## 📝 Summary
- Path traversal is **still common** and **easy to exploit**.    
- Avoid dynamic file handling based on unvalidated input.    
- Harden your app **at every layer**:    
    - Code        
    - Config        
    - API specs        
    - Web/Application firewall    
---


### **Question 1**
**Path Traversal vulnerabilities are:**
✅ **Any file access that wasn’t intended**  
➡️ _Correct_. Path traversal vulnerabilities occur when a user can access files or directories that are outside of the intended directory by manipulating path inputs (like `../../../etc/passwd`).
❌ _Typing in different paths in the URL_  
➡️ Not always a vulnerability unless it results in unauthorized file access.

---
### **Question 2**
**The parameter definition in a spec can help prevent path traversal by:**
✅ **Specifically disallowing filenames**  or Blocking lengthy bypasses of encoding
➡️ _Correct_. If the spec (API or web spec) restricts parameters to known values and disallows arbitrary file names, path traversal can be mitigated.
❌ _Enabling the “No path changes” option_  
➡️ No such standard setting exists in specs.

---
### **Question 3**
**Files that are ok to be kept at the webroot are:**
✅ **Only the ones to be served in responses**  
➡️ _Correct_. The webroot (`/var/www/html`, etc.) should only contain public content—HTML, images, CSS, JS. Configuration files, logs, source code, and secrets must **not** be there.
❌ _Any system and configuration files used for the web service_  
➡️ Dangerous. These should be stored outside the webroot.