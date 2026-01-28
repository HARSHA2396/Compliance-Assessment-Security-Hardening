# NIST SP 800-53 Rev.5 Compliance Assessment – Windows 10/11

## Overview
This assessment maps Windows 10/11 hardening controls to **NIST SP 800-53 Revision 5** security requirements. The evaluation includes compliance status, implementation evidence, and remediation plans.

## Compliance Control Matrix

### Access Control (AC) Family

| Control ID | Control Name | Requirement | Implementation | Status | Evidence |
|-----------|--------------|-------------|-----------------|--------|----------|
| **AC-2** | Account Management | Manage system accounts and access rights | Guest account disabled, named admin accounts with complex passwords, regular access reviews | **MET** | Computer Management |
| **AC-2(1)** | Automated Account Management | Implement automated account lifecycle | Account creation via domain policy only | **MET** | Group Policy |
| **AC-3** | Access Enforcement | Enforce access control policies | NTFS file permissions, registry ACLs configured | **MET** | File Properties |
| **AC-6** | Least Privilege | Limit privileges to minimum necessary | Users in standard group, admin only when needed | **MET** | User Groups |
| **AC-7** | Unsuccessful Login Attempts | Restrict failed login attempts | Account lockout: 5 attempts, 30-minute duration | **MET** | Security Policy |
| **AC-11** | Session Lock | Lock device when unattended | Screen lock: Immediate | **MET** | Control Panel |

### Identification and Authentication (IA) Family

| Control ID | Control Name | Requirement | Implementation | Status | Evidence |
|-----------|--------------|-------------|-----------------|--------|----------|
| **IA-2** | Authentication | Authenticate users before access | Windows login required, NLA enabled for RDP | **MET** | Security Options |
| **IA-2(1)** | Multi-Factor Authentication | Require MFA for remote access | RDP requires NLA + smart card capability enabled | **PARTIAL** | RDP Settings |
| **IA-5** | Authenticator Management | Manage authentication credentials | Password policy: 12+ chars, 24 history, 60-day max age | **MET** | Password Policy |
| **IA-5(1)** | Password-based Authentication | Enforce password strength | Meets requirement: length 12+, mixed case, numbers, symbols | **MET** | Group Policy |

### System and Communications Protection (SC) Family

| Control ID | Control Name | Requirement | Implementation | Status | Evidence |
|-----------|--------------|-------------|-----------------|--------|----------|
| **SC-7** | Boundary Protection | Implement firewall | Windows Firewall enabled (all profiles), inbound default=block | **MET** | firewall-enabled.png |
| **SC-7(5)** | Managed Interfaces | Manage physical/logical interfaces | USB restrictions via policy | **MET** | Device Policy |
| **SC-28** | Protection of Data at Rest | Encrypt sensitive data | BitLocker full-disk encryption, XTS-AES 128-bit | **MET** | bitlocker-enabled.png |
| **SC-28(1)** | Cryptographic Protection | Use FIPS-validated algorithms | BitLocker AES encryption, TLS 1.2+ for network | **MET** | BitLocker Status |

### System and Information Integrity (SI) Family

| Control ID | Control Name | Requirement | Implementation | Status | Evidence |
|-----------|--------------|-------------|-----------------|--------|----------|
| **SI-2** | Flaw Remediation | Apply patches & updates | Automatic Windows Updates enabled, monthly patching verified | **MET** | Update History |
| **SI-3** | Malicious Code Protection | Deploy antivirus/anti-malware | Windows Defender enabled, real-time protection active | **MET** | defender-active.png |
| **SI-4** | Information System Monitoring | Monitor system events | Audit logging enabled, Event Log retention 90 days | **MET** | Event Viewer |
| **SI-7** | Software, Firmware, Integrity | Verify system integrity | File Integrity Monitoring enabled | **MET** | System File Checker |

### Audit and Accountability (AU) Family

| Control ID | Control Name | Requirement | Implementation | Status | Evidence |
|-----------|--------------|-------------|-----------------|--------|----------|
| **AU-2** | Audit Events | Audit critical events | Audit policy: logons, privilege use, object access | **MET** | auditpol output |
| **AU-2(a)** | Logon Events | Log user authentication | Audit logon events enabled (success & failure) | **MET** | Event ID 4624, 4625 |
| **AU-3** | Content of Audit Records | Include required fields | Event records include: User, Time, Event, Result | **MET** | Event Viewer |
| **AU-6** | Audit Review | Review audit logs regularly | Weekly manual review, automated alerts for critical events | **PARTIAL** | Event Log Review |

---

## Compliance Summary by Family

| Control Family | Total Controls | Compliant | Partial | Non-Compliant | Status |
|----------------|----------------|-----------|---------|---------------|--------|
| Access Control (AC) | 6 | 6 | 0 | 0 | ✅ 100% |
| Identification & Auth (IA) | 4 | 3 | 1 | 0 | ⚠️ 75% |
| System & Comm. Prot. (SC) | 4 | 4 | 0 | 0 | ✅ 100% |
| System & Info. Integrity (SI) | 4 | 4 | 0 | 0 | ✅ 100% |
| Audit & Accountability (AU) | 4 | 3 | 1 | 0 | ⚠️ 75% |
| **OVERALL** | **22** | **20** | **2** | **0** | **⚠️ 91%** |

---

## Remediation Plan (Partial Compliance)

### IA-2(1): Multi-Factor Authentication
**Current Status**: RDP supports NLA + smart card, but not enforced  
**Remediation**:
- [ ] Enforce smart card authentication for RDP
- [ ] Implement TOTP for VPN (if applicable)
- [ ] Test MFA with pilot user group
- [ ] Roll out enterprise-wide within 60 days

**Timeline**: 60 days  
**Owner**: Identity & Access Management Team

### AU-6: Audit Review
**Current Status**: Manual review only  
**Remediation**:
- [ ] Deploy SIEM (Splunk, ELK, Sentinel)
- [ ] Configure automated alerts for Event IDs: 4625, 4720, 4728
- [ ] Establish daily log review workflow
- [ ] Generate monthly compliance report

**Timeline**: 90 days  
**Owner**: Security Operations Center

---

## Implementation Evidence

**Screenshot Evidence Location**: `01-Hardening/Windows/screenshots/`

1. `firewall-enabled.png` – Windows Defender Firewall (all profiles)
2. `defender-active.png` – Windows Defender Real-Time Protection
3. `bitlocker-enabled.png` – BitLocker encryption status
4. `password-policy.png` – Password policy configuration

---

## Tools & Methods Used

- **Group Policy Editor** (gpedit.msc) – Policy verification
- **Local Security Policy** (secpol.msc) – Account/audit policy review
- **Event Viewer** – Audit log review
- **PowerShell** – Automated compliance checks
- **BitLocker Management** – Encryption verification
- **Windows Security Center** – Malware/firewall status

---

## Related Documents
- [Windows 10/11 Hardening Assessment](../01-Hardening/Windows/windows-hardening.md)
- [Evidence Documentation](evidence/windows/)
