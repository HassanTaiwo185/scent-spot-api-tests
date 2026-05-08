# Scent Spot API - Test Suite

Professional API test collection for the Scent Spot e-commerce backend.

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

## Functional Test Results
- Total Assertions: 168
- Passed: 168
- Failed: 0

## Load Test Results (JMeter)
- Virtual Users: 100
- Error Rate: 0%
- APDEX: 1.0
- Average Response Time: 142ms
- Max Response Time: 438ms
- Throughput: 38 req/sec

## Run Functional Tests
newman run scent-spot-collection.json \
  --env-var "base_url=YOUR_API_URL" \
  --env-var "adminEmail=YOUR_ADMIN_EMAIL" \
  --env-var "adminPassword=YOUR_ADMIN_PASSWORD" \
  -r htmlextra

## Run Load Tests
cd /path/to/jmeter/bin
./jmeter -n -t scent-spot-load-test.jmx \
  -l results.jtl \
  -e -o ./report

## CI/CD
GitHub Actions automatically runs Newman tests on every push to main.
Secrets required: RAILWAY_PROD_URL, PRODUCT_ID, USER_ID, ADMIN_EMAIL, ADMIN_PASSWORD
