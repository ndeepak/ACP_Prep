# API Authentication and Authorization
* Basic Authentication
* API Keys
* Certificate based authentication
* Token based authentication
* Token based authentication and authorization

### **Authentication vs. Authorization**
- **Authentication** is the process of identifying who is making a request. This could be a user, a machine, or a system. The goal is to determine the identity of the entity making the request.
	- WHO YOU ARE?
    
- **Authorization** answers the question: What can the authenticated entity do? Once we know who the entity is, we need to decide whether or not they have permission to access the resource they are requesting.
	- WHAT are you allowed to do?

It's critical to first **authenticate** a user or system before moving to **authorization**. Without knowing "who" is making the request, it's impossible to answer "what are they allowed to do?"

---
### **API Authentication Overview**
API authentication is a method used to verify the identity of the entity (user or machine) making requests to an API. There are several methods used to achieve this:
1. **Basic Authentication**:    
    - It involves sending the username and password as part of the HTTP header (in plain text or Base64 encoded).        
    - This method is often insecure unless transmitted over HTTPS, as the credentials are exposed in the request.
    - Hard to convey user identity, only machine identity

2. **API Keys**:    
    - API keys are a unique identifier for an application making requests to an API.        
    - While useful for identifying and throttling usage from an application, API keys don't offer the level of security or flexibility needed for modern applications.     
    - Username and password at once
    - API keys usually convey **machine identity**, not user identity.        

3. **Certificate-based Authentication (Mutual TLS)**:    
    - In **mutual TLS**, both the client and the server authenticate each other via certificates.        
    - This is useful for **machine-to-machine** communication where both parties need to establish trust.        
    - The downside is that it’s complex and computationally expensive.        
    - Conveys machine identities

4. **Token-based Authentication**:    
    - This is the modern approach, especially in scenarios where user or machine identities need to be conveyed in a secure manner.        
    - Tokens (e.g., JWTs) are issued by a trusted third party and are used for authentication and authorization the callers.
    - can expire and have an audience.
    - **Token-based authentication** enables features such as **expiration**, **audience restrictions**, and **scopes**.        
    - The API trusts the issuer of the token
    - Can convey both user and machine identity
    - Tokens can convey more information than caller ID
    - Additional details can be used for authorization
    - A token may be valid, but not "powerful" enough to provide access
    - OAuth use scopes, OpenID Connect adds claims


---
### **OAuth Overview**
OAuth is a framework used for **delegated authorization**. This means that an entity (e.g., a user) can grant access to their resources without revealing their credentials to a third-party service.
#### History of OAuth
* OAuth 1 - IETF Standard 2010
	* Driven by Twitter and Google
	* Relied heavily on signing
	* Did not require HTTPS
	* Hard to implement clients
* OAuth 2.0 IETF Standard late 2012
	* Doesnot rely on signing
	* Requires HTTPS
	* Easy to implement Clients
	* Currently wide adoption
	* OAuth 2.1 underway
#### **OAuth Actors**:
OAuth involves several key participants:
1. **Resource Owner**: The entity (usually a user) that owns the data or resources.    
2. **Client**: The application that wants to access the resource owner's data.    
3. **Authorization Server**: The server that issues tokens after authenticating the user and authorizing the client.    
4. **Resource Server**: The server that hosts the protected resources, and it validates access tokens before serving requests.    

#### **OAuth Interaction Patterns**:
OAuth defines several flows to accommodate different use cases:
1. **Authorization Code Flow**: Typically used by web applications. The client gets an authorization code, which it then exchanges for an access token.    
2. **Implicit Flow**: Used by client-side applications (e.g., JavaScript in the browser). The access token is returned directly without the intermediate authorization code.    
3. **Client Credentials Flow**: Used for machine-to-machine communication, where the client is trusted to authenticate itself using its own credentials.    
4. **Resource Owner Password Credentials Flow**: The client directly collects the user's username and password to obtain a token. This is only used when the client is highly trusted.    

---
### OpenID Connect VS OAuth
* OAuth is a delegation protocol
	* API access is the main goal
* OpenID Connect is an Identity layer atop of OAuth
	* Defines user authentication metadata
	* Can Control authentication
	* Federation

---
##### Summary
* Machine level authentication is different from user level authentication
	* both are often needed
	* can be combined
* OAuth uses token based authentication
	* provides a token based architecture
* OAuth 2.0 requires HTTPS (TLS)

----
### **Tokens and JWTs (JSON Web Tokens)**
Tokens are the core of OAuth 2.0 authentication and authorization. They are cryptographically signed pieces of information that convey various details about the requestor. **JWT** is one of the most widely used token formats.
- **JWT Structure**:    
    1. **Header**: Contains metadata about the token, such as the algorithm used for signing.        
    2. **Payload**: Contains claims, which are statements about the entity (e.g., user information) and additional data.        
    3. **Signature**: A cryptographic signature to ensure the integrity of the token.        
- **JWT Advantages**:    
    - **Stateless**: No need to store the session on the server side.        
    - **Compact**: Easily passed in HTTP headers.        
    - **Self-contained**: Contains all the information needed, such as user identity, in the payload.        
JWTs can be used for both **authentication** (verifying who the user is) and **authorization** (determining what actions the user can perform).
---
### **Scopes and Claims**
- **Scopes**: These define the level of access granted. For example, a scope might specify if the user is allowed to read, write, or modify data in the system. OAuth 2.0 defines **scopes** as a way to limit the access the client has to the resource owner's data.    
- **Claims**: These are pieces of information encoded in the JWT. Claims can contain user identity information (e.g., username, email) or other data like roles, groups, or the permissions granted to the user. Common claims include:    
    - **sub**: Subject (the user’s identifier).        
    - **iat**: Issued at time.        
    - **exp**: Expiration time of the token.        
    - **aud**: Audience (who the token is meant for).        
---
### **Gateways and APIs**
- **API Gateway**: Acts as an entry point for all client requests to APIs. It handles tasks such as routing, load balancing, caching, security (e.g., authentication and authorization), and rate limiting. The API gateway is often where OAuth tokens are verified before requests are passed on to backend services.    
- **APIs**: APIs are the actual endpoints that expose data and services to clients. OAuth is commonly used to secure APIs by requiring clients to authenticate and authorize requests using tokens.
    
---
### Conclusion
This overview touched on various API authentication techniques, the OAuth protocol, its interactions, and how tokens (including JWTs) play a crucial role in both authentication and authorization. OAuth allows for secure API access by delegating user authentication while ensuring that the third-party applications don’t access sensitive credentials. It also offers flexibility with **scopes** and **claims** to manage access controls efficiently.


Question 1
###### Authorization is the process of
Figuring out what the user is allowed to do

Question 2
###### Which of the following statements is incorrect about basic authentication
Basic Authentication can be used to authenticate both the user and the machine at the same time.
