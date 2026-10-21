# ZAP Passive Scan Findings

## Target
http://owasp-juice.shop

## Assessment Type
Read-Only / Passive Web Application Security Assessment

## Tool
OWASP ZAP 2.17.0

### Overview

Screenshot:

<img width="1920" height="982" alt="zap_01_ overview" src="https://github.com/user-attachments/assets/c941cc21-a73d-4732-95e0-235aa1279f74" />


---

# 1. Content Security Policy (CSP) Header Not Set

**Risk:** Medium  
**Confidence:** High  
**CWE:** CWE-693

### Description

The application does not set a Content-Security-Policy (CSP) HTTP response header.

CSP tells the browser which sources are allowed to load content such as scripts, styles, images, fonts and frames on a page. It helps reduce the impact of attacks like Cross-Site Scripting (XSS) and data injection.

### Security Impact

Without a CSP, the browser does not restrict where scripts and other content can be loaded from. If an attacker manages to inject malicious content through another vulnerability, the browser has no policy to block it. This can make attacks like XSS more damaging.

### Recommendation

Ensure that your web server, application server, load balancer, etc. is configured to set the Content-Security-Policy header.

### Evidence

Screenshot:

<img width="1920" height="983" alt="Security_Header_missing" src="https://github.com/user-attachments/assets/e8a5b92c-77b9-4735-b6e0-c8ca08efc1e5" />


---

# 2. Cross-Domain Misconfiguration

**Risk:** Medium  
**Confidence:** Medium  
**CWE:** CWE-264

### Description

The web server has a Cross-Origin Resource Sharing (CORS) misconfiguration. The `Access-Control-Allow-Origin` header is set too permissively, which may allow web pages from other domains to load data from this application in the browser.

### Security Impact

If a website allows requests from any origin, a malicious website can make a user's browser read its responses. If any of that data is sensitive and not protected by authentication, it could be exposed to other domains.

### Recommendation

- Make sure sensitive data is not available without authentication (for example, use IP address allow-listing).
- Set the `Access-Control-Allow-Origin` header to a short list of trusted domains, or remove the CORS headers completely so the browser enforces the Same Origin Policy (SOP).

### Evidence

Screenshot:
<img width="1920" height="983" alt="Domain_Misconfiguration" src="https://github.com/user-attachments/assets/9e91684f-32b1-4b9f-9890-f42395a0bde4" />


---

# 3. Missing Anti-clickjacking Header

**Risk:** Medium  
**Confidence:** Medium  
**CWE:** CWE-1021

### Description

The application's response does not protect against clickjacking attacks. It does not include a Content-Security-Policy header with the `frame-ancestors` directive, or an `X-Frame-Options` header.

### Security Impact

Without these headers, another website can load this application's pages inside a hidden or disguised frame. An attacker can then trick a user into clicking something on the page without realizing it, which may cause the user to perform unintended actions.

### Recommendation

Set either the `Content-Security-Policy` header (with `frame-ancestors`) or the `X-Frame-Options` header on all pages returned by the application.

- Use `X-Frame-Options: DENY` if the page should never be framed.
- Use `X-Frame-Options: SAMEORIGIN` if the page should only be framed by pages on the same server.
- Alternatively, use the `frame-ancestors` directive in the Content-Security-Policy header.

### Evidence

Screenshot:

<img width="1920" height="983" alt="Missing Anti-Header" src="https://github.com/user-attachments/assets/22947a99-5a1b-439f-8842-972d12e1e87e" />

---

# 4. Sub Resource Integrity Attribute Missing

**Risk:** Medium  
**Confidence:** High  
**CWE:** CWE-345

### Description

The `integrity` attribute is missing on a `<script>` or `<link>` tag that loads a file from an external server. This attribute lets the browser check that the file has not been changed.

### Security Impact

If the external server is compromised, an attacker can change the file it serves and inject malicious content. Without the `integrity` attribute, the browser will load and run the modified file without any check, which could affect everyone who visits the application.

### Recommendation

Add a valid `integrity` attribute to the `<script>` or `<link>` tag that loads the external resource.

### Evidence

Screenshot:
<img width="1920" height="983" alt="Attribute_Missing" src="https://github.com/user-attachments/assets/c8021499-d1bb-4b00-ab32-a211307133e9" />

---

# 5. X-Content-Type-Options Header Missing

**Risk:** Low  
**Confidence:** Medium  
**CWE:** CWE-693

### Description

The `X-Content-Type-Options` header is not set to `nosniff`. Because of this, some browsers (mainly older versions of Internet Explorer and Chrome) may try to guess the content type of a response instead of using the type declared by the server.

### Security Impact

If a browser guesses the content type, it may treat a response as a different type than the server intended, for example showing or running content that should have been treated as plain data. This could be abused to deliver unexpected content to users. The risk is low because modern browsers such as Firefox use the declared content type.

### Recommendation

- Make sure the server sets the `Content-Type` header correctly.
- Set `X-Content-Type-Options: nosniff` on all web pages.
- If possible, encourage users to use a modern, standards-compliant browser that does not perform MIME-sniffing.

### Evidence

Screenshot:

<img width="1920" height="983" alt="missing_header" src="https://github.com/user-attachments/assets/6e26eaf9-25d9-4318-9228-a8d601f7d9f2" />

---

# 6. Information Disclosure - Suspicious Comments

**Risk:** Informational  
**Confidence:** Medium  
**CWE:** CWE-615

### Description

The response contains comments that may reveal information about the application, such as unfinished work or how it is built. These comments are visible to anyone who views the page source.

### Security Impact

On its own, this is not a vulnerability. However, comments left in public code may give an attacker small hints about the application's internals or known problems, which could help them plan an attack.

### Recommendation

Remove all comments that reveal information an attacker could use, and fix any underlying problems those comments refer to.

### Evidence

Screenshot:

<img width="1920" height="983" alt="Information Disclosure" src="https://github.com/user-attachments/assets/19a64bc6-218b-42d8-8bd2-5db7156afb4a" />

---

# Findings Summary

| ID | Finding | Risk | Confidence |
|----|---------|------|------------|
| ZAP-02 | Content Security Policy (CSP) Header Not Set | Medium | High |
| ZAP-03 | Cross-Domain Misconfiguration | Medium | Medium |
| ZAP-05 | Missing Anti-clickjacking Header | Medium | Medium |
| ZAP-06 | Sub Resource Integrity Attribute Missing | Medium | High |
| ZAP-07 | X-Content-Type-Options Header Missing | Low | Medium |
| ZAP-09 | Information Disclosure - Suspicious Comments | Informational | Medium |

---

# Assessment Limitations

This assessment was performed using passive/read-only techniques.

No exploitation, brute-force attacks, login bypass, denial-of-service, or other disruptive testing was performed.

The findings represent observations made by OWASP ZAP during the assessment and should be validated by the application owner before remediation.
