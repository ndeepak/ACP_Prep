# OWASP API #6 - Unrestricted Access to Sensitive Business Flows
##### [OWASP API Top 10 + Real-World Breaches](https://university.apisec.ai/products/api-security-fundamentals-2025/categories/2157142220)
[[API6 2023 Unrestricted Access to Sensitive Business Flows]]

What is it? 
* Abuse of a legitimate business workflow 
* Excessive, automated use
* Typically result of application logic flaw 

Examples, Risk Exposure 
* Loss of critical business activity 
* Mass, automated ticket purchasing 
* High volume referral bonuses 
* Brute forcing incremental IDs

Prevention
• Consider not just how your application is meant to work
• Avoid use of incremental IDs
• Train API owners, developers to consider non "happy path" usage
• Think like a hacker - how can your app be abused/misused

https://time.com/4922700/instagram-security-breach-verified-users/
https://www.nbcnews.com/tech/social-media/hackers-exploited-instagram-bug-get-celebrity-phone-numbers-emails-n798091
