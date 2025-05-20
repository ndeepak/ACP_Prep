# How to Write Good Documentation
##### [How to Write Good Documentation](https://university.apisec.ai/products/api-documentation-best-practices/categories/2153548927)
---
### 🎯 Know Your Audience
Identify who you're writing for:
- 👨‍💻 Developers (Internal or External)    
- 🔒 Security-gated users    
- 🌐 End consumers (Ungated or Public)

---
### 🛠️ Tips for Generating Useful API Reference
Ensure your API documentation includes:
#### ✅ Request Details:
- API version (`/v2` path or custom headers)    
- Authentication & headers (e.g. Token, OAuth, JWT)    
- Endpoint path (e.g. `/products/{product_id}`)    
- HTTP methods (GET, POST, PUT, DELETE)    
- Request fields & location (path, query string, body)    
#### ✅ Response Details:
- Data expected in responses    
- Example requests & responses    
- HTTP status codes for each method    
- Status code meanings for each call
---
Quick tips on documentation reading:
Let your developers try it.
This is where you want Developer Advocacy: Have your internal developers read your work, even if dedicated roles don't exist, recruit developers (who didn't build the API) to try and follow the documentation to use it. When they do this, take note of:
* Any friction points in the process
	* Where did they struggle? What could be clearer? Is there too much jargon?
* Auth is a very common sticking point, and should be step 1 in "Getting Started"
	* Be sure that the process to get an access token is clear and well tested

---
### 👀 Tips for Reviewing Docs Internally
Encourage **Developer Advocacy**:
- Have **internal developers** (who didn’t build the API) **try** using the documentation.    
- Identify **friction points**:    
    - Where do users struggle?        
    - What needs clarification?        
    - Is there unnecessary jargon?        
#### 🔐 Authentication = Step 1!
- Ensure the **"Getting Started"** section begins with auth    
- Make the token generation process **crystal clear and testable**

---



### ✅ **Question 1:**
**What is the prerequisite to generating any meaningful documentation?**  
➡️ **Answer:** **An OpenAPI document**

---

### ✅ **Question 2:**
**What companies were used as examples of great documentation in this module?**  
➡️ **Answer:** **Twilio and Stripe**

---

### ✅ **Question 3:**
**What are the benefits of using a documentation generator?**  
➡️ **Answer:** **All of the above**
- (✔️ Increased accuracy and less time to market)    
- (✔️ Quickly create an initial reference to share)    
- (✔️ Easily update when the API changes)

---


