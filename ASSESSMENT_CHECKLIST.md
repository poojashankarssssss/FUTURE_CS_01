# Assessment Checklist & Quick Reference

Quick reference guide for conducting the vulnerability assessment using Nmap, OWASP ZAP, and Browser DevTools.

---

## Pre-Assessment Checklist

### Preparation
- [ ] Obtain written authorization to test the target website
- [ ] Define scope and boundaries
- [ ] Document target website information
- [ ] Identify stakeholders and approval contacts
- [ ] Set assessment timeline

### Tools Setup
- [ ] Nmap installed and functioning
  ```bash
  nmap --version
  ```
- [ ] OWASP ZAP installed and updated
  - Version: [____________]
- [ ] Browser DevTools accessible
  - Browser: [Chrome / Firefox / Edge / Safari]
- [ ] Text editor/IDE ready for documentation
- [ ] Screenshot tool available (Snagit, ShareX, or built-in)

### Environment
- [ ] Dedicated testing environment/machine
- [ ] Internet connection stable
- [ ] No VPN/proxy interference (for Nmap)
- [ ] Firewall rules not blocking assessment traffic

---

## Assessment Execution Checklist

### Phase 1: Reconnaissance

#### Network Reconnaissance (Nmap)
- [ ] **Basic Service Discovery**
  ```bash
  nmap -sV target-domain.com
  ```
  - [ ] Document open ports
  - [ ] Note running services
  - [ ] Record service versions
  - [ ] Screenshot results

- [ ] **OS Detection**
  ```bash
  nmap -O target-domain.com
  ```
  - [ ] Document OS information
  - [ ] Note any detected vulnerabilities

- [ ] **Full Port Scan (Optional)**
  ```bash
  nmap -p- target-domain.com
  ```
  - [ ] Check for non-standard ports
  - [ ] Record any interesting findings

#### Browser-Based Reconnaissance
- [ ] **Navigate Target Website**
  - [ ] Open browser DevTools (F12)
  - [ ] Open Network tab
  - [ ] Navigate to target domain
  - [ ] Note HTTPS vs HTTP usage
  - [ ] Screenshot home page

- [ ] **Document Framework/Technology**
  - [ ] Use OWASP ZAP to detect technologies
  - [ ] Check server headers with DevTools
  - [ ] Note framework/CMS information
  - [ ] Document technology stack

### Phase 2: Web Application Scanning

#### OWASP ZAP Configuration
- [ ] Launch OWASP ZAP
- [ ] Set to Passive Mode
  - Menu: Tools → Options
  - Select Passive Scan category
  - Disable active scanning plugins
- [ ] Configure browser proxy (if needed)
  - Address: 127.0.0.1
  - Port: 8080
- [ ] Clear previous scan data (if any)

#### Passive Vulnerability Scanning
- [ ] **Start Passive Scan**
  - [ ] Navigate to each page of target website
  - [ ] Visit main pages
  - [ ] Visit forms/input pages
  - [ ] Visit authentication pages (if accessible)
  - [ ] Allow ZAP to analyze responses
  - [ ] Browse for at least 10-15 minutes

- [ ] **Review ZAP Findings**
  - [ ] Check Alerts tab
  - [ ] Click on each finding
  - [ ] Review description
  - [ ] Note severity levels
  - [ ] Screenshot each finding

#### Security Headers Analysis
- [ ] **Check Missing Headers in ZAP**
  - [ ] Strict-Transport-Security (HSTS)
  - [ ] Content-Security-Policy (CSP)
  - [ ] X-Frame-Options
  - [ ] X-Content-Type-Options
  - [ ] X-XSS-Protection
  - [ ] Referrer-Policy
  - [ ] Permissions-Policy

- [ ] **Manual Header Verification**
  ```bash
  # Linux/macOS
  curl -I https://target-domain.com
  
  # Check headers in browser DevTools
  # Network tab → Click any request → Headers tab
  ```
  - [ ] Document actual header values
  - [ ] Compare with security best practices
  - [ ] Screenshot findings

### Phase 3: Client-Side Analysis

#### JavaScript & Source Code Review
- [ ] **Open Browser DevTools (F12)**
- [ ] **Sources Tab**
  - [ ] Review application.js files
  - [ ] Look for hardcoded credentials
  - [ ] Check for exposed API endpoints
  - [ ] Review authentication logic
  - [ ] Screenshot suspicious findings

#### Console Analysis
- [ ] **Console Tab**
  - [ ] Note any JavaScript errors
  - [ ] Look for debug information
  - [ ] Check for error messages revealing structure
  - [ ] Review API calls in network activity
  - [ ] Screenshot errors/warnings

#### Storage Analysis
- [ ] **Application/Storage Tab**
  - [ ] **Cookies**
    - [ ] Check Secure flag
    - [ ] Check HttpOnly flag
    - [ ] Check SameSite attribute
    - [ ] Look for session tokens in plain text
    - [ ] Screenshot cookie settings
  
  - [ ] **Local Storage**
    - [ ] Check for sensitive data
    - [ ] Look for tokens/credentials
    - [ ] Note any PII stored
    - [ ] Screenshot findings
  
  - [ ] **Session Storage**
    - [ ] Check content
    - [ ] Look for sensitive information
    - [ ] Screenshot if relevant

#### Network Analysis
- [ ] **Network Tab**
  - [ ] Reload page to capture all requests
  - [ ] Filter by XHR/Fetch requests
  - [ ] Check for HTTPS on all requests
  - [ ] Look for sensitive data in URLs
  - [ ] Review authentication headers
  - [ ] Check response headers for security info
  - [ ] Screenshot API requests

---

## Vulnerability Classification

### As You Identify Issues, Classify Them:

#### Information Disclosure
- [ ] Server version information exposed
- [ ] Framework/CMS details visible
- [ ] API endpoints in JavaScript
- [ ] Internal IP addresses revealed
- [ ] Directory listing enabled

#### Security Misconfiguration
- [ ] Missing security headers
- [ ] Default credentials exposed
- [ ] Debug modes enabled
- [ ] Outdated software versions
- [ ] Unnecessary services running

#### Authentication Issues
- [ ] Weak password requirements
- [ ] No MFA/2FA available
- [ ] Session tokens in cookies without HttpOnly
- [ ] Password reset vulnerabilities
- [ ] Account lockout absent

#### Input Validation
- [ ] Forms accepting raw input
- [ ] No client-side validation
- [ ] Search functionality suspicious
- [ ] File upload vulnerabilities
- [ ] Parameter tampering possible

---

## Documentation During Assessment

### For Each Finding, Document:

**Quick Log Template:**
```
Date/Time: [MM/DD/YYYY HH:MM]
Tool: [Nmap / ZAP / DevTools]
Finding: [Brief title]
Severity: [Critical / High / Medium / Low]
Location: [URL / Parameter / Header]
Details: [Key information]
Evidence: [Screenshot / Output file]
```

### Create Folders for Evidence:
```
assets/
├── screenshots/
│   ├── 2026-02-18_header-missing-csp.png
│   ├── 2026-02-18_nmap-scan.png
│   └── 2026-02-18_zap-findings.png
├── nmap-output/
│   └── nmap-scan-2026-02-18.txt
└── zaproxy-reports/
    └── zap-report-2026-02-18.html
```

---

## Post-Assessment Checklist

### Analysis
- [ ] Review all collected findings
- [ ] Remove duplicate findings
- [ ] Verify each finding independently
- [ ] Assign CVSS scores
- [ ] Categorize by OWASP Top 10
- [ ] Verify false positives

### Documentation
- [ ] Complete VULNERABILITY_REPORT.md
- [ ] Create executive summary
- [ ] Develop remediation steps
- [ ] Verify all findings have evidence
- [ ] Proofread all documents

### Reporting
- [ ] Generate ZAP HTML report
  - [ ] Tools → Generate Report
  - [ ] Save to `assets/zaproxy-reports/`
  
- [ ] Save Nmap output
  ```bash
  nmap -sV target-domain.com > assets/nmap-output/scan.txt
  ```

- [ ] Compile all findings in FINDINGS_TRACKER.md
- [ ] Create professional summary documents
- [ ] Organize assets folder

### Delivery
- [ ] Review final report
- [ ] Get approval from stakeholder
- [ ] Commit to GitHub repository
- [ ] Share appropriate documents with client
- [ ] Schedule follow-up assessment

---

## Common Commands Reference

### Nmap
```bash
# Basic service detection
nmap -sV target.com

# Service detection + OS detection
nmap -A target.com

# Aggressive scan on specific ports
nmap -p 80,443 -A target.com

# Save output to file
nmap -sV target.com > output.txt

# Service version intensive
nmap -sV --version-intensity 9 target.com
```

### Curl (For Header Checking)
```bash
# Simply check response headers
curl -I https://target.com

# Follow redirects
curl -IL https://target.com

# Show all response headers
curl -i https://target.com

# Check specific header
curl -I https://target.com | grep -i "Content-Security-Policy"
```

### OWASP ZAP
1. Start ZAP
2. Set mode: Passive
3. Tools → Options → Passive Scan
4. Navigate to target in browser
5. Review Alerts tab
6. Export report: Tools → Generate Report

---

## Quick Severity Reference

| Severity | CVSS Score | Action Timeline | Example |
|----------|-----------|-----------------|---------|
| Critical | 9.0-10.0 | 24-48 hours | Remote code execution |
| High | 7.0-8.9 | 1-2 weeks | SQL injection |
| Medium | 4.0-6.9 | 1 month | XSS vulnerability |
| Low | 0.1-3.9 | Next cycle | Information disclosure |

---

## Important Notes

### What NOT to Do:
- ❌ Do NOT test without written permission
- ❌ Do NOT attempt to exploit vulnerabilities actively
- ❌ Do NOT access other users' data
- ❌ Do NOT modify any data
- ❌ Do NOT test beyond authorized scope
- ❌ Do NOT disclose vulnerabilities publicly

### What TO Do:
- ✅ Document everything thoroughly
- ✅ Take screenshots of evidence
- ✅ Keep detailed notes
- ✅ Stay within authorized scope
- ✅ Communicate with stakeholders
- ✅ Follow responsible disclosure

---

## Troubleshooting

### Nmap Issues
- **"Permission denied"**: Run with `sudo` (Linux/macOS)
- **No response**: Check firewall, try `-Pn` flag
- **Too slow**: Reduce port range with `-p` flag

### OWASP ZAP Issues
- **Scanning not working**: Check proxy configuration
- **Too many false positives**: Review alert thresholds
- **Memory issues**: Close other applications

### Browser DevTools Issues
- **Console not showing**: Press Ctrl+Shift+J (Windows) or Cmd+Option+J (Mac)
- **Storage not visible**: Check browser privacy settings
- **Network not capturing**: Make sure recorder is on

---

## Resources

- OWASP ZAP Documentation: https://www.zaproxy.org/docs/
- Nmap Manual: https://nmap.org/book/
- Browser DevTools: https://developer.chrome.com/docs/devtools/
- CVSS Calculator: https://www.first.org/cvss/calculator/3.1
- CWE/OWASP Top 10: https://owasp.org/Top10/

---

**Last Updated**: February 2026

