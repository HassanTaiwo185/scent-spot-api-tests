# Scent Spot API - Test Suite

API test collection for the Scent Spot e-commerce backend.

## Tech Stack
- Postman / Newman
- MongoDB Atlas
- Node.js / Express
- GitHub Actions CI/CD

## Test Coverage
- Authentication (10 test cases)
- Products (11 test cases)
- Cart (7 test cases)
- Users (10 test cases)
- Security & Middleware (5 test cases)

## Results
- Total Assertions: 168
- Passed: 130
- Failed: 38

## Run Tests
newman run scent-spot-collection.json -e scent-spot-environment.json -r htmlextra
