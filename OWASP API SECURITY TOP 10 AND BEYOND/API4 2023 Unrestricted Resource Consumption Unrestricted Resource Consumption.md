# Unrestricted Resource Consumption
##### [API4:2023 Unrestricted Resource Consumption](https://university.apisec.ai/products/owasp-api-security-top-10-and-beyond/categories/2152492155)
### **API4:2023 - Unrestricted Resource Consumption**
#### **Introduction**
Unrestricted Resource Consumption is a security issue where an API **does not** enforce limits on the consumption of its resources. This can lead to:
- **Denial of Service (DoS) attacks**    
- **Increased financial costs** due to excessive resource usage    
- **Service degradation** affecting other users    
This issue was previously known as **API4:2019 - Lack of Resources and Rate Limiting**, but the 2023 update highlights the broader impact, including **cloud infrastructure costs and operational expenses**.

---
### **How Attackers Exploit This Vulnerability**
Attackers or malicious users can:
1. **Send excessive API requests** to overload the system.    
2. **Use automated tools** to flood the API with high loads of traffic.    
3. **Exploit batch operations** (e.g., sending a single request that retrieves massive amounts of data).    
4. **Craft API requests with large parameters** (e.g., requesting thousands of records in one response).    
5. **Abuse costly operations** (e.g., performing expensive database queries).    
Since API requests require processing power, memory, and bandwidth, **failing to limit resource usage can cause service disruptions** and **financial losses**.

---
### **Common API Weaknesses**
APIs are vulnerable when they lack limitations such as:  
✅ **Execution timeouts** – Prevents long-running requests.  
✅ **Memory allocation limits** – Stops excessive memory consumption.  
✅ **File descriptor limits** – Controls the number of open files.  
✅ **Process limits** – Restricts the number of concurrent API executions.  
✅ **Upload file size limits** – Prevents excessive file uploads.  
✅ **Query limits** – Restricts the number of records per request.  
✅ **Rate limiting & request throttling** – Limits API calls within a timeframe.  
✅ **Spending limits for third-party services** – Controls cloud costs for APIs using external services.
Without these safeguards, an API can suffer from **resource starvation**, leading to **downtime or financial loss**.

---

### **Impact of Unrestricted Resource Consumption**
💥 **Denial of Service (DoS) or Distributed DoS (DDoS)** – Overwhelms the API and makes it unavailable to legitimate users.  
💰 **High operational costs** – More API requests can lead to **increased cloud or infrastructure expenses** (e.g., auto-scaling).  
📉 **Poor user experience** – API performance degrades, causing slow responses or service failures.  
🚨 **Abuse of monetization models** – Attackers can bypass API rate limits and extract excessive data without paying.

---

### **How to Prevent Unrestricted Resource Consumption**
🔒 **Implement Rate Limiting & Throttling**
- Limit how many requests a client can make **per minute/hour/day**.    
- Return HTTP **429 Too Many Requests** when the limit is exceeded.    
- Example using **NGINX**:
```nginx
limit_req_zone $binary_remote_addr zone=api_limit:10m rate=100r/s;
server {
    location /api/ {
        limit_req zone=api_limit burst=20;
    }
}
```
🛑 **Set API Usage Limits**
- Define **maximum records per response** (e.g., max 100 records instead of 10,000).
- Restrict the **number of operations per batch request**.    
- Example using **GraphQL**:
```graphql
query {
    users(limit: 100) {  # Prevents returning unlimited users
        id
        name
    }
}
```

📏 **Enforce Execution & Resource Limits**
- Set **timeouts** on API execution to prevent long-running requests.
- Limit **memory usage per request**.    
- Restrict **max upload size** to prevent abuse (e.g., 5MB max file upload).    

💡 **Monitor and Alert on API Usage**
- Track **suspicious spikes in requests**.    
- Detect **abnormal API behavior** using logging and monitoring tools (e.g., Prometheus, ELK stack).
---
## Additional Resources
- ["Availability" - Web Service Security Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Web_Service_Security_Cheat_Sheet.html#availability)
- ["DoS Prevention" - GraphQL Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/GraphQL_Cheat_Sheet.html#dos-prevention)
- ["Mitigating Batching Attacks" - GraphQL Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/GraphQL_Cheat_Sheet.html#mitigating-batching-attacks)
- [CWE-770: Allocation of Resources Without Limits or Throttling](https://cwe.mitre.org/data/definitions/770.html)
- [CWE-400: Uncontrolled Resource Consumption](https://cwe.mitre.org/data/definitions/400.html)
- [CWE-799: Improper Control of Interaction Frequency](https://cwe.mitre.org/data/definitions/799.html)
- "Rate Limiting (Throttling)" - [Security Strategies for Microservices-based Application Systems](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-204.pdf), NIST