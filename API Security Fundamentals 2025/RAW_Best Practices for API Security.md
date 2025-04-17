[Best Practices for API Security](https://university.apisec.ai/products/api-security-fundamentals-2025/categories/2157143833)

## Common Sources of
* Unknown APIs
	* Lack of complete API inventory 
	* Shadow/zombie APIs 
* Vulnerable APIs 
	* Cross-account access
	* Logic flaws 
	* Data exposure
* Weak runtime defenses 
	* Improperly configured WAF 
	* Lack of rate-limiting*
* 3rd party APIs
	* Unknown 3rd party APIs
	* Untested/vulnerable APIs
	* Lack of input validation
* Weak governance
	* Lack of standards
	* Inconsistent processes
	* Patchy documentation
* Poor collaboration
	* Security and Engineering siloed
	* Incomplete/inefficient info sharing

---
Top 10 API Do's and Don'ts
- Don't trust anything (inputs/network)
- Do validate all inputs (not just user)
- Don't reveal useful info in error messages
- Do expect attackers to find your APIs
- Don't have hidden/unadvertised features
- Don't filter data in UI - control at app level
- Do use Gateways to control access, traffic
- Don't forget authentication & authorization
- Do require API documentation
- Do continuously test, pre-production