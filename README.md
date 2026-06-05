# 🔐 Cyber Security Internship — Task 1

![Internship](https://img.shields.io/badge/Internship-Future%20Interns-blue?style=for-the-badge)
![Task](https://img.shields.io/badge/Task-3%20%7C%20Vulnerability%20Assessment%20Report-red?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)
![Tools](https://img.shields.io/badge/Tools-Kali%20Linux%20%7C%20Nmap%20%7C%20OWASP%20ZAP%20%7C%20DevTools-orange?style=for-the-badge)

---

**Internship Program:** Cyber Security Internship by Future Interns

**Intern Name:** Kothamasu Sai Prasad

**Task-1:** Vulnerability Assessment Report for a Live Website

---

## 🧩 Introduction

Vulnerability assessment is the process of **identifying and analyzing security weaknesses in a system** without actively exploiting them. Unlike penetration testing, this approach focuses on discovery and classification of risks in a read-only and passive manner.

In this task, the assessment was performed on **BadSSL** — a platform specifically designed to demonstrate SSL/TLS vulnerabilities in a controlled environment.

---

## 🎯 Objective

Analyze a public website for security weaknesses using passive and read-only techniques, and document findings in a professional vulnerability assessment report.

- ✅ Analyze a public website for security weaknesses
- ✅ Identify common vulnerabilities
- ✅ Classify risks based on severity
- ✅ Provide clear remediation steps
- ✅ Present findings in a professional report

---

## 📚 What It Teaches

| Skill Area | Practical Outcome |
|---|---|
| **SSL/TLS Analysis** | Identifying expired, self-signed, and weak certificate configurations |
| **HTTP Header Inspection** | Detecting missing or misconfigured security headers |
| **Port & Service Scanning** | Using Nmap to identify open ports and services |
| **Passive Vulnerability Scanning** | Using OWASP ZAP without performing active attacks |
| **Reporting** | Writing professional vulnerability assessment reports |

---

## 🏗️ Target Details

```
┌─────────────────────────────────────────────┐
│           Assessment Environment            │
│                                             │
│  ┌────────────────────┐                     │
│  │   Kali Linux       │                     │
│  │  (Analysis Host)   │──► Passive Scan     │
│  │                    │──► Read-Only        │
│  └────────────────────┘                     │
│                                             │
│  ┌────────────────────┐                     │
│  │    badssl.com      │                     │
│  │  (Target Website)  │◄── HTTPS            │
│  └────────────────────┘                     │
└─────────────────────────────────────────────┘
```

| Component | Details |
|---|---|
| **Target Website** | https://badssl.com |
| **Scope** | Read-only testing only |
| **Approach** | Passive analysis, no exploitation |

---

## 🛠️ Tools & Software

| Tool | Purpose |
|---|---|
| Kali Linux | Analysis and scanning platform |
| Nmap | Port and service identification |
| OWASP ZAP | Passive vulnerability scanning |
| Chrome DevTools | HTTP header and network inspection |

---

## ⚙️ Assessment Methodology

The following steps were performed:

1. Explored the target website and its test endpoints
2. Analyzed SSL/TLS configurations across subdomains
3. Observed browser security warnings
4. Inspected HTTP headers using DevTools
5. Performed port and service scan using Nmap
6. Conducted passive vulnerability scanning using OWASP ZAP
7. Documented all findings with evidence

---

## 💻 Commands Used

### 1. Nmap Service Scan

```bash
nmap -sV badssl.com
```

> Identifies open ports and running services on the target host.

---

### 2. OWASP ZAP — Passive Scan

```
Action: Enter target URL → Run Automated Passive Scan
```

> Detects vulnerabilities without performing active attacks or exploitation.

---

### 3. Browser DevTools — Header Inspection

```
Actions: Inspect HTTP headers → Check console warnings → Monitor network requests
```

> Identifies client-side security issues and server misconfigurations.

---

## 🔍 Technical Findings

### 🔴 Finding 1: Expired SSL Certificate

| Field | Details |
|---|---|
| **Type** | SSL Misconfiguration |
| **Risk** | High |

**Description:** The application uses an expired SSL certificate.  
**Evidence:** Browser displays "connection is not private" warning on `expired.badssl.com`.  
**Impact:** Loss of user trust; risk of man-in-the-middle attacks.  
**Remediation:** Renew SSL certificates before expiration; enable auto-renewal.

---

### 🔴 Finding 2: Self-Signed Certificate

| Field | Details |
|---|---|
| **Type** | SSL Misconfiguration |
| **Risk** | High |

**Description:** The application uses a self-signed certificate not issued by a trusted CA.  
**Evidence:** Browser shows certificate warning on `self-signed.badssl.com`.  
**Impact:** Not trusted by browsers; risk of spoofing.  
**Remediation:** Replace self-signed certificates with CA-issued certificates.

---

### 🟡 Finding 3: Mixed Content

| Field | Details |
|---|---|
| **Type** | Configuration Issue |
| **Risk** | Medium |

**Description:** HTTPS pages load resources over insecure HTTP.  
**Evidence:** Warnings visible in browser console on `mixed-content.badssl.com`.  
**Impact:** Data interception risk; breaks secure communication integrity.  
**Remediation:** Ensure all resources are loaded exclusively over HTTPS.

---

### 🟡 Finding 4: Missing Security Headers

| Field | Details |
|---|---|
| **Type** | Security Misconfiguration |
| **Risk** | Medium |

**Description:** Important HTTP security headers are missing or improperly configured.  
**Evidence:** HTTP response header inspection via DevTools revealed absence of `Content-Security-Policy`, `X-Frame-Options`, and `X-Content-Type-Options`.  
**Impact:** Vulnerable to XSS and clickjacking attacks.  
**Remediation:** Implement CSP, HSTS, X-Frame-Options, and X-Content-Type-Options headers.

---

### 🟡 Finding 5: Weak SSL/TLS Configuration

| Field | Details |
|---|---|
| **Type** | Cryptographic Issue |
| **Risk** | Medium |

**Description:** Outdated and insecure SSL/TLS protocol versions are supported.  
**Evidence:** Accessing TLS 1.0 and TLS 1.1 test pages on BadSSL triggered browser warnings indicating use of deprecated protocols.  
**Impact:** Weak encryption risks; susceptibility to protocol downgrade attacks.  
**Remediation:** Enforce TLS 1.2 or higher; disable TLS 1.0 and TLS 1.1.

---

## 📊 Impact Analysis

The identified vulnerabilities may allow attackers to:

- 🔓 Intercept sensitive information transmitted over the network
- 🕵️ Perform man-in-the-middle attacks via untrusted certificates
- 🔧 Exploit weak encryption protocols
- 🖱️ Compromise user trust through browser security warnings

---

## 📉 Risk Rating

| Severity | Description |
|---|---|
| 🔴 **High** | Critical vulnerability requiring immediate action |
| 🟡 **Medium** | Moderate risk requiring timely remediation |
| 🟢 **Low** | Minor issue with limited impact |

---

## 🛡️ Remediation Summary

| Action | Priority |
|---|---|
| Renew and automate SSL certificate renewal | High |
| Replace self-signed certs with CA-issued certificates | High |
| Enforce HTTPS for all page resources | Medium |
| Implement CSP, HSTS, and X-Frame-Options headers | Medium |
| Disable TLS 1.0 and TLS 1.1; enforce TLS 1.2+ | Medium |
| Regularly monitor and audit security configurations | Ongoing |

---

## ✅ Conclusion

The vulnerability assessment identified multiple high and medium-risk issues, primarily related to SSL/TLS configurations and security header practices. Although these vulnerabilities are demonstrated in a controlled environment on BadSSL, they accurately reflect real-world risks that organizations must proactively address.

This task enhanced practical understanding of security analysis, risk classification, and professional reporting in the context of web application security.

---

## 📚 References

| Resource | Link |
|---|---|
| OWASP Top 10 | https://owasp.org/www-project-top-ten/ |
| Nmap Documentation | https://nmap.org/docs.html |
| OWASP ZAP Documentation | https://www.zaproxy.org/docs/ |
| BadSSL | https://badssl.com |

---

> ⚠️ **Disclaimer:** This assessment was conducted entirely in a read-only and passive manner for educational purposes only. No exploitation was performed and no real or production systems were targeted or harmed.

---

<div align="center">

**Made with 🔐 by Kothamasu Sai Prasad**  
*Cyber Security Internship — Future Interns*

</div>
