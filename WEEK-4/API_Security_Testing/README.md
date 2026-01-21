# API Security Testing (OWASP crAPI)

## Overview
This section documents an API security assessment performed against the
**OWASP crAPI (Completely Ridiculous API)** application in a controlled lab
environment. The objective was to demonstrate practical API pentesting skills
such as request interception, parameter manipulation, logic testing, and impact
validation aligned with the **OWASP API Top 10**.

---

## Scope and Environment
- Target Application: OWASP crAPI
- Testing Platform: Kali Linux
- Intercepting Proxy: Caido
- Testing Methodology:
  - Manual request interception
  - Endpoint analysis
  - Parameter tampering
  - Authorization testing
  - Authentication logic testing

---

## Tools Used
- Caido (Intercepting proxy)
- Browser
- Kali Linux
- Docker (crAPI environment)

---

## Initial Interaction

Two users were created for testing.

Example user:
```json
User-1
{"name":"lazzer","email":"lazzer@hackcorp.com","number":"1234567890","password":"SuperStrong@123"}
```

This allowed validation of authorization flaws by attempting cross-user access.
---

## Vulnerability 1: Content Discovery & Sensitive Data Exposure
### Observation

While browsing the community posts feature, the frontend did not reveal much
information. However, inspection of backend API responses using Caido revealed
that the API exposes sensitive user information.

### Evidence

The intercepted response contained:
```
"author": {
  "nickname": "Robot",
  "email": "robot001@example.com",
  "vehicleid": "4bae9968-ec7f-4de3-a3a0-ba1b2ab5e5c",
  "created_at": "2026-01-19T18:07:16.065Z"
}

```

This behavior exposes:

- Email addresses

- Internal user identifiers

- Vehicle identifiers

📸 Screenshots:
API_Security_Testing/Evidence/content-discovery-1.png
API_Security_Testing/Evidence/content-discovery-2.png


### Impact

This represents Excessive Data Exposure, allowing attackers to collect user
information for further targeted attacks.


## Vulnerability 2: IDOR / BOLA (Broken Object Level Authorization)
### Observation

Using the Contact Mechanic feature, backend requests containing ID parameters
were observed.

The request included a user-specific identifier.

By modifying the ID value to another user's ID, data belonging to other users
became accessible.

### Proof of Exploitation

By changing the ID parameter:

- Other users’ details were retrieved

- Vehicle identifiers were exposed

- Additional requests allowed fetching of other users' vehicle locations

Example sensitive field abused:

```
"vehicleid": "4bae9968-ec7f-4de3-a3a0-ba1b2ab5e5c"

```
This was later used to successfully retrieve vehicle location information.

📸 Screenshots:

API_Security_Testing/Evidence/idor-request.png
API_Security_Testing/Evidence/idor-response.png
API_Security_Testing/Evidence/location-access.png


### Impact

This confirms a BOLA (Broken Object Level Authorization) vulnerability.
Any authenticated user can access other users’ sensitive data by modifying
request parameters.


## Vulnerability 3: OTP Bypass → Account Takeover
### Observation

The password reset functionality required OTP verification.

Invalid OTP attempts returned:
```
{ "message": "Invalid OTP! Please try again.." }
```

After multiple attempts, rate-limiting was enforced:
```
{ "message": "You've exceeded the number of attempts." }

```

### Bypass Technique

By modifying the API version header to an older version, the rate-limiting
controls were bypassed.

This allowed OTP brute-forcing to succeed.

Successful request:
```
{"email":"robot001@example.com","otp":"4872","password":"Password@123"}

```

The password reset succeeded, resulting in full account takeover.

📸 Screenshots:

API_Security_Testing/Evidence/otp-bypass-header.png
API_Security_Testing/Evidence/otp-success.png
API_Security_Testing/Evidence/account-access.png

### Impact

This vulnerability allows:

- OTP brute-force attacks

- Password reset abuse

- Full account takeover

- Abuse of legacy API versions

This maps to Broken Authentication and Improper API Versioning Controls
within the OWASP API Top 10.
