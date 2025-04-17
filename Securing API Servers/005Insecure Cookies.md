# Insecure Cookies
## 🔹 What are Cookies?
Cookies are **small pieces of data stored in the browser** to maintain stateful information like:
- Session IDs    
- User preferences    
- Login status    
- Tracking info    
They’re set using the `Set-Cookie` HTTP response header, and sent back via the `Cookie` request header.
---
## 🔸 Common Cookie Contents
Cookies can contain:

|Type|Example|
|---|---|
|**Boolean**|`loggedIn=true`|
|**Base64**|`user=YWRtaW46MTIzNA==` (base64 of `admin:1234`)|
|**Integer**|`userid=1245`|
|**Timestamps**|`expires=1684200000`|
|**Session ID**|`JSESSIONID=F04A12C93BA...`|
|**Paths**|Used to limit scope of cookies (`Path=/`)|

**Set-Cookie** header example:
`Set-Cookie: sessionId=abc123; Path=/; Secure; HttpOnly; SameSite=Strict`

---

## 🔹 Cookie Decoding
### 1. **Extracting & Understanding**
Use browser dev tools or tools like Burp Suite to extract cookies.
```zsh
# curl example
curl -I https://example.com
# Look for Set-Cookie in response
```
### 2. **Look for interesting data**
- IDs    
- Tokens    
- Base64 blobs    
- `admin=true`, `role=1`   

### 3. **Decode if needed**
Python example to decode base64 cookie:
```python
import base64
cookie = "YWRtaW46cGFzc3dvcmQ="
decoded = base64.b64decode(cookie).decode()
print(decoded)  # admin:password
```


---

## ❗ The Problem: Insecure Cookie Risks
### ⚠️ 1. **Cookie Forging**
If a cookie like `role=admin` is not protected, a user might modify it and gain elevated access.
`Cookie: user_id=1023; role=admin`

### ⚠️ 2. **XSS - Stealing Cookies**
If cookies are not marked `HttpOnly`, JavaScript can access them:
`document.cookie; // attacker steals session cookie via XSS`

### ⚠️ 3. **Session Hijacking via HTTP**
If `Secure` flag is missing, cookies are sent over **unencrypted HTTP**.

---
## ✅ The Solution: Secure Cookie Attributes

|Attribute|Description|
|---|---|
|**Secure**|Sends cookie only over HTTPS|
|**HttpOnly**|Disallows JS access to cookie|
|**SameSite**|Protects against CSRF (Strict/Lax/None)|
|**Domain/Path**|Restricts where cookies are sent|

---

### 🍪 Secure Cookie Example
```http
Set-Cookie: sessionId=abc123;
  Path=/;
  Secure;
  HttpOnly;
  SameSite=Strict;
  Domain=example.com
```
### 🛡️ Express.js Example (NodeJS Backend)
```js
res.cookie("sessionId", "abc123", {
  secure: true,
  httpOnly: true,
  sameSite: 'strict',
  domain: 'example.com',
  path: '/'
});
```

---
### 🛡️ Django Example (Python Backend)
In `settings.py`:
```python
SESSION_COOKIE_SECURE = True
SESSION_COOKIE_HTTPONLY = True
SESSION_COOKIE_SAMESITE = 'Strict'
```

---
## 💡 Offensive Mindset (Security Testing Use Case)
1. **Tamper with cookie values manually** (admin=true).    
2. **Base64-decode any suspicious-looking string.**    
3. **Remove `HttpOnly` flag to test XSS cookie stealing (lab scenarios).**    
4. **Try setting SameSite=None; Secure with http** – browser should reject.    
5. **BurpSuite → Repeater → Try fuzzing cookies** with altered sessions.    

---
## 🔚 Summary

| Do ✅                                 | Don’t ❌                            |
| ------------------------------------ | ---------------------------------- |
| Use `Secure`, `HttpOnly`, `SameSite` | Store sensitive data in plain text |
| Keep cookies minimal & encrypted     | Trust cookie input blindly         |
| Validate cookie content server-side  | Let JS access session cookies      |

---

### ✅ **Question 1**
**Insecure Cookies are:**
✔️ **Easily harvested data on customers' machines**
> Insecure cookies are stored on the client-side and can be accessed or stolen if not properly protected using flags like `HttpOnly`, `Secure`, and `SameSite`.

---

### ✅ **Question 2**
**Cookie Data should be treated as:**
✔️ **Untrusted input**
> Cookie data comes from the client. Never trust it blindly — always validate and sanitize it server-side.

---

### ✅ **Question 3**
**Which of these is NOT a security flag for cookies:**
✔️ **SSL**
> `SSL` is **not** a cookie attribute. The correct flag is `Secure`, which ensures the cookie is only sent over HTTPS.  
> `maxAge` is not a _security_ flag, but a session-expiration flag.