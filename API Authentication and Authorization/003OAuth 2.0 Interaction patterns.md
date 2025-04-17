# OAuth 2.0 Interaction patterns
##### [OAuth 2.0 Interaction patterns](https://university.apisec.ai/products/api-authentication/categories/2155375676)
---
## 🔹 **What is OAuth 2.0?**
OAuth 2.0 is an **authorization framework** that allows applications to securely **access resources on behalf of a user** without exposing their credentials (username/password).
✅ **Key Actors in OAuth 2.0**
1. **Resource Owner** → The user who owns the data.    
2. **Client** → The application that needs access to the user's data.    
3. **Authorization Server** → The server that issues tokens after verifying the user.    
4. **Resource Server** → The API that holds the user's protected resources.

---
## 🔹 **OAuth Flows (Interaction Patterns)**
OAuth defines different **flows (also called grants)** depending on the type of client application.
### **1️⃣ Authorization Code Flow (For Web Apps & Server-Side Apps)**
✔️ **Use case**: Best for web applications (with back-end servers).  
✔️ **Security**: Highly secure, requires a server for storing client secrets.  
✔️ **How it works**:
- Uses a **front-end (browser) redirect** to obtain an **authorization code**, then exchanges it for an **access token** on the back-end.
### **🔹 Step-by-Step Example**
📌 **Scenario**: A web app (example.com) wants to access a user's GitHub repositories.
1️⃣ **User clicks "Login with GitHub"**
- The user is redirected to GitHub's **authorization endpoint**:
```ruby
GET https://github.com/login/oauth/authorize
?client_id=YOUR_CLIENT_ID
&redirect_uri=https://example.com/callback
&response_type=code
&scope=repo
```
2️⃣ **User logs in and approves the request**
- GitHub **redirects the user back** to the web app's callback URL with an **authorization code**:    
    `https://example.com/callback?code=AUTHORIZATION_CODE`
3️⃣ **Web app exchanges code for an access token**
- The web app's backend makes a **POST request** to GitHub's **token endpoint**:
```bash
curl -X POST https://github.com/login/oauth/access_token \
    -d "client_id=YOUR_CLIENT_ID" \
    -d "client_secret=YOUR_CLIENT_SECRET" \
    -d "code=AUTHORIZATION_CODE" \
    -d "redirect_uri=https://example.com/callback"
```
    

4️⃣ **GitHub responds with an access token**
```json
{
  "access_token": "your_access_token",
  "token_type": "bearer",
  "scope": "repo"
}
```

5️⃣ **Web app uses the token to access APIs**
- Now, the app can **call GitHub APIs**:
    `curl -H "Authorization: Bearer your_access_token" https://api.github.com/user/repos`
    

📌 **Why use Authorization Code Flow?** ✅ Secure – Tokens are exchanged on the back-end (not in the browser).  
✅ Protects client secrets.  
✅ Uses **PKCE (Proof Key for Code Exchange)** to prevent attacks.

---
### **2️⃣ Implicit Flow (For SPA, now deprecated)**
❌ **Not recommended anymore due to security risks**
- Tokens are returned **directly in the browser** (risk of exposure).    
- Now replaced by **Authorization Code Flow + PKCE**.
---
### **3️⃣ Client Credentials Flow (For Machine-to-Machine APIs)**
✔️ **Use case**: When an application needs to access an API **without user involvement** (e.g., backend jobs, cron jobs).  
✔️ **Security**: Uses **client authentication** (no user login).  
✔️ **How it works**: The client authenticates with the authorization server to get a token.

### **🔹 Step-by-Step Example**
📌 **Scenario**: A microservice needs to access another API without a user.
1️⃣ **Client requests a token from the token endpoint**
```bash
curl -X POST https://auth.example.com/oauth/token \
    -d "grant_type=client_credentials" \
    -d "client_id=YOUR_CLIENT_ID" \
    -d "client_secret=YOUR_CLIENT_SECRET"
```

2️⃣ **Authorization server responds with an access token**
```json
{
  "access_token": "your_access_token",
  "token_type": "bearer",
  "expires_in": 3600,
  "scope": "read:data"
}
```

3️⃣ **Client uses the token to access the API**
`curl -H "Authorization: Bearer your_access_token" https://api.example.com/data`

📌 **Why use Client Credentials Flow?** ✅ Ideal for **backend services** that don't involve users.  
✅ No need for login UI.

---
### **4️⃣ Refresh Token Flow (For Long-Lived Sessions)**
✔️ **Use case**: When access tokens expire, the client uses a refresh token to get a new one **without user login**.  
✔️ **Security**: **Refresh tokens should be stored securely** (e.g., in a database).

### **🔹 Step-by-Step Example**
📌 **Scenario**: A user is logged into a mobile app. The app's access token expires every 5 minutes, but it has a refresh token to renew access.

1️⃣ **Client requests a new token using refresh token**
```bash
curl -X POST https://auth.example.com/oauth/token \
    -d "grant_type=refresh_token" \
    -d "client_id=YOUR_CLIENT_ID" \
    -d "client_secret=YOUR_CLIENT_SECRET" \
    -d "refresh_token=YOUR_REFRESH_TOKEN"
```

2️⃣ **Authorization server responds with a new access token**
```json
{
  "access_token": "new_access_token",
  "expires_in": 300,
  "refresh_token": "new_refresh_token"
}
```

📌 **Why use Refresh Token Flow?** ✅ Prevents users from re-authenticating frequently.  
✅ Reduces login friction in mobile and web apps.

---
## 🔹 **Choosing the Right OAuth Flow**

| **Flow**                  | **Use Case**                      | **Security Level**             |
| ------------------------- | --------------------------------- | ------------------------------ |
| **Authorization Code**    | Web apps, back-end authentication | 🔒🔒🔒 (Most secure)           |
| **Client Credentials**    | Machine-to-machine API calls      | 🔒🔒 (No user needed)          |
| **Refresh Token**         | Long-lived sessions               | 🔒🔒 (Requires secure storage) |
| **Implicit (Deprecated)** | Single-page apps (SPA)            | ❌ (Insecure, use PKCE)         |

---
## 🔹 **Conclusion**
✅ OAuth 2.0 provides **different flows** depending on the application type.  
* OAuth flows are client interaction patterns
* The most common one is the authorization code flow
* Select flow based on application type
* Always strive to use the highest security flow
✅ **Authorization Code Flow** is the most secure for **user authentication**.  
✅ **Client Credentials Flow** is great for **server-to-server communication**.  
✅ **Refresh Tokens** keep sessions active without re-login.

---

OAuth 2 quiz:
**Question 1:**  
✅ **After the user has been redirected to the authorization server**
- The user authentication happens after they are redirected to the authorization server, where they log in.    

**Question 2:**  
✅ **It can be used to refresh the access token**
- This is **NOT** true. The authorization code is only used to obtain an access token, not to refresh it. A **refresh token** is used for that purpose.

**Question 3:**  
✅ **Obtain new access tokens**
- The refresh token is used to get a new access token **without requiring the user to log in again**.

**Question 4:**  
✅ **Only an access token**
- In the **Client Credentials flow**, there is no user authentication, so only an access token is issued—**not** an authorization code or refresh token.