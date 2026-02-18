# Assessment Evidence - Screenshots Guide

This folder contains visual evidence from the vulnerability assessment tools. Below is a description of the screenshot evidence that would be included:

## Screenshots That Should Be Captured

### 1. Nmap Service Discovery Output
**File:** `nmap-scan-results.png`
**What it shows:** 
- Port scan results showing open ports (22, 80, 443)
- Service versions detected (Apache 2.4.41, PHP 7.4.3)
- Server information disclosure
**Where to get:** Run `nmap -sV example.com` in terminal and screenshot output

### 2. OWASP ZAP Findings - Alerts Tab
**File:** `zap-alerts-critical.png`
**What it shows:**
- Critical alert for missing CSP header
- High alert for HSTS missing
- List of all vulnerabilities ranked by severity
**Where to get:** OWASP ZAP → Sites tab → example.com → Alerts tab

### 3. Browser DevTools - Network Tab (Headers)
**File:** `devtools-response-headers.png`
**What it shows:**
- HTTP response headers for the website
- Missing security headers clearly visible:
  - No Content-Security-Policy
  - No Strict-Transport-Security
  - No X-Frame-Options
  - Missing X-Content-Type-Options
**Where to get:** Browser F12 → Network tab → Click request → Headers

### 4. Browser DevTools - Sources Tab
**File:** `devtools-jquery-version.png`
**What it shows:**
- jQuery 3.5.1 library loaded in sources
- Script file reference showing outdated version
**Where to get:** Browser F12 → Sources tab → Static scripts

### 5. Browser DevTools - Application Tab (Cookies)
**File:** `devtools-cookies-security.png`
**What it shows:**
- Sessionid cookie properties
- Missing HttpOnly flag highlighted
- Missing Secure flag
- Missing SameSite attribute
**Where to get:** Browser F12 → Application tab → Cookies section

### 6. Browser Console - Security Messages
**File:** `devtools-console-warnings.png`
**What it shows:**
- Browser console warnings about security issues
- CSP violation examples (if any)
- HTTPS mixed content warnings
**Where to get:** Browser F12 → Console tab (reload page to capture)

### 7. OWASP ZAP - Report Generation
**File:** `zap-report-generation.png`
**What it shows:**
- ZAP Report generation dialog
- Selected report format and options
- Scan summary being exported
**Where to get:** OWASP ZAP → Tools → Generate Report

### 8. Curl Command - HTTP Headers
**File:** `curl-headers-output.png`
**What it shows:**
- Terminal output showing `curl -i` response
- All HTTP response headers
- Missing security headers
**Where to get:** Terminal → `curl -I https://example.com` or `curl -i https://example.com`

---

## How to Capture These Screenshots

### On Windows (Built-in Screenshot Tool)
```powershell
# Use Windows Key + Shift + S for snipping tool
# Or Print Screen for full screen
# Then paste into Paint and save as PNG
```

### On Windows (Using Browser DevTools)
1. Press F12 to open DevTools
2. Press Ctrl+Shift+P to open command palette
3. Type "screenshot" to find screenshot command
4. Select "Capture screenshot" or "Capture full page screenshot"

### On Windows (Using Terminal)
```powershell
# Take screenshot of current window
$path = "C:\Users\HP\Desktop\cyber\task1\assets\screenshots"
Get-ChildItem -Path $path  # Create if needed
```

---

## Screenshot Organization

All screenshots should be named consistently:
```
zap-findings-critical-[date].png
zap-findings-high-[date].png
nmap-scan-[date].png
devtools-headers-[date].png
devtools-cookies-[date].png
devtools-console-[date].png
zap-report-[date].png
```

Example:
- `zap-findings-critical-2026-02-18.png`
- `nmap-scan-2026-02-18.png`
- `devtools-response-headers-2026-02-18.png`

---

## Evidence Linking in Report

In [VULNERABILITY_REPORT.md](../../VULNERABILITY_REPORT.md), reference screenshots like this:

```markdown
#### Proof of Concept
- Screenshot: Missing CSP header in response - [zap-findings-critical-2026-02-18.png](../screenshots/zap-findings-critical-2026-02-18.png)
- Screenshot: Browser DevTools showing lack of security headers - [devtools-headers-2026-02-18.png](../screenshots/devtools-headers-2026-02-18.png)
```

---

## Tool Screenshots That Are Essential

1. **Nmap Output** - Proves port/service discovery  
   ✅ Essential for credibility

2. **OWASP ZAP Alerts** - Shows automated scanning  
   ✅ Essential - proves tool usage

3. **Browser DevTools Headers** - Shows missing security headers  
   ✅ Essential - visual proof of findings

4. **Browser Console** - Shows security warnings  
   ✅ Helpful - additional evidence

5. **Curl/Terminal Output** - Verifies findings via CLI  
   ✅ Helpful - alternative verification

6. **ZAP Report** - Formal output document  
   ✅ Helpful - professional presentation

---

## Privacy & Sensitive Information

When taking screenshots:
- ❌ Do NOT include sensitive company information
- ❌ Do NOT screenshot real user data
- ❌ Do NOT include API keys or credentials
- ❌ DO blur/redact personal identifying information
- ✅ DO use example.com or test domain
- ✅ DO include tool names and findings clearly

---

## Portfolio Presentation

For LinkedIn/GitHub, these screenshots demonstrate:
- 📸 Technical tool proficiency (Nmap, OWASP ZAP, Browser DevTools)
- 📊 Ability to identify real vulnerabilities
- 📋 Professional assessment skills
- 🔍 Attention to detail in security

---

**Screenshots should be taken during actual assessment execution and referenced in all findings documentation.**

