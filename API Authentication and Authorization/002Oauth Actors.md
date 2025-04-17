## OAuth 2.0: Actors and Problem Statement

### **The Problem That OAuth Solves**
Before OAuth, third-party applications that needed access to a user's account had to ask for the user's username and password. This was problematic because:
1. **Security Risk** – Sharing credentials with third-party applications meant they could store or misuse them.    
2. **No Granular Access Control** – The third party got full access, even if only limited access was required.    
3. **Credential Management Issues** – If the user changed their password, all third-party applications would break.    

OAuth was designed to solve this problem by allowing users to **delegate access** to third-party applications **without sharing credentials**.

---
### **OAuth 2.0 Actors**
OAuth 2.0 has four key actors:
1. **Resource Owner (User)**   (RO) 
    - The RO has content at RS
    - The entity that owns the protected resource.        
    - Example: A user who owns their Gmail account.        
2. **Client (Third-party Application)**    
    - The RO wants to use 3rd party app to reach content
    - The application requesting access to the user's resource.        
    - Example: A calendar app that wants to read the user's Gmail events.        
3. **Authorization Server**    (AS)
    - The system that authenticates the resource owner and issues access tokens.        
    - Example: Google's OAuth authorization server.        
4. **Resource Server**    (RS)
    - The API that holds the user's data and validates access tokens.        
    - Example: Gmail API, which provides access to the user's emails.        

---
### **Authorization vs Delegation**
OAuth is **not** an authorization protocol (or Open Authorization) but a **delegation protocol**. The difference is:
1. **Delegation** – The user allows an application to act on their behalf.    
    - Example: A boss signs a letter authorizing an employee to withdraw money.        
2. **Authorization** – The system decides whether access should be granted at the time of request.  
    - Example: The bank may still deny the transaction if its policies don’t allow delegation.       

🔹 **Key Point:** Just because a client gets an OAuth token doesn’t mean it will be granted access. The resource server can still apply additional rules.

Summary:
* OAuth delegates access to applications on a user's behalf
* The client is the application
* The Resource Server is the API
* Delegation != Authorization
	* The API may still deny the request

---
### **Question 1**
**What was the main problem that led to the inception of OAuth?**  
✅ **Companies wanted to expose APIs that used authentication but didn't want 3rd parties to see the user's credentials**
🔹 **Explanation:** OAuth was created to allow third-party applications to access user data **without sharing user credentials**. This prevents security risks and gives users control over what data is shared.
### **Question 2**
**The Actors of OAuth 2.0 are:**  
✅ **The client, the resource server, the authorization server, and the resource owner**
🔹 **Explanation:** OAuth 2.0 involves four key actors:
1. **Resource Owner (User)** – Owns the data.    
2. **Client (Third-party App)** – Requests access.    
3. **Authorization Server** – Issues tokens after verifying the user.    
4. **Resource Server** – Holds the protected data and validates access
### **Question 3 (Revised Answer)**
**Who delegates to whom in OAuth?**
✅ **The authorization server delegates to the client**
### **Explanation:**
- **The user (resource owner)** grants permission to access their data.    
- **The authorization server** then **delegates access** by issuing an **access token** to the **client**.    
- The **client** then uses this token to access the **resource server** on behalf of the user.    

So, in OAuth, **delegation flows from the authorization server to the client** in the form of an **access token**.

---