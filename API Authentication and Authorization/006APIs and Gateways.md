# APIs and Gateways
##### [APIs and Gateways](https://university.apisec.ai/products/api-authentication/categories/2155385711)
---
### **APIs and API Gateways in OAuth Security**
In this section, we're going to explore how tokens flow from clients to APIs and how API gateways fit into this security model.

---
## **1. Why Use API Gateways?**
API gateways act as an entry point between external clients and internal APIs. They serve multiple purposes:
- **Security:** Provide **Layer 7 (application layer) firewalling** to inspect traffic and allow/block requests.    
- **Traffic Management:** Direct requests to the right API.    
- **Authentication & Authorization:** Validate OAuth tokens before forwarding the request.    
- **Network Protection:** Prevent direct access to APIs from the internet.    
- Visibility of exposed APIs
### **Basic Flow of an API Gateway**
1. The **client** sends a request (e.g., a `GET` request) to the API Gateway.    
2. The **gateway terminates the request**, inspects it, and decides if it should forward it and where. 
3. If approved, the **gateway forwards** the request to the correct API.    
---
## **2. Token Handling in API Gateway**
When an OAuth **access token** is used in an API request, the **gateway** is responsible for validating it. There are two types of tokens:
- **By Value Tokens:** Typically **JSON Web Tokens (JWTs)**, which contain all required information.    
- **By Reference Tokens:** Contain just an identifier that references token details stored in a database.    

For security, reference tokens are preferred **when sending tokens outside of the gateway** to avoid leaking sensitive data.

---

## **3. The Phantom Token Flow**
This pattern improves security when forwarding tokens:
1. **Outside the gateway:** Use **opaque (reference) tokens** to protect sensitive data.    
2. **Inside the gateway:** Convert the reference token into a **JWT (by-value token)** before sending it to APIs which is then forwarded.    
3. This ensures:    
    - **Better security** (opaque token outside, readable JWT inside).        
    - **Stronger audit trails** (tracking user identity across services) all the way to final trail.        
    - **Zero-trust security** (tokens should always be used instead of raw JSON messages).        
---
### All APIs should depend on JWTs
* Accept no request without a JWT
* Verify issuer, audience, validity, scopes and claims
* Uniform security model internally
* Easy re-use of validation logic
* Zero-trust enabled
* Identity data is kept and can be trusted at API level
---
### **Token Introspection**
When a gateway receives a **reference token**, it must query the **Authorization Server** (AS) to validate it. This process is called **introspection**.  
The AS responds with:
- If the token is valid, **JSON metadata** about the token.    
- If invalid, `{ "active": false }`.    
---
## **4. Token Exchange Strategies or API to API Calls** 
When one API calls another API, it must pass the token forward. There are **three main ways** to do this:
### **A. Token Exchange (On-Demand) Powerful options**
* Use token exchange to get a to get another token
- API calls the **Authorization Server** to exchange the original token for a new one with **reduced scope**.    
- Gateway is the client itself in this.
- The new token has fewer permissions, minimizing security risks.    
- Best used when the second API does not need **all permissions** of the first token.    

### **B. Token Embed (Pre-Provisioned)**
* Put more tokens inside the first token*
- The **original token contains an embedded token** (inside a claim) for the next API.    
- The API extracts and forwards it.    
- More efficient than token exchange but adds extra data to every token.    
- When it is known to happen on every request

### **C. Token Sharing**
* Use the same token
- The same token is forwarded directly to the next API.    
- Less secure because the second API can **reuse the token** maliciously.    
- Works well when both APIs are in the **same security domain**.    
- When the APIs are in the same security domain

---
## **API Authorization Overview**

API authorization ensures that only authenticated and authorized users or services can access specific API resources and perform allowed actions. It involves multiple levels of authorization to enforce security and access control at various stages of API interaction.
### **Coarse-Grained Authorization**
Coarse-grained authorization is a high-level access control mechanism that determines whether a user or service has permission to access an API endpoint based on broad criteria. It is typically enforced at the API gateway level or through centralized access control mechanisms.
#### **1. Invoice Type-Based Authorization**
- Access to different types of invoices (e.g., purchase invoices, sales invoices, credit notes) is controlled based on user roles or predefined policies.    
- Example: A finance department employee may access all invoice types, while a sales representative can only view sales invoices.    

#### **2. Scope Identification**
- OAuth 2.0 and OpenID Connect (OIDC) use scopes to define the level of access granted to a token holder.    
- Example:    
    - `invoice.read`: Allows reading invoice data.        
    - `invoice.write`: Grants permission to modify invoice data.        
    - `invoice.admin`: Provides full administrative control over invoices.        
- The API gateway checks the scope in the access token before forwarding the request to the API.

### **Fine-Grained Authorization**
Fine-grained authorization provides more detailed access control based on contextual information, attributes, and policies. It is enforced at the API level, often leveraging external policy engines.
#### **1. Checking Claims**
- Claims are key-value pairs within a token (e.g., JWT) that provide user or service identity details.
- Examples of claims used for fine-grained authorization:    
    - `user_id`: The unique identifier of the user making the request.        
    - `role`: The role assigned to the user (e.g., `finance_manager`, `sales_rep`).        
    - `region`: The geographical location of the user (e.g., `US`, `EU`).        
- The API extracts claims from the token and evaluates them against authorization rules.

#### **2. Invoice Read Permission**
- The API enforces access control at the resource level.    
- Example of a policy:    
    - A user with `invoice_read` permission can access only invoices assigned to their department or within their jurisdiction.        
    - A manager with `invoice_admin` permission can access all invoices.        

#### **3. Policy Decision Point (PDP)**
- The API can delegate fine-grained authorization decisions to a policy engine.    
- **Common policy decision points (PDPs):**    
    - **OPA (Open Policy Agent)**: A flexible policy engine that enforces fine-grained access control based on policies written in Rego.        
    - **Axiomatics**: An Attribute-Based Access Control (ABAC) solution that evaluates policies based on dynamic attributes.        

### **Summary and Best Practices**
1. **Gateways should enforce coarse-grained authorization**    
    - The API gateway should validate tokens and check high-level permissions (e.g., scopes).       
2. **The API should handle fine-grained authorization**    
    - APIs should verify claims and apply attribute-based or role-based access control at a granular level.
        
3. **Use the phantom token flow to keep PII inside the firewall**    
    - Instead of exposing Personally Identifiable Information (PII) in access tokens, use reference tokens (phantom tokens) that are resolved within a secure boundary.
        
4. **Tokens can be shared, exchanged, or embedded**    
    - Depending on the security model, tokens can be passed between services, converted into different formats, or embedded in requests.
        
5. **Map token contents to the domain they are targeting**    
    - Ensure that token attributes align with the API’s authorization requirements for better security and efficiency.

---
## **5. Summary & Best Practices**
- **Always use API gateways** for security and traffic management.    
- **Use opaque tokens externally** and JWTs internally (Phantom Token Flow).    
- **Validate tokens at the gateway** before forwarding.    
- **Use token exchange** when reducing permissions for security.    
- **Embed tokens for efficiency** if the second API is always required.    
- **Avoid direct token sharing** across unrelated APIs for security reasons.    

---
Question 1
###### Which is the standard flow to use in a gateway to know what's inside an opaque token
Introspection

Question 2
###### The phantom token flow defines a pattern to:
Hide sensitive data on the Internet but expose it internal

Question 3
###### There are three methods to use tokens for API to API calls
Exchange, embed, share

Question 4
###### What is good practice for the gateway when it comes to authorization
To validate the token and inspect the scopes to perform a coarse grained authorization decision

---
