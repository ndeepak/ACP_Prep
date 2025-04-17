# OWASP API #9 - Improper Inventory Management
##### [OWASP API Top 10 + Real-World Breaches](https://university.apisec.ai/products/api-security-fundamentals-2025/categories/2157142220)
[[API9 2023 Improper Inventory Management]]
What is it?
* Lack of awareness of all APIs
* Improper version control

Examples, Risk Exposure
* Zombie, shadow, rogue APIs
* Old versions of APIs, unpatched endpoints
* Data/account theft via unretired, unsupported APIs
* Endpoints with weaker security
* Outdated documentation
* Unnecessarily exposed endpoints


Prevention
* Define common, standard processes for API development 
* Create a complete inventory of APIs 
	* Traffic-based discovery 
	* Code-based discovery 
	* App crawling discovery 
	* Dictionary discovery 
	* Go talk to Engineering discovery 
* Identify internally developed APIs, as well as 3rd party APIs 
* Deploy/manage all APIs in Gateway 
* Define versioning rules and retirement 
* Make sure all parties upgrade to latest version 
* Periodically audit 3rd party access


https://www.upguard.com/blog/how-did-the-optus-data-breach-happen
https://www.slatergordon.com.au/class-actions/current-class-actions/optus-data-breach
https://www.qld.gov.au/community/your-home-community/cyber-security/cyber-security-for-queenslanders/case-studies/optus-data-breach#:~:text=In%20September%202022%2C%20a%20cyber,phone%20numbers%2C%20and%20email%20addresses.