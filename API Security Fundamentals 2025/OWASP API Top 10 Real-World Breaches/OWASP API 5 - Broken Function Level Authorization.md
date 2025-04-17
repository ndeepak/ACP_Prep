# OWASP API #5 - Broken Function Level Authorization
##### [OWASP API Top 10 + Real-World Breaches](https://university.apisec.ai/products/api-security-fundamentals-2025/categories/2157142220)
[[API5 2023 Broken Function Level Authorization]]

What is it?
* Abuse of API functionality to improperly modify objects (create, update, delete)
* Often involves replacing passive methods (GET) with active (PUT, DELETE)

Examples, Risk exposure
* may be used to escalate privilege
* Modify parameters, e.g. "user-type=premium"
* Can be exploited to modify account details
* Delete an invoice
* Set account balance = $0

Prevention
* Identify and prioritize functions that expose high sensitivity capability
* Develop controls to limit access
* Implement continous release testing to ensure proper behavior
* Review RBAC permissions across all user types and detect drift