# Information Leak

## Server Information Leak
Broadcasting Tech Stack

### Server Info Leak = tech stack advertisement in headers
* Web Servers advertise in headers by default
* Appliances can also add headers
* These headers have no benefit
* Detecting and removing them is easy
* Finding server information and versions from headers to source codes and known vulnerabilities

### Analyze your headers
1. Use a client to access the API (nothing cached)
2. Headers will be returned in any client or programming language
3. Look for:
	1. Server
	2. X-Powered-By
	3. X-Version

### Solutions of this?
* UVICORN -> --no-server-headers option to disable
* Nginx --> nginx.conf ADD server_tokens off;
* Express --> install helmet.js or request.removeHeader(`X-Powered-By`)

