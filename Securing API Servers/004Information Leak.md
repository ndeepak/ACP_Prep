## 🔍 What is **Information Leak**?
**Information Leak** refers to accidentally or unintentionally revealing **sensitive system or application information** through:
- HTTP headers    
- Error messages    
- API responses    
- Comments in code or HTML    
- Log files    

One critical type of info leak is **Server Information Leak** — it reveals **which technologies** you’re running, **how they’re configured**, and even **their version numbers**.

---
## 🚨 Server Information Leak: Broadcasting Tech Stack
### ❗What Happens?
By **default**, many web servers and platforms "advertise" their tech stack in HTTP headers.
Example:
```makefile
Server: nginx/1.18.0
X-Powered-By: Express
X-Version: 3.2.1
```

These headers **reveal unnecessary and potentially dangerous details**:
- The type of server (Apache, Nginx, etc.)    
- The framework/language (Express.js, PHP, etc.)    
- Exact version numbers (useful to find CVEs)    

---
### 🧠 Why is this BAD?
Attackers use this leaked info to:
- Search public CVE databases (like [CVE Details](https://www.cvedetails.com))    
- Look for known exploits or weaknesses in that version    
- Tailor attacks (e.g., bypassing filters, knowing file structures, etc.)

---
## 🔍 How to **Detect** Server Info Leak
### 1. Use a tool like:
- `curl -I http://target.com`    
- `httpie`: `http http://target.com`    
- **Browser Dev Tools** (Inspect > Network > Headers)    
- `Burp Suite` or Postman
### 2. Look for:

| Header          | Meaning                          |
| --------------- | -------------------------------- |
| `Server:`       | Web server software & version    |
| `X-Powered-By:` | Language/framework powering site |
| `X-Version:`    | App/API version                  |

---
## 🛡️ How to **Prevent Server Information Leak**
### ➤ **Uvicorn** (Python ASGI Server):
`uvicorn main:app --host 0.0.0.0 --port 8000 --no-server-header`
- The `--no-server-header` flag disables `Server: uvicorn`.

---
### ➤ **Nginx**:
In `nginx.conf`:
`server_tokens off;`
- This removes `Server: nginx/1.18.0` and changes it to just `Server: nginx` or nothing.

---

### ➤ **Express (NodeJS)**:
#### 1. Disable `X-Powered-By`:
`app.disable('x-powered-by');`

#### 2. Or use Helmet.js (security middleware):
`npm install helmet`

```js
const helmet = require('helmet');
app.use(helmet());

```
Helmet automatically hides `X-Powered-By` and sets other security headers.

---
## ✅ Bonus: Other Recommendations

| Server        | Fix Command / Config                                      |
| ------------- | --------------------------------------------------------- |
| Apache        | `ServerTokens Prod` + `ServerSignature Off`               |
| Django        | Set `SECURE_PROXY_SSL_HEADER`, remove default error views |
| IIS (Windows) | Remove `X-Powered-By` using web.config                    |
| Tomcat        | Edit `server.xml` & `web.xml` files to mask version       |

---

## 🧪 Test Challenge
1. Open Dev Tools > Network > Inspect headers for any website.    
2. Identify exposed headers.    
3. Search those versions in [CVE Details](https://www.cvedetails.com).    
4. Propose a fix using server config.

### ✅ **Question 1: What Header is NOT a concern for sending to clients?**
**Correct Answer: `Cache-Control`**
- **Why?**  
    `Cache-Control` is a standard and **useful** header that helps **browsers or CDNs** manage how resources are cached.  
    It doesn’t leak any sensitive information.
- **Others like:**    
    - `Server`: Leaks server type/version.        
    - `X-Powered-By`: Leaks framework used (e.g., Express, PHP).        
    - `X-Version`: Can reveal app/API version — can be exploited if vulnerable.

---
### ✅ **Question 2: What is a known vulnerability commonly called?**
**Correct Answer: `CVE`**
- **Why?**  
    CVE = **Common Vulnerabilities and Exposures**  
    Example: `CVE-2021-22047`  
    It’s a universal identifier for publicly disclosed security flaws.
    
- **Wrong Options:**
    - Malware = malicious software.        
    - Bug = general programming error (may or may not be a security issue).        
    - Ticket = used in project management or issue tracking systems.        

---

### ✅ **Question 3: Response Headers are:**
**Correct Answer: `Information sent to all client applications`**
- **Why?**  
    HTTP response headers are metadata **automatically sent** by servers with every response.  
    They are visible to any client (browser, Postman, curl).
    
- **Wrong Options:**    
    - Rarely needed? ❌ Many headers are essential (CORS, auth, caching, etc.).        
    - Secure communication? ❌ Headers themselves are not secure unless HTTPS is used.        
    - Exclusive API data? ❌ They are part of the HTTP protocol, not exclusive.
