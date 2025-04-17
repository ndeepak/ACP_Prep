##### [Cross Origin Resource Sharing (CORS)](https://university.apisec.ai/products/securing-api-servers/categories/2153643293)
CORS is a set of browser controls set by web servers CORS defines what responses are allowed from where
* Origins
* Credentials
* Methods
* Headers

Why use CORS?
* You have an API or web server with something to protect
	* User data
	* Intellectual property
	* Branding

* When CORS Helps?
	* Malicious System --> API
	* Malicious Site --> CORS Blocked (Unsuspecting Users)

Common CORS Scenarios
* Create a new server for an API
* The server is set with some basic security in place
* Developer gets a CORS allow-Origin error from a localhost test
* Developer "Fixes" the error by bypassing CORS
* This hole is never plugged for production


CORS Solution
* Set the headers, define what is allowed


