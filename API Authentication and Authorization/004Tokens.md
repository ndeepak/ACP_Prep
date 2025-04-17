# Tokens
##### [Tokens](https://university.apisec.ai/products/api-authentication/categories/2155385519)
---
# Understanding Tokens in Authentication and Authorization
## 1. Introduction to Tokens
Tokens are a fundamental aspect of authentication and authorization in security frameworks. They are issued during interaction patterns and serve various purposes, including access control and identity verification. Tokens can be categorized based on their format, purpose, and type.

## 2. Token Formats
Tokens can be encoded in two primary ways:
### 2.1 By Reference Tokens
- These tokens are opaque to the holder, meaning they cannot be read or decoded.
- They are essentially a random string that serves as a reference to a database entry.    
- To access the token's details, the holder must query the authorization server.    
- This format is privacy-preserving and secure for internet-based communications.    

### 2.2 By Value Tokens
- These tokens contain all the necessary details within them.    
- They can be validated by the receiver without additional calls to the authorization server.    
- By-value tokens can be signed, encrypted, or both.    
- Common formats include:    
    - JSON Web Tokens (JWTs)        
    - SAML Assertions        
    - CWTs (CBOR Web Tokens)        
## 3. Token Purpose
Tokens serve different purposes based on their use case. The main types of tokens are:
### 3.1 Access Tokens
- Intended for the resource server (RO).    
- Used to authenticate requests and grant access to protected resources.    
### 3.2 Refresh Tokens
- Used to obtain new access tokens when the previous one expires.    
- Should be sent only to the authorization server (AS).    
- Must be kept confidential and never shared.    
### 3.3 ID Tokens (OpenID Connect)
- Provided after the authentication process.    
- Meant for the client and should not be transmitted elsewhere.    

---
##### Using an Access Token
* Send in the authorization header
* user the keyword bearer
* Make no assumptions about the structure or format of the token
---
## 4. Token Types
Tokens are classified based on how they are transmitted and used:
### 4.1 Bearer Tokens
- Function like cash; whoever holds the token can use it i.e. can by used by anyone.    
- No sender verification is required.    
- Must be transmitted securely over TLS/HTTPS.    
- Should not be logged or stored in a browser.
- Common tokens
- Cookie are also bearer tokens

### 4.2 Proof of Possession (POP) or Holder of Key Tokens
- Similar to a credit card, requiring additional proof (e.g., a PIN or private key).    
- Sender must prove ownership of the private key.    
- Cannot be send by other parties.
- Prevents token misuse if intercepted.    
- Sender constrained tokens
- Examples:    
    - Demonstration of Proof of Possession (DPoP)    
	    - Send in the authorization header
	    - use the keyword DPoP
	    - Must send additional token to prove ownership
    - Mutual TLS (mTLS)        
---
## 5. JSON Web Tokens (JWTs)
JWTs are widely used due to their ease of use and structured format. 
JWT is a format. It can be used for many purposes:
* ID tokens are always JWTs
* Access tokens can be JWTs
* Refresh Token are "never"  JWTs
Most Often signed (JWS). and can be encrypted (JWE).
They consist of three parts:
### 5.1 JWT Structure
![[Pasted image 20250403110456.png]]
https://jwt.io
https://research.securitum.com/jwt-json-web-token-security/
1. **Header**: Contains metadata such as:    
    - Key ID (KID) referencing the signing key.        
    - Algorithm (ALG) used for signing (e.g., RS256).        
2. **Payload**: Contains claims about the user, client, and token details, including:    
    - Issuer (ISS): The entity that issued the token.        
    - Subject (SUB): The authenticated user.        
    - Audience (AUD): The intended recipient.        
    - Expiry (EXP) and Not Before (NBF) timestamps.        
    - Unique Identifier (JTI): Ensures token uniqueness.        
3. **Signature**: Ensures the token's integrity and authenticity.    
https://oauth.tools/
### 5.2 Signed-JWS vs. Encrypted-JWE
- **JSON Web Signatures (JWS)**: Ensures authenticity using asymmetric keys.    
	- Proves who issued the token
	- The prominent way for JWTs
	- Asymmetric signatures
	- Always whitelist algorithms
	- Don't only rely on signature, verify contents as well
		- Audience
		- Issuers
		- Expiration
- **JSON Web Encryption (JWE)**: Encrypts the token for confidentiality.    
	- Keeps data confidential
	- Used in OpenID Connect
	- ID Tokens
	- User info responses
	- Not practical for access tokens
	- Opaque tokens are preferred to keep confidentiality
- Ensure only whitelisted algorithms are allowed to avoid vulnerabilities (e.g., "none" algorithm bypassing validation).    

## 6. Secure Token Handling
- Always send access tokens in the authorization header (e.g., `Authorization: Bearer <token>`).    
- Never assume a token's structure; treat it as an opaque string.    
- Always validate the token's expiration, issuer, and audience before using it.    
- Use encrypted tokens when confidentiality is required.    
- Secure storage and transmission of tokens are critical for security.    

----
#### JWTs and Protocols
* A JWT is not a protocol
* They can be used in different ways depending on protocols
* They should not be used against the protocols' intention
Example
* Access tokens are for the API
* They are issued to the client
* The client should not decode the access token
---
## 7. Conclusion
Tokens play a vital role in authentication and authorization. Understanding their format, purpose, and type helps in designing secure and efficient authentication mechanisms. Proper token handling and security best practices ensure the integrity and confidentiality of user sessions and access control systems
* Tokens have a purpose, a format and a type
	* Purpose is the intended use
	* Format is the encoding
	* Type is the way it can be sent
* By value and by reference
	* JWT is by value
* Using JWTs is not enough
	* Must follow a protocol
----
QUIZ
Question 1
###### Which are the three axes used to define a token
Format, purpose and type

Question 2
###### Which of the following statements is NOT true about JWTs
All access tokens are JWTs

Question 3
###### What is the key benefit of using PoP tokens as access tokens
They can only be sent by the client they were issued to

Question 4
###### Access tokens have an audience, what does that mean:
They should only be accepted by the entities listed in the audience claim

---