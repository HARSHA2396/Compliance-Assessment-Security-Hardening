# Bring Your Own Device (BYOD) Policy

**Policy ID**: SEC-BYOD-001  
**Effective Date**: January 2026  
**Review Date**: January 2027  

---

## 1. Purpose

To establish secure guidelines for employees using personal devices to access organizational data, systems, and resources while protecting corporate information.

## 2. Scope

This policy applies to all employees, contractors, and authorized users accessing company resources via personal devices (smartphones, tablets, laptops, smartwatches).

## 3. Device Eligibility

### 3.1 Supported Platforms
- iOS 15+ (Apple iPhone/iPad)
- Android 11+ (Samsung, Google Pixel, OnePlus)
- Windows 10/11 (laptops/tablets)
- macOS 11+ (MacBooks)

### 3.2 Device Requirements
- **Operating System**: Current version with latest security patches
- **Encryption**: Full device encryption enabled
- **Screen Lock**: Strong password or biometric (minimum 6-digit PIN)
- **Security Software**: Antivirus/anti-malware installed and active
- **Device Registration**: MDM enrollment mandatory
- **Remote Wipe**: Enabled for lost/stolen device management

## 4. Access Control & Authentication

### 4.1 Multi-Factor Authentication
- MFA required: Email, VPN, critical applications
- Methods accepted: TOTP (Google Authenticator, Microsoft Authenticator), hardware tokens
- No SMS-only authentication for sensitive systems

### 4.2 VPN Requirements
- VPN mandatory for accessing corporate network or resources
- Approved VPN provider: Company-provided certificate
- Always-on VPN: Recommended for continuous protection
- VPN authentication: Must match corporate credentials

### 4.3 Device Management (MDM)
- Device enrollment: Mandatory before access
- Compliance check-in: Daily verification
- Device policies: Auto-enforced by MDM
- Removal from MDM: Immediate data wipe

### 4.4 Session Management
- Automatic logout: 15 minutes inactivity
- Session timeout: 8 hours maximum
- Concurrent sessions: Limited to 1 per user

## 5. Data Protection & Handling

### 5.1 Data Storage
- **Restricted**: No sensitive data stored locally on device
- **Approved**: Company cloud storage only (OneDrive, Teams, SharePoint)
- **Method**: Files downloaded only when necessary, deleted after use
- **Sync**: Only approved folders synchronized

### 5.2 Data Classification
- **Public data**: May be stored locally
- **Internal data**: Cloud storage only, no local storage
- **Confidential data**: Cloud storage with encryption, limited access
- **Restricted data**: Not permitted on personal devices

### 5.3 Backup & Recovery
- Device backup: Encrypted cloud backup only
- Corporate data backup: Daily automated backup
- Recovery: Company IT-managed only
- Deletion: Secure wipe procedure required

## 6. Application & Software Policy

### 6.1 Approved Applications
- Email: Outlook, Gmail (corporate account only)
- Productivity: Office 365, Teams, SharePoint
- VPN: Company-provided VPN client only
- Security: Company-approved antivirus/anti-malware

### 6.2 Prohibited Applications
- Root/jailbreak tools (Xposed, Cydia, etc.)
- Unauthorized file sharing apps
- Proxy/VPN services (except company VPN)
- Retail shopping or personal financial apps (security risk)
- Development tools that modify system

### 6.3 Application Updates
- Security updates: Install immediately
- Major OS updates: Within 30 days
- App updates: Within 60 days
- Enforcement: MDM non-compliance triggers access revocation

## 6. Network & Connectivity Security

### 6.1 Wi-Fi Usage
- **Public Wi-Fi**: ONLY with VPN enabled (mandatory)
- **Open networks**: Prohibited without VPN
- **Known networks**: Connect to company-managed networks only
- **Forget networks**: Remove insecure networks regularly

### 6.2 Bluetooth & NFC
- Bluetooth: Disabled when not in use
- Pairing: Only with trusted devices (personal headphones acceptable)
- NFC: Disabled for contactless payments

### 6.3 Mobile Hotspot
- Permitted: Using device hotspot for company work
- Security: WPA2 encryption minimum, 12+ character password
- Prohibited: Sharing with unauthorized users

## 7. Prohibited Activities

- ✗ Rooting/jailbreaking devices
- ✗ Using unauthorized applications
- ✗ Sharing credentials or access tokens
- ✗ Connecting to unsecured Wi-Fi without VPN
- ✗ Disabling security features (firewall, encryption, MDM)
- ✗ Installing unauthorized certificates
- ✗ Allowing others to use device
- ✗ Storing passwords in notes or unencrypted storage

## 8. Device Loss, Theft, or Compromise

### 8.1 Incident Response
- **Immediate**: Contact IT Security (within 1 hour)
- **Reporting**: Complete incident report within 24 hours
- **Device Action**: Remote wipe initiated by IT
- **Investigation**: Security team assesses data exposure

### 8.2 Notification
- Company notifies user of device wiping
- Access credentials reset
- Cloud accounts password reset
- Email notification of incident details

### 8.3 Recovery
- New device enrollment required
- Previous device marked as compromised
- Data recovery from cloud backup
- Security review before re-access

## 9. Monitoring & Compliance

### 9.1 Device Monitoring
- MDM continuous monitoring: Security posture verification
- Compliance check-in: Daily automated verification
- Device location: Not tracked by default
- Usage logs: Application access patterns logged

### 9.2 Compliance Audits
- Monthly compliance verification
- Quarterly device inventory audit
- Semi-annual policy compliance review
- Annual comprehensive security assessment

### 9.3 Auditing & Logging
- VPN access logs: 90-day retention
- Failed authentication: Logged and reviewed
- Data access logs: Cloudonly, company-managed
- MDM events: Retained for 1 year

## 10. User Responsibilities

- ✓ Maintain device security (patches, updates, lock screen)
- ✓ Enable and maintain all security features
- ✓ Use company VPN for all corporate access
- ✓ Report lost/stolen devices immediately
- ✓ Do not allow others to use device
- ✓ Comply with data classification standards
- ✓ Complete BYOD security training annually
- ✓ Cooperate with MDM management
- ✓ Do not install unauthorized applications

## 11. Company Responsibilities

- ✓ Provide VPN and approved applications
- ✓ Manage and support MDM platform
- ✓ Provide security training and documentation
- ✓ Respond to incidents within 2 hours
- ✓ Maintain data backups and recovery capabilities
- ✓ Conduct regular security audits
- ✓ Update policy based on emerging threats

## 12. Enforcement & Violations

| Violation | First Offense | Subsequent Offenses |
|---|---|---|
| Unauthorized app installation | Warning + removal | Access suspension |
| Disabled security features | Immediate remediation | Access revoked |
| Public Wi-Fi without VPN | Warning | 30-day suspension |
| Non-compliance with updates | Warning notice | Access revoked |
| Policy non-compliance | Warning | Disciplinary action |

## 13. Exception & Appeals

- Exceptions: Submit to CISO for review
- Approval: Business justification + risk assessment required
- Term: 90-day maximum, renewable with review
- Appeal: Contact Security Manager within 5 business days

## 14. Training & Acknowledgment

- **Mandatory Training**: All BYOD users annually
- **Content**: Security best practices, policy compliance, threat awareness
- **Acknowledgment**: User must sign policy agreement before access
- **Certification**: Training completion tracked by HR

---

**Approved By**: Chief Information Security Officer  
**Distribution**: All Staff (mandatory acknowledgment required)  
**Effective**: All new device enrollments must comply immediately
