# OWASP API #7 - Server Side Request Forgery
##### [OWASP API Top 10 + Real-World Breaches](https://university.apisec.ai/products/api-security-fundamentals-2025/categories/2157142220)
[[API7 2023 Server Side Request Forgery]]

What is it?
* "Tricking" your API server to go somewhere it shouldn't
* Exploiting URL inputs to make a request to a malicious, 3rd party server


Examples, Risk Exposure
* Creates channel for malicious requests, data access or other fraudulent activity
* Potential for data leaks
* User inputs malicious destinations:
	* Malware site
	* /localhost/etc/passwd


Prevention
* Utilize least privilege model
* Don't trust any inputs without input validation and sanitization
* Validate ALL user-supplied information, including URL parameters
* Simulate SSRF attacks during QA/testing to identify any vulnerabilities


https://dl.acm.org/doi/10.1145/3546068
https://krebsonsecurity.com/2019/08/what-we-can-learn-from-the-capital-one-hack/
https://www.techtarget.com/searchsecurity/news/252467901/Capital-One-hack-highlights-SSRF-concerns-for-AWS#:~:text=The%20Capital%20One%20hack%20has,contributing%20factor%20with%20the%20breach.