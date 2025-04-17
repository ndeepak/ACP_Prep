### **Question 1: Which of the following statements is true about token-based architectures?**
✅ **It provides fundamentals to build a zero-trust architecture**
- Token-based authentication allows for fine-grained access control, which is a key principle of Zero Trust.    
### **Question 2: Which HTTP request header is used to pass the access token?**
✅ **The Authorization header**
- The `Authorization` header is used to pass access tokens in the format `Authorization: Bearer <token>`.    
### **Question 3: What does the client need to send along with an access token of type Bearer when calling the API?**
✅ **Nothing**
- A Bearer token is self-contained, and the client does not need to send anything additional.    
### **Question 4: Which OAuth flow is most suitable for web applications?**
✅ **Code flow**
- The **Authorization Code Flow** is the best OAuth flow for web applications because it allows the client to securely obtain an access token without exposing the user’s credentials.    
### **Question 5: Who is the only allowed final recipient (audience) of a refresh token?**
✅ **The Authorization Server**
- Refresh tokens are used to obtain new access tokens and should only be sent to the Authorization Server.   

### **Question 6: What is the difference between scopes and claims?**
✅ **Scopes don't have values but claims do**
- Scopes define the level of access granted, while claims contain user-specific values (e.g., roles, permissions).    
### **Question 7: Why do we say that the access token is the identity API for the APIs?**
✅ **The access token contains claims that can be tailored for the API’s identity needs**
- APIs use claims in access tokens to make authorization decisions.   

### **Question 8: What are the two base OAuth endpoints called?**
✅ **Authorization endpoint and token endpoint**
- The **Authorization Endpoint** is used to obtain an authorization code, and the **Token Endpoint** is used to exchange the code for an access token.    

### **Question 9: How does a user authenticate when the client starts a code flow?**
✅ **It is not defined by the OAuth specification**
- OAuth does not dictate authentication methods. It depends on the Identity Provider (IdP).    

### **Question 10: Why are scopes helpful for application (client) level permissions?**
✅ **Because they limit what the client can do, no matter who logs in**
- Scopes restrict the client’s capabilities independently of the user’s identity.