# Scent Spot API — Test Suite & QA Pipeline

> A complete API testing project: 43 test cases, 168 assertions, automated CI/CD pipeline, and a JMeter load test — applied to a live Node.js/Express e-commerce backend.

[![Tests](https://img.shields.io/badge/assertions-168%20passing-brightgreen)](https://github.com/HassanTaiwo185/scent-spot-api-tests)
[![Pipeline](https://img.shields.io/badge/pipeline-green-brightgreen)](https://github.com/HassanTaiwo185/scent-spot-api-tests/actions)
[![Load test](https://img.shields.io/badge/load%20test-0%25%20error%20rate-brightgreen)](https://github.com/HassanTaiwo185/scent-spot-api-tests)

---

## What this project demonstrates

This is not just a test collection — it's a full QA engineering workflow applied to a real backend:

1. **Black-box test design** against a live API with no access to the source code
2. **Bug discovery** — 10 bugs found including security vulnerabilities
3. **Root cause reporting** to the backend developer with enough detail to reproduce and fix each issue
4. **CI/CD pipeline** that runs the full test suite automatically on every push
5. **Load testing** to validate the API holds up under concurrent traffic
6. **Green pipeline achieved** — 168/168 assertions passing after all fixes were applied

---

## The backend under test

Scent Spot is an e-commerce API built with Node.js, Express, and MongoDB Atlas. It handles authentication, product management, shopping cart, and user management.

The test suite treats it as a black box — tests were written against the API contract (expected inputs, outputs, and status codes) without reading the implementation.

---

## Test coverage

| Module | Test cases | Assertions |
|---|---|---|
| Authentication | 10 | ~40 |
| Products | 11 | ~45 |
| Cart | 7 | ~28 |
| Users | 10 | ~40 |
| Security & Middleware | 5 | ~15 |
| **Total** | **43** | **168** |

---

## QA process — red to green

### Phase 1 — Test design and initial run

Wrote 43 black-box test cases in Postman covering happy paths, edge cases, validation errors, auth failures, and security boundaries. First Newman run revealed **38 failing assertions** across all 5 modules.

### Phase 2 — Bug discovery

The failing assertions uncovered 10 bugs:

| # | Module | Bug | Severity |
|---|---|---|---|
| 1 | Auth | Validation errors returning `500` instead of `400` | Medium |
| 2 | Auth | Login failures returning `400` instead of `401` | Low |
| 3 | Users | Incorrect model import causing all user endpoints to return `500` | High |
| 4 | Users | Two controllers chained on same route causing double execution | High |
| 5 | Users | **Password exposed in API responses** | **Critical** |
| 6 | Users | **No ownership check on update/delete — any user could modify another user's data** | **Critical** |
| 7 | Products | Missing `return` after `400` response causing double response error | Medium |
| 8 | Products | No quantity validation on stock fields | Medium |
| 9 | Cart | Empty cart returning no response body | Low |
| 10 | Security | No brute force protection on login endpoint | High |

Two of these are security vulnerabilities: passwords being returned in API responses, and missing ownership checks that would allow any authenticated user to edit or delete another user's account. Both were caught purely through systematic black-box testing.

### Phase 3 — Bug fixes

All 10 bugs were fixed in the backend (`scent-spot-backend`). Each fix was verified by re-running the affected test cases.

### Phase 4 — Green pipeline

After all fixes: **168/168 assertions passing, 0 failures.**

---

## Functional test results

| Metric | Before fixes | After fixes |
|---|---|---|
| Assertions passed | 130 | 168 |
| Assertions failed | 38 | 0 |
| Pipeline status | 🔴 RED | 🟢 GREEN |

---

## Load test results (JMeter)

Validated the API's performance under realistic concurrent load.

| Metric | Result |
|---|---|
| Virtual users | 100 |
| Ramp-up period | 10 seconds |
| Error rate | 0% |
| APDEX score | 1.0 (perfect) |
| Average response time | 142ms |
| Max response time | 438ms |
| Throughput | 38 req/sec |

An APDEX of 1.0 means every single request under 100 concurrent users was served within the satisfactory threshold. The 142ms average response time is well within acceptable range for a cloud-hosted API.

---

## CI/CD pipeline

GitHub Actions runs the full Newman test suite automatically on every push to `main`. If any assertion fails, the pipeline goes red and deployment is blocked.

The pipeline uses GitHub Secrets for all sensitive values — no credentials are hardcoded or committed.

**Secrets required:**
- `RAILWAY_PROD_URL` — API base URL
- `ADMIN_EMAIL` / `ADMIN_PASSWORD` — test admin credentials
- `PRODUCT_ID` / `USER_ID` — seeded test data IDs

---

## Running tests locally

### Functional tests (Newman)

```bash
npm install -g newman newman-reporter-htmlextra

newman run scent-spot-collection.json \
  --env-var "base_url=YOUR_API_URL" \
  --env-var "adminEmail=YOUR_ADMIN_EMAIL" \
  --env-var "adminPassword=YOUR_ADMIN_PASSWORD" \
  -r htmlextra
```

The `htmlextra` reporter generates a full HTML report with pass/fail breakdown per request.

### Load tests (JMeter)

```bash
cd /path/to/jmeter/bin
./jmeter -n -t scent-spot-load-test.jmx -l results.jtl -e -o ./report
```

Open `./report/index.html` for the full load test dashboard.

---

## Tech stack

| Tool | Purpose |
|---|---|
| Postman | Test case design and collection authoring |
| Newman | CLI test runner (used in CI) |
| newman-reporter-htmlextra | HTML test reports |
| GitHub Actions | CI/CD pipeline |
| Apache JMeter | Load and performance testing |
| Railway | Backend deployment environment |# Scent Spot API — Test Suite & QA Pipeline

> A complete API testing project: 43 test cases, 168 assertions, automated CI/CD pipeline, and a JMeter load test — applied to a live Node.js/Express e-commerce backend.

[![Tests](https://img.shields.io/badge/assertions-168%20passing-brightgreen)](https://github.com/HassanTaiwo185/scent-spot-api-tests)
[![Pipeline](https://img.shields.io/badge/pipeline-green-brightgreen)](https://github.com/HassanTaiwo185/scent-spot-api-tests/actions)
[![Load test](https://img.shields.io/badge/load%20test-0%25%20error%20rate-brightgreen)](https://github.com/HassanTaiwo185/scent-spot-api-tests)

---

## What this project demonstrates

This is not just a test collection — it's a full QA engineering workflow applied to a real backend:

1. **Black-box test design** against a live API with no access to the source code
2. **Bug discovery** — 10 bugs found including security vulnerabilities
3. **Root cause reporting** to the backend developer with enough detail to reproduce and fix each issue
4. **CI/CD pipeline** that runs the full test suite automatically on every push
5. **Load testing** to validate the API holds up under concurrent traffic
6. **Green pipeline achieved** — 168/168 assertions passing after all fixes were applied

---

## The backend under test

Scent Spot is an e-commerce API built with Node.js, Express, and MongoDB Atlas. It handles authentication, product management, shopping cart, and user management.

The test suite treats it as a black box — tests were written against the API contract (expected inputs, outputs, and status codes) without reading the implementation.

---

## Test coverage

| Module | Test cases | Assertions |
|---|---|---|
| Authentication | 10 | ~40 |
| Products | 11 | ~45 |
| Cart | 7 | ~28 |
| Users | 10 | ~40 |
| Security & Middleware | 5 | ~15 |
| **Total** | **43** | **168** |

---

## QA process — red to green

### Phase 1 — Test design and initial run

Wrote 43 black-box test cases in Postman covering happy paths, edge cases, validation errors, auth failures, and security boundaries. First Newman run revealed **38 failing assertions** across all 5 modules.

### Phase 2 — Bug discovery

The failing assertions uncovered 10 bugs:

| # | Module | Bug | Severity |
|---|---|---|---|
| 1 | Auth | Validation errors returning `500` instead of `400` | Medium |
| 2 | Auth | Login failures returning `400` instead of `401` | Low |
| 3 | Users | Incorrect model import causing all user endpoints to return `500` | High |
| 4 | Users | Two controllers chained on same route causing double execution | High |
| 5 | Users | **Password exposed in API responses** | **Critical** |
| 6 | Users | **No ownership check on update/delete — any user could modify another user's data** | **Critical** |
| 7 | Products | Missing `return` after `400` response causing double response error | Medium |
| 8 | Products | No quantity validation on stock fields | Medium |
| 9 | Cart | Empty cart returning no response body | Low |
| 10 | Security | No brute force protection on login endpoint | High |

Two of these are security vulnerabilities: passwords being returned in API responses, and missing ownership checks that would allow any authenticated user to edit or delete another user's account. Both were caught purely through systematic black-box testing.

### Phase 3 — Bug fixes

All 10 bugs were fixed in the backend (`scent-spot-backend`). Each fix was verified by re-running the affected test cases.

### Phase 4 — Green pipeline

After all fixes: **168/168 assertions passing, 0 failures.**

---

## Functional test results

| Metric | Before fixes | After fixes |
|---|---|---|
| Assertions passed | 130 | 168 |
| Assertions failed | 38 | 0 |
| Pipeline status | 🔴 RED | 🟢 GREEN |

---

## Load test results (JMeter)

Validated the API's performance under realistic concurrent load.

| Metric | Result |
|---|---|
| Virtual users | 100 |
| Ramp-up period | 10 seconds |
| Error rate | 0% |
| APDEX score | 1.0 (perfect) |
| Average response time | 142ms |
| Max response time | 438ms |
| Throughput | 38 req/sec |

An APDEX of 1.0 means every single request under 100 concurrent users was served within the satisfactory threshold. The 142ms average response time is well within acceptable range for a cloud-hosted API.

---

## CI/CD pipeline

GitHub Actions runs the full Newman test suite automatically on every push to `main`. If any assertion fails, the pipeline goes red and deployment is blocked.

The pipeline uses GitHub Secrets for all sensitive values — no credentials are hardcoded or committed.

**Secrets required:**
- `RAILWAY_PROD_URL` — API base URL
- `ADMIN_EMAIL` / `ADMIN_PASSWORD` — test admin credentials
- `PRODUCT_ID` / `USER_ID` — seeded test data IDs

---

## Running tests locally

### Functional tests (Newman)

```bash
npm install -g newman newman-reporter-htmlextra

newman run scent-spot-collection.json \
  --env-var "base_url=YOUR_API_URL" \
  --env-var "adminEmail=YOUR_ADMIN_EMAIL" \
  --env-var "adminPassword=YOUR_ADMIN_PASSWORD" \
  -r htmlextra
```

The `htmlextra` reporter generates a full HTML report with pass/fail breakdown per request.

### Load tests (JMeter)

```bash
cd /path/to/jmeter/bin
./jmeter -n -t scent-spot-load-test.jmx -l results.jtl -e -o ./report
```

Open `./report/index.html` for the full load test dashboard.

---

## Tech stack

| Tool | Purpose |
|---|---|
| Postman | Test case design and collection authoring |
| Newman | CLI test runner (used in CI) |
| newman-reporter-htmlextra | HTML test reports |
| GitHub Actions | CI/CD pipeline |
| Apache JMeter | Load and performance testing |
| Railway | Backend deployment environment |
