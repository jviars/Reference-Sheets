# Cybersecurity Cheat Sheet

## Authentication & Access Control

### Password Security
- Minimum length: 12+ characters
- Complexity requirements: uppercase, lowercase, numbers, special characters
- Password hashing algorithms: Argon2id, bcrypt, PBKDF2
- Salt requirements: Unique per user, random, minimum 16 bytes
- Never store plaintext passwords
- Implement account lockout after failed attempts

### Multi-Factor Authentication (MFA)
- Time-based One-Time Password (TOTP)
- FIDO2/WebAuthn
- Hardware security keys
- Backup codes for recovery
- SMS as last resort only (vulnerable to SIM swapping)

### Session Management
- Generate cryptographically secure session IDs
- Invalidate sessions on logout
- Implement absolute and idle timeouts
- Secure session storage
- Set secure and HttpOnly cookie flags
- Implement CSRF tokens

## Network Security

### TLS/SSL Configuration
- Minimum TLS version: 1.2
- Recommended cipher suites:
  TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256
  TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
- Enable Perfect Forward Secrecy
- Implement HSTS
- Configure CAA DNS records

### Firewall Rules
- Default deny all
- Allow only necessary ports/services
- Implement rate limiting
- Log all denied traffic
- Regular rule review and updates
- Implement egress filtering

### Network Monitoring
- Enable IDS/IPS
- Log suspicious activities
- Monitor bandwidth usage
- Implement network segmentation
- Regular vulnerability scanning
- Configure alerts for anomalies

## Application Security

### Input Validation
- Validate on server side
- Whitelist allowed characters
- Use parameterized queries
- Encode output
- Validate file uploads
- Implement size limits

### API Security
- Use API keys/tokens
- Implement rate limiting
- Validate JWT tokens
- Use HTTPS only
- Implement proper error handling
- Version your APIs

### Security Headers
```
Strict-Transport-Security: max-age=31536000; includeSubDomains; preload
Content-Security-Policy: default-src 'self'
X-Frame-Options: DENY
X-Content-Type-Options: nosniff
Referrer-Policy: strict-origin-when-cross-origin
Permissions-Policy: geolocation=(), camera=()
```

## Incident Response

### Preparation
- Incident response plan
- Contact list
- System backups
- Documentation
- Regular drills
- Recovery procedures

### Detection
- Log monitoring
- Alert systems
- User reporting
- System monitoring
- Network monitoring
- File integrity checks

### Response Steps
1. Identify and confirm incident
2. Contain the breach
3. Eradicate the threat
4. Recover systems
5. Document everything
6. Post-incident analysis

## Data Protection

### Encryption
- Data at rest: AES-256
- Data in transit: TLS 1.2+
- Key management
- Regular key rotation
- Secure key storage
- Encryption at application layer

### Backup Strategy
- 3-2-1 Rule
  - 3 copies of data
  - 2 different media types
  - 1 offsite backup
- Regular testing
- Encryption of backups
- Access control
- Retention policy

## Compliance & Auditing

### Logging
- Authentication attempts
- System changes
- Security events
- Access to sensitive data
- Error messages
- Network traffic

### Audit Requirements
- Regular security assessments
- Penetration testing
- Vulnerability scanning
- Code review
- Access review
- Third-party audits

## Security Tools

### Network Security
- Wireshark
- Nmap
- Snort
- pfSense
- Metasploit
- Nessus

### Application Security
- OWASP ZAP
- Burp Suite
- Acunetix
- SonarQube
- GitGuardian
- Dependency Check

### System Security
- ClamAV
- OSSEC
- Fail2Ban
- SELinux/AppArmor
- Tripwire
- Lynis

## Best Practices

### System Hardening
- Disable unnecessary services
- Regular updates/patches
- Secure configurations
- Remove default accounts
- Implement least privilege
- Regular security scans

### Code Security
- Input validation
- Output encoding
- Error handling
- Access control
- Secure dependencies
- Code signing

### Security Culture
- Regular training
- Security awareness
- Incident reporting
- Clear policies
- Regular updates
- Security champions

## Regular Maintenance

### Daily Tasks
- Monitor logs
- Check alerts
- Verify backups
- Update threat intel
- Review access attempts
- System health checks

### Monthly Tasks
- Patch management
- Access review
- Policy updates
- Training updates
- Vulnerability scans
- Metrics review

### Quarterly Tasks
- Penetration testing
- Disaster recovery test
- Policy review
- Vendor assessment
- Compliance check
- Risk assessment
