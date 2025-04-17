# OWASP API #4 - Unrestricted Resource Consumption
##### [OWASP API Top 10 + Real-World Breaches](https://university.apisec.ai/products/api-security-fundamentals-2025/categories/2157142220)
[[API4 2023 Unrestricted Resource Consumption Unrestricted Resource Consumption]]

What is it?
* Formerly "Lack of Resources and Rate Limiting"
* Abuse of APIs due to high volumes of API calls, large requests, etc.

Examples, Risk Exposure
* Missing/inadequate rate controls
* Mass data harvesting
* Execution timeouts
* Max memory, number of files, upload size
* Excessive operations in single request
* Excessive records returned in a request
* Denial of Service
* Performance impact

Prevention
* Implement traffic controls
* Test effectiveness of controls
* Note: rate limiting is a velocity control, not a volume control
	* Attackers are clever and determined
	* Will evade detection by limiting requests velocity
	* Breaches can take months

https://www.rescana.com/post/trello-api-security-breach-15-million-email-addresses-leaked-in-massive-data-exposure