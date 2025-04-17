# OWASP API #8 - Security Misconfiguration
##### [OWASP API Top 10 + Real-World Breaches](https://university.apisec.ai/products/api-security-fundamentals-2025/categories/2157142220)
[[API8 2023 Security Misconfiguration]]

What is it?
* Broad category encompasses lack of hardening to unnecessary services 
* Use of bots to scan, detect and exploit misconfigurations 

Examples, Risk Exposure 
* Lack of security hardening 
* Missing security patches 
* Unnecessary features enabled 
* Missing TLS 
* Improperly configured permissions 
* Missing headers: Rate Limit, HSTS, CORS policy missing/improperly set 
* Verbose, revealing error messages 
* Misconfigurations can expose sensitive user data 
* Potential for full server compromise

Prevention
* Implement hardening procedures
* Enforce proper headers and policies: CORS, HSTS, Rate Limit
* Ensure error messages are helpful, but not revealing
* Prevent path traversal, server information leakage
* Routinely review configurations
* Test configuration to ensure proper settings; discover drift
* Recommendation: review Securing API Servers course [[000Introduction]]


https://krebsonsecurity.com/2021/04/experian-api-exposed-credit-scores-of-most-americans/
https://www.cyberdefensemagazine.com/experian-api-exposed/