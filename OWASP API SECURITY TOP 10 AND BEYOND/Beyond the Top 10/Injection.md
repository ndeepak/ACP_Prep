# Injection
##### [Beyond the Top 10](https://university.apisec.ai/products/owasp-api-security-top-10-and-beyond/categories/2152492281)
---
## **Understanding Injection Attacks in APIs**
Injection vulnerabilities have been among the **most severe security risks** for over two decades. These occur when an attacker sends **malicious input** to an API, which is then **executed** by the underlying system, such as a database or operating system.
### **Common Types of Injection Attacks**
1. **SQL Injection (SQLi)**    
    - Attackers manipulate SQL queries to **bypass authentication**, **steal data**, or **modify databases**.        
    - Example:
```sql
SELECT * FROM users WHERE username = '' OR '1'='1' -- ' AND password = 'password';
```
- If an API accepts this input **without sanitization**, it will return **all user records**.
        
2. **NoSQL Injection**    
    - Targets **MongoDB, CouchDB, and Firebase**, which do not use traditional SQL queries.   
    - Example: Sending this JSON request:
```json
{ "username": { "$ne": null }, "password": { "$ne": null } }
```     
- If an API does not validate input properly, it could **return all users**.
        
3. **Command Injection**    
    - Executes **shell commands** on the underlying OS.        
    - Example:
```json
curl -X POST -d "username=admin; rm -rf /" http://example.com/api/login
```
   - This could **delete important files** if executed.
        
4. **LDAP Injection**    
    - Manipulates LDAP queries used for authentication.        
    - Example:        
```scss
(&(user=*)(password=*)(uid=*)(|(uid=*)(cn=*)))
```
   - If not filtered, an attacker can **bypass authentication**.
        
5. **XML Injection**    
    - Injects malicious **XML payloads** into APIs using XML data.        
    - Example:
```xml
<!DOCTYPE foo [<!ENTITY xxe SYSTEM "file:///etc/passwd">]>
<user>
  <name>&xxe;</name>
</user>
```
   - This technique, known as **XXE (XML External Entity)** injection, can **leak sensitive files**.      

---
## **How Attackers Find Injection Vulnerabilities**
1. **Verbose Errors** – APIs returning detailed SQL/OS errors give clues about vulnerabilities.    
2. **HTTP Response Codes** – Unexpected `500 Internal Server Errors` may indicate an injection point.    
3. **Fuzzing & Scanning** – Attackers use **Burp Suite, SQLmap, or custom scripts** to automate attacks.   
Example:
```bash
sqlmap -u "http://example.com/api/users?id=1" --db
```

This **automatically tests** for SQL injection in API requests.

---
## **Impact of Injection Attacks**
- **Data leaks** (exposure of sensitive information).    
- **Authentication bypass** (logging in as admin without credentials).    
- **System takeover** (executing system commands).    
- **Denial of Service (DoS)** (API crashes due to unexpected input).    

---
## **Preventing Injection Attacks**
1. **Use Parameterized Queries**    
    - Example (in Python with SQL):
```python
cursor.execute("SELECT * FROM users WHERE username = ?", (username,))
```
- This prevents SQL injection by treating input as **data** rather than **executable code**.
        
2. **Validate and Sanitize Inputs**    
    - Use **whitelists** instead of blacklists.        
    - Example (only allowing alphanumeric usernames):        
```python
import re
if not re.match("^[a-zA-Z0-9_]+$", username):
    return "Invalid username"
```
        
3. **Escape Special Characters**    
    - Example: `"<script>alert(1)</script>"` should be stored as `&lt;script&gt;alert(1)&lt;/script&gt;`.
        
4. **Use a Web Application Firewall (WAF)**    
    - Tools like **ModSecurity, AWS WAF, or Cloudflare WAF** can detect and block injection attempts.
        
5. **Limit API Responses**    
    - Example: Instead of returning **all records**, limit the response to **10 per request**.
        
6. **Regular Security Testing**    
    - Use tools like:        
        - **Burp Suite** (Manual API security testing)            
        - **ZAP (Zed Attack Proxy)** (Automated security scans)            
        - **SQLmap** (Automated SQL injection testing)
---
## **Example API Injection Attack**
### **Vulnerable API Endpoint**
```http
POST /api/v1/login HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "username": "' OR '1'='1",
  "password": "password"
}
```
If the API does **not use prepared statements**, this could **bypass authentication**.
### **Secure Fix**
- Use **parameterized queries** and **validate input** before processing.    
- **Never** expose **detailed error messages**.

---
## **Final Thoughts**
🔹 **Injection is one of the most critical API vulnerabilities** that allows attackers to manipulate backend systems.  
🔹 **Best protection methods include** input validation, parameterized queries, and Web Application Firewalls (WAFs).  
🔹 **Automated tools like SQLmap, Burp Suite, and OWASP ZAP** can help test API security.

---
## Additional Resources
- [OWASP Injection Flaws](https://www.owasp.org/index.php/Injection_Flaws)
- [SQL Injection](https://www.owasp.org/index.php/SQL_Injection)
- [NoSQL Injection Fun with Objects and Arrays](https://www.owasp.org/images/e/ed/GOD16-NOSQL.pdf)
- [Command Injection](https://www.owasp.org/index.php/Command_Injection)
- [CWE-20: Improper Input Validation](https://cwe.mitre.org/data/definitions/20.html)
- [CWE-200: Exposure of Sensitive Information to an Unauthorized Actor](https://cwe.mitre.org/data/definitions/200.html)
- [CWE-319: Cleartext Transmission of Sensitive Information](https://cwe.mitre.org/data/definitions/319.html)
- [Web Security Academy: OS Injection](https://portswigger.net/web-security/os-command-injection)
- [Web Security Academy: SQL Injection](https://portswigger.net/web-security/sql-injection)
- [Web Security Academy: XML Injection](https://portswigger.net/web-security/xxe)

---
