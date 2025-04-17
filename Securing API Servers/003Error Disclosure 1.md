# ✅ 1. **Hands-on Error Disclosure Lab Setup**
You can simulate error disclosure in a **local environment** using Flask (Python) and Express (Node.js).

---
### 🔬 A. Python (Flask) Lab – Error Disclosure Demo
**Install Flask:**
`pip install flask`

**Code: `app.py`**
```python
from flask import Flask, request

app = Flask(__name__)

@app.route('/find-user', methods=['GET'])
def find_user():
    email = request.args.get('email')
    # Simulated user lookup
    users = ["deepak@bank.com", "admin@corp.com"]

    if email not in users:
        # BAD: reveals internal logic
        return f"User with email {email} not found!", 404

    return "User exists."

if __name__ == '__main__':
    app.run(debug=True)
```

**Exploit test:**
`curl http://127.0.0.1:5000/find-user?email=unknown@bank.com`

🔍 **Try Fixing:**
```python
# Good error handling
if email not in users:
    return "Invalid request.", 404
```

---

### 🔬 B. Node.js (Express) Lab – Stack Trace Disclosure
**Setup:**
```bash
npm init -y
npm install express
```
**Code: `app.js`**
```javascript
const express = require("express");
const app = express();

app.get("/view-file", (req, res) => {
  try {
    const filename = req.query.file;
    const fs = require("fs");
    const data = fs.readFileSync(filename, "utf8"); // Potential path traversal
    res.send(data);
  } catch (err) {
    // BAD: reveals internal error
    res.status(500).send(err.stack);
  }
});

app.listen(3000, () => console.log("Server running on http://localhost:3000"));
```

**Exploit test:**
`curl http://localhost:3000/view-file?file=../../etc/passwd`

🔍 **Try Fixing:**
`res.status(500).send("Something went wrong.");`

---

# 🧠 2. Quiz: Error Disclosure Awareness
**Q1.** What is the biggest risk of error disclosure?  
A. Faster performance  
B. Better UI  
C. Leaking sensitive internal system info ✅  
D. Showing users how smart your devs are

---

**Q2.** What is the best practice for API error response?  
A. Show full stack trace  
B. Return detailed SQL errors  
C. Return generic error message ✅  
D. Ignore error

---

**Q3.** What happens if the app says “User not found”?  
A. Secure  
B. Exposes valid/invalid usernames ✅  
C. Helps user  
D. Prevents SQL injection

---

**Q4.** Why should you avoid `debug=True` in production Flask apps?  
A. Too slow  
B. Breaks CSS  
C. Exposes stack trace and secrets ✅  
D. None

---

**Q5.** Which of these is OWASP's recommended best practice?  
A. Catch all errors silently  
B. Show exception in UI  
C. Log detailed errors and return vague message ✅  
D. Let frontend show internal logs

---

# 🛠️ 3. Error Handling Security Checklist (Dev + SecOps)

|✅|Task|
|---|---|
|🔒|Use generic user-facing error messages (e.g. "Something went wrong.")|
|🧾|Log all exceptions with stack trace (internal only)|
|🔐|Do not expose system paths, filenames, SQL queries|
|🚨|Avoid detailed auth error messages ("invalid password" vs "user not found")|
|⚙️|Disable debug mode in production (e.g., Flask `debug=False`)|
|📡|Use standard HTTP status codes (`404`, `403`, `500`)|
|🛑|Avoid stack traces or unfiltered error dumps in API/HTML|
|📄|Customize error pages (e.g. GitHub-style 404 page)|
|🔍|Test for email/user enumeration via error messages|
|📚|Educate developers: Dev errors ≠ Customer errors|

---