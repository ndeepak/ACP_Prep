Question 1

###### What is the most common area where injection flaws are often found?

Within input parameters that are expected to be sent to an interpreter

Correct answer.

With the webpage's HTML

API requests that involve XML instead of JSON.

Within HTTP DELETE requests

Question 2

###### When is an API considered to be vulnerable to injection flaws?

If client-supplied data is validated, filtered, or sanitized by the API.

If data coming from external systems is validated, filtered, or sanitized by the API.

If client-supplied data is directly used or concatenated to SQL/NoSQL/LDAP queries, OS commands, XML parsers, and ORM/ODM without validation.

Correct answer.

If the API uses secure data transmission channels.

Question 3

###### What is a key prevention strategy for injection flaws in APIs?

Disable user input in API endpoints.

Allowing unrestricted data flow from integrated systems.

Keep data separate from commands and queries, and ensuring data validation using a reliable library.

Correct answer.

Accept all special characters in user input data.

Question 4

###### Which of the following is NOT a vulnerability in terms of API logging and monitoring?

API does not produce any logs.

Log integrity is guaranteed.

Correct answer.

Logs are not continuously monitored.

API infrastructure is not continuously monitored.

Question 5

###### What are the key measures to prevent the misuse of APIs due to lack of sufficient logging and monitoring?

Log all failed authentication attempts, denied access, and input validation errors.

Use a Security Information and Event Management (SIEM) system to aggregate and manage logs from all components of the API stack and hosts.

Configure custom dashboards and alerts, enabling suspicious activities to be detected and responded to earlier.

All of the above.

Correct answer.

Question 6

###### Which of the following can be considered a business logic vulnerability?

An application that uses base64 to encode data

An application that posts unvalidated input publicly

An application that allows trusted end users to upload and execute code without restrictions

Correct answer.

An application that exposes unsupported endpoints

Question 7

###### A rule of thumb to identify business-logic vulnerabilities is:

Fuzzing request parameters

Brute-forcing user authentication processes

Understanding business functions and how a feature could be leveraged in an attack

Correct answer.

Making requests to endpoint versions that are not included in documentation

Question 8

###### According to OWASP, which vulnerability is still an unsolved problem, but is more relevant to the 2019 OWASP API Security Top 10?

Insecure Design

Incorrect.

Business Logic Flaws

Broken Object Level Authorization

Injection

Question 9

###### Which of the vulnerabilities beyond the 2023 OWASP Top 10 is the most difficult to identify generically?

Injection

Business Logic Flaws

Correct answer.

Broken Function Level Authorization

Insufficient Logging and Monitoring

Question 10

###### Which of the vulnerabilities beyond the 2023 OWASP Top 10 will most likely lead to user-supplied code being executed?

Injection

Correct answer.

Insufficient Logging and Monitoring

Mass Assignment

Business Logic Flaws