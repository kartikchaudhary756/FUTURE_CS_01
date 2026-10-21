# FUTURE_CS_01 — Web Application Vulnerability Assessment

## Future Interns Cyber Security Internship — Task 1

This repository contains my submission for Task 1 of the Future Interns Cyber Security Internship.

The task involved performing a read-only vulnerability assessment of a publicly hosted web application and documenting observable security weaknesses, their risk levels, and recommended remediation steps.

---

## Target

**Website:** http://owasp-juice.shop

**Assessment Date:** 21 October 2026

**Assessment Type:** Read-only Passive Web Application Assessment

---

## Objective

The objective of this assessment was to:

- Identify exposed services and basic network exposure.
- Review HTTP security headers and configuration.
- Perform passive analysis using OWASP ZAP.
- Identify observable security weaknesses.
- Classify findings by risk level.
- Provide practical remediation recommendations.

---

## Scope & Methodology

The assessment was performed using a **read-only and non-invasive approach**.

### Performed

- Public-facing page review
- Nmap port and exposure analysis
- OWASP ZAP passive scanning
- HTTP security-header analysis
- Browser/network inspection
- Configuration observations
- Risk classification
- Remediation recommendations

### Not Performed

- Exploitation
- Login bypass
- Brute force
- Denial-of-service
- Any activity intended to harm or disrupt the target

---

## Tools Used

- **Nmap** — Port and service exposure analysis
- **OWASP ZAP 2.17.0** — Passive web application security analysis
- **Firefox Developer Tools** — Browser and network inspection
- **Kali Linux** — Assessment environment

---

## Key Findings

| ID | Finding | Risk |
|---|---|---|
| F-01 | Content Security Policy (CSP) Header Not Set | Medium |
| F-02 | Cross-Domain Misconfiguration | Medium |
| F-03 | Missing Anti-clickjacking Header | Medium |
| F-04 | Sub Resource Integrity Attribute Missing | Medium |
| F-05 | X-Content-Type-Options Header Missing | Low |
| F-06 | Information Disclosure - Suspicious Comments | Informational |

---

## Evidence

Evidence collected during the assessment is organized in the following directories:

- `Nmap/` — Nmap scan outputs and screenshots
- `owasp_zap/` — OWASP ZAP evidence and findings

Sensitive cookie/session values and other potentially sensitive information have been excluded or redacted from published evidence.

---

## Report

The complete OWASP ZAP findings are available in:

```text
owasp_zap/zap-findings.md
```
