# Scent Spot API - Test Suite

Professional API test collection for the Scent Spot e-commerce backend built with Node.js, Express and MongoDB.

## Tech Stack
- Postman / Newman
- MongoDB Atlas
- Node.js / Express
- GitHub Actions CI/CD
- JMeter (Load Testing)

## Test Coverage
- Authentication (10 test cases)
- Products (11 test cases)
- Cart (7 test cases)
- Users (10 test cases)
- Security & Middleware (5 test cases)
- **Total: 43 test cases, 168 assertions**

## QA Process — Red to Green

### Phase 1 — Test Design and Bug Discovery
Wrote 43 black-box test cases against the live API using Postman. Initial Newman run revealed 38 failing assertions across 5 modules.

Bugs discovered:
- AUTH: Validation errors returning 500 instead of 400
- AUTH: Login failures returning 400 instead of 401
- USERS: Incorrect model import causing all user endpoints to return 500
- USERS: Two controllers chained on same route
- USERS: Password exposed in API responses
- USERS: No ownership check on update/delete endpoints
- PRODUCTS: Missing return after 400 causing double response
- PRODUCTS: No quantity validation
- CART: Empty cart returning no response body
- SECURITY: No brute force protection on login endpoint

### Phase 2 — CI/CD Pipeline Setup
- Deployed backend to Railway
- Set up GitHub Actions to run Newman on every push
- Injected sensitive values via GitHub Secrets
- Pipeline showed RED with 38 failures

### Phase 3 — Bug Fixes
Fixed all root causes across auth, users, products, cart and security controllers.

### Phase 4 — Green Pipeline
After all fixes 168/168 assertions passing, 0 failures.

## Functional Test Results
| Metric | Before Fixes | After Fixes |
|--------|-------------|-------------|
| Passed | 130 | 168 |
| Failed | 38 | 0 |
| Pipeline | RED | GREEN |

## Load Test Results (JMeter)
- Virtual Users: 100
- Ramp-up: 10 seconds
- Error Rate: 0%
- APDEX: 1.0
- Average Response Time: 142ms
- Max Response Time: 438ms
- Throughput: 38 req/sec

## Run Functional Tests
newman run scent-spot-collection.json --env-var "base_url=YOUR_API_URL" --env-var "adminEmail=YOUR_ADMIN_EMAIL" --env-var "adminPassword=YOUR_ADMIN_PASSWORD" -r htmlextra

## Run Load Tests
cd /path/to/jmeter/bin
./jmeter -n -t scent-spot-load-test.jmx -l results.jtl -e -o ./report

## CI/CD
GitHub Actions automatically runs Newman tests on every push to main.
Secrets required: RAILWAY_PROD_URL, PRODUCT_ID, USER_ID, ADMIN_EMAIL, ADMIN_PASSWORD
