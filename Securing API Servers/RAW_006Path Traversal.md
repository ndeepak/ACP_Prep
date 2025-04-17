# Path Traversal

### Path traversal = allowing access to unintended paths on a server
* Directory Traversal
* Direct file reference either inside or outside
* Server Configurations
* Defensive coding
* Spec

Example Traversal Vulnerability
Malicious Cookie | Dynamic Path Source codes

### Expect Encoding
%2e%2e%2e%2e%2e%2f =../../../
alike
Don't anticipate and filter. Specifically define what's allowed
Directory Traversal tools

### The problem
1. Input data validation
2. Server config (Directory listings, and allowed include paths)
3. Dynamic paths in source code
4. Loose spec "String" allows attacks

### Solution
Security Vulnerabilities, CVEs (Directory traversal)
https://www.cvedetails.com/vulnerability-list/opdirt-1/vulnerabilities.html
1. Scrub input data
	1. Specify what's allowed. Enum/Array/List?
	2. Don't try filtering what's bad
2. Disable server directory listings
3. Don't store anything sensitve at web root
4. Put the web root on a separate drive than system
5. When in doubt, error


### Summary
1. Path traversal vulnerabilities can be severe
	1. /etc/passwd
	2. .rsa, .git
	3. c:/inetpub/logs/logfiles
2. They share common solutions as other issues
3. Test + Static Analysis

