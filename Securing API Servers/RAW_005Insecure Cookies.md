# Insecure Cookies
Protect customer data from harvesting
### Insecure Cookies= Cookies stored without restrictive security settings
* Secure Cookies Option
* HTTP Only
* SameSite, Domains, Subdomains

### Understanding Cookies
what are they?
what they contains?
Booleans value, Base64, Integer Value, Salts, Some values
Delimiters of cookie value
Session numbers
Timestamps
Paths
Set-Cookie Headers

New Cookie --< Cookie Data

### Cookie Decoding
* Find interesting keys/fields
* Sort data types
	* Unique ID string
	* Numeric ID
	* Booleans
	* Encoded data
* Decoding Data
	* Delimiters
	* Base64 decode and similar
### The Problem
* Cookie forging/Fuzzing (Trusting cookie data)
* Data harvesting, different site (httponly + no Domains)
* Data harvesting, through XSS (httponly)
* Data harvesting in transit (Secure flag)

### The Solution
* Treat cookies as untrusted user data
* Be restrictive on what data is stored in cookies
* Analyze your cookies from an offensive mindset