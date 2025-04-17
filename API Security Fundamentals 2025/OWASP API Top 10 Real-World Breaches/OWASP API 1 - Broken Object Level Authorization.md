# OWASP API #1 - [[API1 2023 Broken Object Level Authorization BOLA]]Broken Object Level Authorization
##### [OWASP API Top 10 + Real-World Breaches](https://university.apisec.ai/products/api-security-fundamentals-2025/categories/2157142220)

### What is it?
* Broken Authorization refers to flaws in logic/rules governing access
* Most common and damaging API vulnerability
* Very difficult to detect in runtime
* Critical to test for BOLA in pre-production

#### Examples, Risk Exposure
* Significant risk of data loss
* Example: can UserA access UserB's data?
* Fraudulent transactions
### Prevention
* Discuss authorization rules during API design phase
* Review business requirements and define data access policies
* Enforce authorization controls at application logic layer
* Implement automated, pre-production testing to find BOLA flaws



https://techcrunch.com/2021/05/05/peloton-bug-account-data-leak/