## 🔐 **Cross-Origin Resource Sharing (CORS) – In Detail**
---
### ✅ What is CORS?
**CORS (Cross-Origin Resource Sharing)** is a **browser-based security mechanism** enforced by the **client-side (browser)**, and **configured by the server** using specific HTTP headers.
> "CORS tells the browser whether or not a web page from one origin is allowed to access a resource from another origin."
---
### 🧱 Core Concepts of CORS:
#### 1. **Origins**
- **Origin = Protocol + Host + Port**    
- CORS works based on origin checks.    
- If a request comes from a **different origin**, the browser **blocks it by default**, unless the server explicitly allows it.   
#### 2. **Credentials**
- Refers to **cookies, HTTP authentication, and client-side SSL certificates**.    
- Controlled by:    
    - `Access-Control-Allow-Credentials: true`        
    - Requires **exact origin match** (cannot use `*` with credentials).        
    - Browser must send request with: `withCredentials: true` in JS.
#### 3. **Methods**
- These are the HTTP methods the browser is allowed to use in cross-origin requests.    
- Defined in header:    
    - `Access-Control-Allow-Methods: GET, POST, PUT`        
#### 4. **Headers**
- Custom headers the client is allowed to send.    
- Defined in header:    
    - `Access-Control-Allow-Headers: Content-Type, Authorization`

---
## ❓Why Use CORS?
Because without it, any malicious website can make authenticated API calls to your server on behalf of a logged-in user.
### Examples of What You Protect:
- 🔐 User Data (e.g. banking, medical, personal)    
- 📜 Intellectual Property (e.g. source code, algorithms)    
- 🎨 Branding (e.g. your content rendered somewhere else without permission)

---
## 🚨 When Does CORS Help?

|Scenario|CORS Behavior|
|---|---|
|**Malicious system (cURL, Postman)**|CORS doesn't protect – it's enforced by browsers only|
|**Malicious site (JS in browser)**|✅ Browser blocks requests if CORS not allowed|
|**Unsuspecting users**|✅ Protected from cross-origin hijacking|

---

## ⚠️ Common CORS Vulnerability Scenario
1. Developer sets up a new API server.    
2. API is meant to be accessed by the main site (e.g., `https://frontend.company.com`).    
3. Developer tests locally (`http://localhost:3000`) and hits a CORS error.    
4. Developer "fixes" it with:    
    `Access-Control-Allow-Origin: *`    
5. This header goes to production, unintentionally exposing **user data to any origin**.

---
## 🛡️ Secure CORS Implementation (CORS Solution)
✅ **Explicitly set these headers on your server:**
```http
Access-Control-Allow-Origin: https://your-site.com
Access-Control-Allow-Methods: GET, POST, PUT
Access-Control-Allow-Headers: Content-Type, Authorization
Access-Control-Allow-Credentials: true
```

### Best Practices:
- **DO NOT** use `Access-Control-Allow-Origin: *` if handling credentials.    
- **Whitelist specific origins** instead of allowing all.    
- Validate the `Origin` header and dynamically return CORS headers only for trusted domains.    
- Enable only required methods and headers.    
- Secure **preflight requests** (OPTIONS requests) properly.

---
### 🧪 Testing CORS Misconfigurations
You can test with tools like:
- **Burp Suite** → Intercept requests and manipulate the `Origin` header.
- **curl**:
    `curl -H "Origin: https://evil.com" -I https://target.com/api`
    → See if it reflects `Access-Control-Allow-Origin: https://evil.com`.

---
## 💣 CORS Exploitation
If a server responds with:
```http
Access-Control-Allow-Origin: *
Access-Control-Allow-Credentials: true
```

That’s a **severe misconfiguration**. It allows any site to make credentialed requests on behalf of users (e.g., steal cookies, sessions).
### Exploitation steps:
1. Host a malicious HTML/JS page.    
2. Have a logged-in victim visit it.    
3. JS on your site sends a `fetch()` request to the vulnerable API.    
4. The browser sends cookies due to `withCredentials: true`.    
5. The server allows it because of the misconfigured CORS.    
6. You get access to sensitive user data.    

---
### 📌 Summary Table

|Header|Purpose|
|---|---|
|`Access-Control-Allow-Origin`|Specifies allowed origin(s)|
|`Access-Control-Allow-Methods`|HTTP methods that are allowed|
|`Access-Control-Allow-Headers`|Custom headers allowed|
|`Access-Control-Allow-Credentials`|Whether cookies/auth can be included|

---
