# OWASP API #3 - Broken Object Property Level Authorization
##### [OWASP API Top 10 + Real-World Breaches](https://university.apisec.ai/products/api-security-fundamentals-2025/categories/2157142220)
[[API3 2023 Broken Object Property Level Authorization BOPLA]]

#### What is it?
* Exploit of endpoints by reading and/or modifying values of objects
* Ability to update object elements ("mass assignment")
* Revealing unnecessary sensitive data ("excessive data exposure")
Examples, Risk Exposure
* User is able to set "account-type=premium"
* API returns excessive, unnecessary details
* Exposing sensitive user data
* Data theft


Prevention
* Ensure user can only access legitimate, permitted fields
* Return only minimum amount of data required for the use case
* Define data requirements in API specifications
* Test to validate policy compliance
* Implement proper controls enforced to prevent mass assignment exploits
* Test controls to identify logic flaws

https://www.wired.com/story/i-scraped-millions-of-venmo-payments-your-data-is-at-risk/
https://techcrunch.com/2019/06/16/millions-venmo-transactions-scraped/