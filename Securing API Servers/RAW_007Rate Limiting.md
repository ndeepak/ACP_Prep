# Rate Limiting

### rate limiting = Setting inbound limitations to ensure a service level and reliability
1. RateLimit Headers
	1. RateLimit-Limit: 10
	2. RateLimit-Remaining: 1
	3. RateLimit-Reset: 7
2. HTTP Status: 429
3. Scope: user, origin, global, resource, endpoint
4. Server Side Throttling

### Why Rate Limit?
* [[API4 2023 Unrestricted Resource Consumption Unrestricted Resource Consumption]] OWASP-API-4: Unrestricted Resource Consumption
* Service Availability
* Security
* Budget

### Limiting in Layers
1. Gateway / Network Appliance
2. Service
3. Server
4. Endpoint
5. User
6. Client Signature
7. Quota
8. Logic

### Sandbox
OWASP CRAPI has a rate limiting issue
* Perform a layer 7 DoS using 'contact mechanic' feature
	* Should it be authenticated?
	* How often should someone use this function?
	* Are there any restrictions to enforce this?
* What's happening?
	* An unauthenticated endpoint
	* it's allowing the DB to be locked with inserts

#### Scenario 1: Application Layer DDoS
Botnet: Bots are coordinating bursts of requests to an endpoint
XSS: request come through people clicking on crafted links that reflect to your endpoint

Requiring Authentication helps, throttle by User Or Client signature after that.


#### Scenario 2: Impatient User
Easily identified by identical requests

Manageable through a browser 'debounce'
	420 Enhance Your Calm (Twitter)
	Returned by Version 1 of the twitter search and trends API when the client is being rate limited; version 1.1. and later use the 429 Too Many Requests response code instead.

#### Scenario 3: The Brute Force
1. 4-digit Pin=10,000 combinations
2. User Enumeration
3. Scraping
* Attempts within a session can be easily counted
* Across a session use a client signature to keep a count of attempts


https://sitechecker.pro/what-is-420-status-code/
https://devcommunity.x.com/t/increase-in-420-enhance-your-calm/50714
https://evertpot.com/http/420-enhance-your-calm


#### Scenario 3: The Budget Server
Hosting resources cost `$$`
Don't get hit in the wallet

The more processing or scaling invoked by an endpoint the higher the cost will be not limiting.

Limit concurrency or scope of queries
Limit by quotas


### Tech Tips
* Avoid SQL operations to manage throttling
* Avoid disk operations
* Include IP with User
* Use cache where appropriate, (same query)
	* Example throttle Solution - memcache style
		* Key=user
		* value= scope
		* TTL=time frame of throttle
	* Example cache solution = memcache or key value store:
		* key=hash of the query
		* value=result
		* short TTL
