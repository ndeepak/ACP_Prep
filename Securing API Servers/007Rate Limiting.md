# 🔐 **Rate Limiting – Detailed Notes**
---
## ✅ **What is Rate Limiting?**
**Rate Limiting** is the process of **restricting the number of requests** a user, client, or system can make to a service (like an API) over a certain period. It helps prevent abuse, maintain performance, and protect systems from **DoS attacks, scraping, brute force, and budget depletion**.

---
### 📊 Example Headers (HTTP/1.1 RateLimit Headers):
```http
RateLimit-Limit: 10        # Total allowed requests in the window
RateLimit-Remaining: 1     # How many requests are left before reset
RateLimit-Reset: 7         # Time (in seconds) until the limit resets
```

These headers help clients **understand** their quota and manage requests accordingly.

---
### 🚫 HTTP Status Code: `429 Too Many Requests`
This is the **standard response** when a rate limit is exceeded. It tells the client to **slow down**.

---
## 🎯 Why Use Rate Limiting?
OWASP 2023 lists **API4: Unrestricted Resource Consumption** as a top API vulnerability. Rate limiting directly mitigates it. [[API4 2023 Unrestricted Resource Consumption Unrestricted Resource Consumption]]

**Benefits:**
- 🔄 **Service Availability** – Prevent overloads or crashes    
- 🔐 **Security** – Stops brute-force, scraping, API abuse    
- 💰 **Budget Protection** – Prevents unnecessary cloud resource usage    
- 📊 **Fair Usage Enforcement** – Ensures equitable access

---
## 🧱 Limiting in Layers
Rate limiting can be enforced at multiple levels:

|Layer|Description|
|---|---|
|**1. Gateway**|API Gateway (like Kong, NGINX) blocks requests|
|**2. Service**|App logic enforces request caps|
|**3. Server**|Web server-level (e.g., Apache modules)|
|**4. Endpoint**|Limit per specific API function|
|**5. User**|Unique user-based quotas|
|**6. Client Sig.**|Device/browser fingerprinting-based|
|**7. Quota**|Monthly/weekly/daily limits|
|**8. Logic**|Limits based on business context|

---

## 🧪 **Sandbox Case Study (CRAPI)**
**Scenario: 'Contact Mechanic' feature abuse**
- 💥 **Layer 7 DoS attack** (application level)    
- ❌ No auth → endpoint open to bots    
- 🧨 Endless DB inserts slow down the system    
- ❓ Questions to consider:    
    - Should this endpoint be authenticated?        
    - What’s the intended frequency of usage?        
    - Can we rate-limit based on IP or session?

---
## 🚨 Attack Scenarios & Rate Limiting Mitigation
---
### **Scenario 1: Application Layer DDoS (Layer 7 DoS)**
- **Botnets** flood a public endpoint    
- **XSS** reflected input tricks users into clicking
**Mitigation:**
- Require auth    
- Throttle by **user ID** or **client signature**    
- Apply CAPTCHAs or JS challenges    

---
### **Scenario 2: Impatient User**
- User hammers refresh/clicks many times quickly
- Often **accidental** but causes load    

**Mitigation:**
- Implement browser-side **debounce** logic    
- Return HTTP `429` or even Twitter-style `420 Enhance Your Calm` (legacy)    

---

### **Scenario 3: Brute Forcing and Scraping**
- Attacker trying all 4-digit pins → 10,000 combos    
- Or scraping user data using scripts    

**Mitigation:**
- Track attempts per **session** or **user**    
- Track attempts across IP/client signature    
- Add CAPTCHAs after threshold    
- Set increasing time delays or lockouts    

---
### **Scenario 4: Budget Server Defense**
Your API costs money:
- Query-heavy endpoints    
- Auto-scaling infrastructure    

**Mitigation:**
- Limit concurrency (e.g., only 1 job at a time)    
- Quota limits (e.g., 500MB queries/day)    
- Use **caching** and **query hashing**    

---
## ⚙️ Tech Tips for Implementing Rate Limiting

|Tip|Reason|
|---|---|
|❌ Avoid SQL-based throttling|Slow and can be abused|
|❌ Avoid disk-based throttling|Inefficient for high-throughput APIs|
|✅ Use cache (e.g., Redis, Memcached)|Fast and efficient|
|✅ Track by IP + User|Helps manage both per-user and global limits|
|✅ Use TTL (Time To Live) counters|Easy reset of request limits|

---

### 🧠 **Throttle Example with Cache (e.g., Redis)**
#### ✅ For Rate Limiting:
```bash
Key = user_123
Value = count
TTL = 60 seconds
```

Each time a request is made, increment the count. If it exceeds the limit (e.g., 10), return `429`.
#### ✅ For Caching Responses:
```bash
Key = sha256(GET:/api/products?id=5)
Value = JSON result
TTL = 5 mins
```

---
### 🗂️ Quotas vs Rate Limiting

|Feature|Quotas|Rate Limiting|
|---|---|---|
|Time Window|Monthly/Daily/Weekly|Per minute/hour/second|
|Purpose|Fair billing or usage cap|Prevent burst traffic|
|Example|10,000 API calls/month|100 requests/minute|

---
## ✅ Summary: Checklist
- [ ]  Do endpoints have a reasonable rate limit?    
- [ ]  Are limits based on user, IP, or API key?    
- [ ]  Is caching used instead of DB/disk?    
- [ ]  Is there a fallback for burst scenarios (queue, retry-after)?    
- [ ]  Are limits visible to the user (via headers)?    
- [ ]  Are unauthenticated endpoints locked down?
---

### ✅ **Question 1: User Enumeration is...**
> **Correct Answer:** Determining valid from invalid accounts through brute force.
**Explanation:** User Enumeration is a security vulnerability where an attacker can **distinguish valid usernames/emails from invalid ones** based on system responses.
🔍 **Example:**
- Login error:    
    - ❌ Invalid username → "User not found"        
    - ✅ Valid username but wrong password → "Incorrect password"        
- Attacker uses this to verify which usernames exist → **enumeration attack**    

🔐 **Mitigation:**
- Always return **generic messages** like `"Invalid credentials"` regardless of username validity.

---
### ✅ **Question 2: Standard HTTP Status Code for “Too Many Requests”**
> **Correct Answer:** **429**
**Explanation:** HTTP `429 Too Many Requests` is the official status code used when a user or client has sent too many requests in a short time and has **hit a rate limit**.
🧠 Other options:
- `411` – Length Required    
- `414` – URI Too Long    
- `420` – Non-standard (used by early Twitter, not part of HTTP spec)
---
### ✅ **Question 3: Which of the following is NOT a vector for an application layer DoS?**
> **Correct Answer:** **Mass DNS reflection attack**

**Explanation:**
- An **application layer DoS (Layer 7)** targets the app directly – login forms, search fields, account creation, etc.    
- A **Mass DNS Reflection Attack** is a **network-layer (Layer 3/4)** attack, using spoofed DNS queries to **overwhelm a target server**, not the application logic.    

🧨 **Application Layer DoS vectors include:**
- Botnets hammering a login or search API    
- XSS triggering thousands of users to access your app simultaneously    
- Even **legitimate users** overwhelming a poorly scaled endpoint    
---
