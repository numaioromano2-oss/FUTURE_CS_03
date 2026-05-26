# FUTURE_CS_03 — API Security Risk Analysis Report

**Future Interns · Cyber Security Internship · Task 3**  
CIN: `FIT/APR26/CS8070` · Intern: Romano · Date: 07 May 2026

---

## 🎯 Overview

This repository contains the deliverables for **Task 3** of the Future Interns Cyber Security internship:  
a read-only **API Security Risk Analysis** of two public test APIs, mapped to the OWASP API Security Top 10.

---

## 🌐 APIs Tested

| API | Base URL | Purpose |
|---|---|---|
| **JSONPlaceholder** | `https://jsonplaceholder.typicode.com` | Public REST API for testing — fake user/post data |
| **ReqRes** | `https://reqres.in/api` | API testing platform with mock auth endpoints |

> Both APIs are publicly available and explicitly designed for developer testing and security learning.

---

## 📊 Findings Summary

| ID | Risk | Endpoint(s) | Severity | OWASP Ref |
|---|---|---|---|---|
| R-01 | No Authentication on Endpoints | /users, /posts, /comments | 🔴 HIGH | API1 |
| R-02 | Excessive Data Exposure | /users, /comments | 🔴 HIGH | API3 |
| R-03 | No Rate Limiting | All endpoints | 🔴 HIGH | API4 |
| R-04 | Token Exposed in JSON Body | /api/login, /api/register | 🟡 MEDIUM | API2 |
| R-05 | Broken Object Level Authorization | /api/users/:id | 🟡 MEDIUM | API1 |
| R-06 | Missing Security Headers + Wildcard CORS | All endpoints | 🟡 MEDIUM | API8 |
| R-07 | Weak Input Validation | /api/register | 🟢 LOW | API6 |
| R-08 | No API Versioning Strategy | All endpoints | 🟢 LOW | API9 |

**Total: 8 findings — 3 High · 3 Medium · 2 Low**

---

## 🛠️ Tools Used

| Tool | Purpose |
|---|---|
| **Postman** | Send API requests, inspect responses, check headers |
| **Insomnia** | Cross-verify endpoint behaviour |
| **Browser DevTools** | Inspect request/response headers and CORS behaviour |
| **curl** | Raw HTTP request and header inspection |

---

## 🔍 Scope & Methodology

**Allowed:**
- GET requests (read-only)
- Safe POST requests (login/register test only)
- Header and response inspection
- Documentation-based analysis

**Not Performed:**
- Exploitation or bypass attempts
- Rate-limit stress testing / DoS
- Private or production API access
- Brute-force attacks

**Methodology:**
1. Endpoint enumeration and documentation review
2. Authentication requirement assessment
3. Response data analysis for excessive exposure
4. Header inspection (security headers, CORS, rate-limit headers)
5. Token handling review
6. Input validation testing (safe POST only)
7. OWASP API Top 10 risk mapping
8. Risk classification and remediation documentation

---

## 📁 Repository Structure

```
FUTURE_CS_03/
├── README.md
├── FUTURE_CS_03_API_Security_Report.html    ← full report (open in browser)
├── FUTURE_CS_03_API_Security_Report.pdf     ← Canva export
└── evidence/
    ├── postman_users_unauthenticated.png    ← R-01: no auth required
    ├── postman_excessive_data.png           ← R-02: fields returned
    ├── postman_no_ratelimit_headers.png     ← R-03: missing rate limit
    ├── reqres_token_in_body.png             ← R-04: token in JSON
    ├── reqres_bola_user_ids.png             ← R-05: any user accessible
    ├── curl_missing_headers.png             ← R-06: security headers
    └── postman_weak_password.png            ← R-07: 1-char password accepted
```

---

## 📌 Top Remediations

1. **[P1]** Require Bearer token / API key on all data endpoints
2. **[P1]** Implement rate limiting — return 429 with Retry-After on breach
3. **[P1]** Strip unnecessary fields from all API responses (data minimisation)
4. **[P2]** Move auth tokens to HttpOnly Secure cookies — not JSON body
5. **[P2]** Validate object ownership on every user-specific request
6. **[P2]** Restrict CORS to specific origins — remove wildcard

---

## 📚 References

- [OWASP API Security Top 10 (2023)](https://github.com/OWASP/API-Security)
- [API Security Checklist](https://github.com/shieldfy/API-Security-Checklist)
- [JSONPlaceholder](https://jsonplaceholder.typicode.com)
- [ReqRes](https://reqres.in)
- [Public APIs Collection](https://github.com/public-apis/public-apis)

---

*Submitted as part of the Future Interns Cyber Security Internship Programme.*  
*All testing was read-only and conducted against APIs designed for public testing.*
