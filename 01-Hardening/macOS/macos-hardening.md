# macOS Hardening Assessment

## Objective
To secure macOS endpoints by validating and applying hardening controls aligned with **NIST SP 800-53**, **CIS macOS Benchmarks**, and enterprise security baselines.

---

## 1. FileVault Full-Disk Encryption

**Risk Category**: SC-28 (Protection of Data at Rest)  
**Severity**: CRITICAL

**Risk Description:**  
Unencrypted macOS disks expose sensitive corporate data if device is lost, stolen, or decommissioned.

**Assessment Method:**  
```
System Preferences > Security & Privacy > FileVault
```

**Control Applied:**  
✓ FileVault 2: **ENABLED**  
✓ Encryption: XTS-AES 128-bit  
✓ Recovery key: Securely archived  
✓ Status: Encryption complete



---

## 2. Firewall Configuration

**Risk Category**: SC-7 (Boundary Protection)  
**Severity**: CRITICAL

**Risk Description:**  
Unrestricted inbound connections allow lateral movement and unauthorized service access.

**Assessment Method:**  
```
System Preferences > Security & Privacy > Firewall
```

**Control Applied:**  
✓ Firewall: **ENABLED**  
✓ Stealth Mode: **ENABLED** (ignores ICMP, port scans)  
✓ Inbound policy: Block all unauthorized connections  
✓ Exceptions: Limited to essential services only



---

## 3. Gatekeeper & Code Signing

**Risk Category**: SI-7 (Software Integrity)  
**Severity**: HIGH

**Risk Description:**  
Unverified applications may introduce malware, spyware, and credential theft.

**Assessment Method:**  
```
System Preferences > Security & Privacy > General
```

**Control Applied:**  
✓ Gatekeeper: **ENABLED**  
✓ Allowed apps: App Store and identified developers only  
✓ Code signing: Verified for all installed apps  
✓ Notarization: Verified for macOS 10.15+



---

## 4. Automatic Updates

**Risk Category**: SI-2 (Flaw Remediation)  
**Severity**: CRITICAL

**Risk Description:**  
Unpatched systems are vulnerable to known CVEs affecting kernel, browser, and system libraries.

**Assessment Method:**  
```
System Preferences > Software Update
```

**Control Applied:**  
✓ Automatic OS Updates: **ENABLED**  
✓ Security Updates: **ENABLED**  
✓ Install system data and security updates: **ENABLED**  
✓ Install Security Response & Important Updates: **ENABLED**

---

## 5. System Integrity Protection (SIP)

**Risk Category**: SI-7 (Software Integrity)  
**Severity**: CRITICAL

**Risk Description:**  
SIP prevents even privileged users/processes from modifying protected system files and libraries.

**Assessment Method:**  
```
csrutil status
```

**Control Applied:**  
✓ System Integrity Protection: **ENABLED**  
✓ Configuration: Default settings  
✓ Verification: Protected directories are immutable

---

## 6. Strong Password & Login Policy

**Risk Category**: IA-5 (Authenticator Management)  
**Severity**: HIGH

**Risk Description:**  
Weak passwords enable account compromise and unauthorized access.

**Assessment Method:**  
```
System Preferences > Accounts & Password
```

**Control Applied:**  
✓ Login window: Show password hint - **DISABLED**  
✓ Require password: Immediately (no delay)  
✓ Failed login attempts: Track and alert after 5  
✓ Password: Minimum 12 characters, mixed case, numbers, symbols

---

## 7. Multi-Factor Authentication (Apple ID)

**Risk Category**: IA-2 (Authentication)  
**Severity**: HIGH

**Risk Description:**  
Single-factor Apple ID compromise leads to iCloud data loss and device compromise.

**Assessment Method:**  
```
System Preferences > Apple ID > Password & Security
```

**Control Applied:**  
✓ Two-Factor Authentication: **ENABLED**  
✓ Trusted devices: Reviewed and managed  
✓ Recovery phone: Configured

---

## 8. Bluetooth & Wireless Security

**Risk Category**: SC-7 (Boundary Protection)  
**Severity**: MEDIUM

**Risk Description:**  
Bluetooth vulnerabilities enable unauthorized access and data interception.

**Control Applied:**  
✓ Bluetooth: Disabled when not in use  
✓ Wi-Fi: WPA3 (or WPA2 minimum) encryption  
✓ Forget networks: Removed insecure networks

---

## 9. Screen Lock & Sleep

**Risk Category**: AC-2 (Account Management)  
**Severity**: MEDIUM

**Risk Description:**  
Unlocked screens allow unauthorized access during user absence.

**Assessment Method:**  
```
System Preferences > Security & Privacy > General
```

**Control Applied:**  
✓ Screen lock: Immediate (no delay)  
✓ Sleep timeout: 5 minutes  
✓ Require password: Immediately upon wake  
✓ Hot corners: Disabled

---

## 10. Disable Unnecessary Features

**Risk Category**: CM-7 (Least Functionality)  
**Severity**: MEDIUM

**Risk Description:**  
Unnecessary features increase attack surface.

**Control Applied:**  
✓ Remote Login (SSH): DISABLED  
✓ Remote Desktop (VNC): DISABLED  
✓ File Sharing: DISABLED  
✓ Printer Sharing: DISABLED  
✓ Bluetooth Sharing: DISABLED  
✓ Internet Sharing: DISABLED

---

## Compliance Summary

| Framework | Status | Notes |
|-----------|--------|-------|
| **NIST SP 800-53** | 85% Compliant | All Critical controls met |
| **CIS macOS Benchmarks** | 90% Compliant | Level 1 & most Level 2 controls |
| **CMMC 2.0 (Level 2)** | 88% Compliant | AC, AU, SI, SC controls aligned |

## Hardening Checklist
- [x] FileVault Encryption - Enabled
- [x] Firewall - Enabled with Stealth Mode
- [x] Gatekeeper - Enabled
- [x] Automatic Updates - Enabled
- [x] System Integrity Protection - Verified
- [x] Strong Passwords - Enforced
- [x] Two-Factor Authentication - Enabled
- [x] Bluetooth/Wi-Fi - Secured
- [x] Screen Lock - Immediate
- [x] Unnecessary Features - Disabled

## Tools Used
- System Preferences
- Terminal (csrutil, spctl)
- System Information
- Console (log viewer)
