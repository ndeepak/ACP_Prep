# Scopes and Claims
##### [Scopes and Claims](https://university.apisec.ai/products/api-authentication/categories/2155385653)
---
### **Understanding Tokens, Scopes, and Claims**
Tokens are a fundamental part of modern authentication and authorization systems. They are used to grant access to resources in a secure and scalable way. Let's dive into the key concepts you need to know:

---
### **1. What Are Scopes?**
👉 **Scopes define what an application can access.**  
They act like permission keys that determine which parts of a system the client can interact with.
✅ **Key Characteristics of Scopes:**
- **They are just keys, not values.** Example: `read:invoices`, `update:profile`, `write:payments`.  
- **Pre-defined and approved.** The authorization server defines which scopes can be requested.    
- **Application-level permissions, not user-level.** Scopes define what a client (app) can do, not what a specific user can do.    
- **Can be requested by a client but issued at the discretion of the authorization server.**    

📌 **Example of How Scopes Work:**
- Suppose there’s an app that lets users view and update invoices.    
- A **consumer** (end-user) app may request:    
    `Scope: user_invoice_read`    
    This means the app can read invoices but **not** update them.    
- A **finance department** app may request:    
    `Scope: user_invoice_read user_invoice_update`
    This means the app can both **read and update** invoices.    

💡 **Scopes act as a security boundary. Even if a super admin logs into an app, they can only perform actions allowed by the app's scope.**

#### User Consent
* Scopes can involve the user
* The user can optionally consent to giving the application/client access
* Sometimes useful in 3rd party client integrations
---
### **2. What Are Claims?**
👉 **Claims are key-value pairs that contain information about a user.**  
* They help with fine-grained access control.
* Inside the token, Asserted by the issuer, claim truth about the subject
* Can be used for fine grained access control
* Example: 
	* subject=jacob
		* aget=42
		* profession=identity geek
		* workplace=Curity
		* subscription_level=gold

✅ **Key Characteristics of Claims:**
- **They are inside the token (like a JWT).**    
- **Issued by the authorization server and trusted.**    
- **Define user-specific information** like user ID, role, or subscription level.    
- **Can be used for more granular access control.**    

📌 **Example of Claims in a JWT Token:**
```json
{
  "sub": "jacob123",
  "email": "jacob@example.com",
  "subscription_level": "gold",
  "age": 42
}
```

Here:
- `"sub": "jacob123"` is the unique user identifier.    
- `"email": "jacob@example.com"` is a claim about the user's email.    
- `"subscription_level": "gold"` may determine video streaming quality or premium access.    
- `"age": 42` might be used for age-restricted content.    
🔑 **Claims can help APIs make decisions based on user identity.**

#### The Access token claims
* can be the API for your API
* Single source of truth for identity data
* Avoid external calls from the API
* Design a common identity API for your APIs
* Can be different depending on the scopes in the token
---
### **3. How Scopes and Claims Work Together**
Think of scopes as a **door key** and claims as **rules inside the building.**
- **Scopes decide if an application (client) is allowed to enter.**    
- **Claims decide what a specific user is allowed to do once inside.**    

📌 **Example Scenario – Accessing Invoices:**  
Imagine a user (Jacob) wants to access invoice `123`.
1. **The client app requests a token with scope:**    
    `user_invoice_read`
    
2. **The authorization server issues a token with claims:**    
```json
{
  "sub": "jacob123",
  "scope": "user_invoice_read",
  "subscriber_id": "ABC123",
  "role": "customer"
}
```
    
3. **The API server checks:** ✅ Does the token have the `user_invoice_read` scope? (Yes, access granted)  
    ✅ Is `subscriber_id` **ABC123**, matching the invoice owner? (Yes, return invoice)    

💡 **Scopes allow access, but claims decide what data is returned.**

---
### **4. Summary of Scopes vs. Claims**

|Feature|Scopes|Claims|
|---|---|---|
|Purpose|Defines application-level permissions|Defines user-specific identity data|
|Format|List of keys (`read:profile`)|Key-value pairs (`"email": "xyz@example.com"`)|
|Who Uses Them?|APIs check scopes for access control|APIs use claims for fine-grained decisions|
|Example Use|Can the app **read invoices**?|Is this **invoice really mine**?|
|Coarse/Fine Control|Coarse-grained|Fine-grained|

---
### **5. Audience in Tokens**
👉 **Access tokens have an audience (aud claim).**  
This ensures they are only used by the right API.
✅ **Audience (`aud`) claim meaning:**
- **"They should only be accepted by the entities listed in the audience claim."**    
- If a token's `aud` is `"api.example.com"`, then only that API should accept the token.    

📌 **Example JWT payload with `aud`:**
```json
{
  "sub": "jacob123",
  "scope": "user_invoice_read",
  "aud": "api.example.com"
}
```
- Only `api.example.com` should accept this token.    
- If `api.other.com` tries to use it, the request should be rejected.    

---
### **6. PoP Tokens (Proof-of-Possession Tokens)**
👉 **PoP tokens prevent token theft attacks.**  
They ensure only the original client that got the token can use it.
✅ **Key Benefits:**
- **They bind the token to a specific client.**    
- **Even if stolen, they cannot be used by another party.**    
- **Enhances security for APIs.**    

📌 **Why are PoP tokens better than regular tokens?**
- Normal access tokens (like JWTs) can be stolen and used by an attacker.    
- PoP tokens require **cryptographic proof** (e.g., a secret key only the client knows).    
💡 **Think of PoP tokens as a key that only fits one lock, even if someone steals a copy.**

---
### **Final Takeaways**
1. **Tokens grant access securely** – They act like digital keys for APIs.    
2. **Scopes control what an app can do** – They define broad permissions.    
3. **Claims control what a user can do** – They provide user-specific details.    
4. **Audience (`aud`) claims ensure tokens are used by the correct API.**    
5. **PoP tokens prevent stolen tokens from being used by attackers.**    
----
Summary
* Scopes define the "scope of access* for the token
	* Application level permissions
	* Not user level
* Claims provide user details
	* Identity data - trusted - about the user
* Scopes are coarse grained
* Claims are fine grained
---
##### Scopes and Claims Quiz
Question 1
###### Which of the following statements is NOT true about scopes
The scope carries values that are true about the user


Question 2
###### Why are claims useful to pass in access tokens
They enable the API to make fine grained access control decisions related to the user

----