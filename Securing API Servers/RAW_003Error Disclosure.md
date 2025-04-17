# Error Disclosure
Error Handling + Defensive Coding

### Error Disclosure = revealing technology and code in an error
* Error out is necessary, Why? for systems engineers, hackers, developers, etc.
* Intentional error handling is good
* Developers and Customers are separate error message audiences

How attackers are find email addresses of users, using email verification errors, how and why.

### How does this happen?
in python, try and catch error with example
In NodeJS, try catch too but differently and explicitly with example
Exceptions, uncaught errors, and all management

### Why is that bad?
CVE-2021-22047 Expose URIs unauthorized
CVE-2021-22047: Potential Security Bypass for customized Spring Data REST Resource
https://spring.io/security/cve-2021-22047

Being Defensive=> how can this be used maliciously?

"Something Went Wrong"
* UI: Send to a login page
* API: Provide generic error message
How it should be

Brand Approach, like Github uses 404 error, that "This is not the web page you are looking for."
Github error for anything you can't access, whether it exists or not.

### Error Handling Best Practices
#### Do
* Error Early
* Include useful information for developers in an error
* Log the error
* Display something specifically crafted for customers on error

#### DO NOT
* Bypass Errors
* Expose developer information to customers

https://cheatsheetseries.owasp.org/cheatsheets/Error_Handling_Cheat_Sheet.html


https://cheatsheetseries.owasp.org/