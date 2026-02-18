# Remediation Steps Guide

**Purpose:** Detailed, step-by-step instructions for addressing identified vulnerabilities

**Target Audience:** Development & Operations Teams

---

## Template for Each Vulnerability Fix

### [Issue #1] - [Vulnerability Title]

**Severity Level:** [Critical/High/Medium/Low]

#### Problem Statement
[Clear description of the vulnerability and why it needs to be fixed]

#### Solution Overview
[High-level explanation of the fix approach]

#### Implementation Steps

**Step 1: [Preparation]**
- Action item 1
- Action item 2
```bash
# Example command if applicable
```

**Step 2: [Implementation]**
- Detailed instruction 1
- Detailed instruction 2
```
# Code example or configuration
```

**Step 3: [Testing]**
- How to verify the fix is working
- Expected results
```bash
# Test command or procedure
```

**Step 4: [Deployment]**
- How to roll out to production
- Rollback procedure if needed

#### Verification Checklist
- [ ] Issue has been fixed
- [ ] Testing completed successfully
- [ ] No new issues introduced
- [ ] Documentation updated
- [ ] Deployed to production

#### Additional Notes
- Estimated time to implement: [X hours]
- Potential impact on performance: [None/Low/Medium]
- Rollback complexity: [Simple/Moderate/Complex]

---

## Common Vulnerability Fixes

### Missing Security Headers

#### HTTP Strict-Transport-Security (HSTS)
```
Strict-Transport-Security: max-age=31536000; includeSubDomains; preload
```

#### Content-Security-Policy (CSP)
```
Content-Security-Policy: default-src 'self'; script-src 'self' 'unsafe-inline'; style-src 'self' 'unsafe-inline'
```

#### X-Content-Type-Options
```
X-Content-Type-Options: nosniff
```

#### X-Frame-Options
```
X-Frame-Options: DENY
```

#### X-XSS-Protection
```
X-XSS-Protection: 1; mode=block
```

#### Referrer-Policy
```
Referrer-Policy: strict-origin-when-cross-origin
```

**Implementation (Apache .htaccess):**
```apache
<IfModule mod_headers.c>
    Header always set Strict-Transport-Security "max-age=31536000; includeSubDomains; preload"
    Header always set Content-Security-Policy "default-src 'self'"
    Header always set X-Content-Type-Options "nosniff"
    Header always set X-Frame-Options "DENY"
    Header always set X-XSS-Protection "1; mode=block"
    Header always set Referrer-Policy "strict-origin-when-cross-origin"
</IfModule>
```

**Implementation (Nginx):**
```nginx
add_header Strict-Transport-Security "max-age=31536000; includeSubDomains; preload" always;
add_header Content-Security-Policy "default-src 'self'" always;
add_header X-Content-Type-Options "nosniff" always;
add_header X-Frame-Options "DENY" always;
add_header X-XSS-Protection "1; mode=block" always;
add_header Referrer-Policy "strict-origin-when-cross-origin" always;
```

### Outdated Dependencies

#### Node.js/npm Projects
```bash
# Check for outdated packages
npm outdated

# Update packages
npm update

# Check for security vulnerabilities
npm audit

# Fix vulnerabilities automatically
npm audit fix
```

#### Python Projects
```bash
# Check outdated packages
pip list --outdated

# Update all packages
pip install --upgrade pip

# Use requirements.txt for version management
pip install -r requirements.txt --upgrade
```

### Missing Cookie Attributes

**Secure Flag:**
```javascript
// Set HTTPS-only cookies
Set-Cookie: sessionid=abc123; Secure; HttpOnly; SameSite=Lax
```

**Implementation in Node.js/Express:**
```javascript
app.use(session({
    secret: 'your-secret',
    resave: false,
    saveUninitialized: true,
    cookie: {
        secure: true,    // HTTPS only
        httpOnly: true,  // No JavaScript access
        sameSite: 'lax'  // CSRF protection
    }
}));
```

### Input Validation Issues

**Example: Form Input Validation**

```javascript
// Client-side validation (in addition to server-side)
function validateEmail(email) {
    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    return emailRegex.test(email);
}

// Server-side validation (Critical!)
function sanitizeInput(input) {
    return input.trim().replace(/[<>\"']/g, '');
}
```

### Authentication/Authorization Hardening

#### Password Policy
- Minimum 12 characters
- Mix of uppercase, lowercase, numbers, symbols
- No dictionary words or personal information
- Regular change requirements (90 days)

#### Multi-Factor Authentication (MFA)
```javascript
// TOTP (Time-based One-Time Password) example using speakeasy
const speakeasy = require('speakeasy');

const secret = speakeasy.generateSecret({
    name: 'Your App'
});

// Verify code
const verified = speakeasy.totp.verify({
    secret: secret.base32,
    encoding: 'base32',
    token: userProvidedToken
});
```

---

## Prioritization & Timeline

### Immediate (24-48 hours)
- Critical vulnerabilities
- Active exploitation risk

### Short-term (1-2 weeks)
- High-severity issues
- Medium visibility vulnerabilities

### Medium-term (1 month)
- Medium-severity issues
- Configuration improvements

### Long-term (Ongoing)
- Low-severity issues
- Security enhancements
- Monitoring setup

---

## Testing & Validation

### Post-Remediation Testing Checklist

- [ ] Vulnerability has been fixed
- [ ] No errors in application logs
- [ ] No impact on functionality
- [ ] Performance remains acceptable
- [ ] No new vulnerabilities introduced
- [ ] Backup/rollback plan validated

### Re-assessment

After implementing all remediation steps, conduct a follow-up assessment using the same tools:
1. Re-run OWASP ZAP passive scan
2. Re-check security headers with Nmap
3. Review browser DevTools for client-side issues

---

## Support & Questions

For issues during remediation:
1. Refer to tool documentation
2. Consult security team
3. Document any obstacles encountered

---

**Last Updated:** February 2026
