# Windows Server Build Sheet - Enterprise Hardening

**Document ID**: WSS-001  
**Applicable Versions**: Windows Server 2019, 2022, 2024  
**Environment**: Production Cloud & On-Premises  
**Last Updated**: January 2026  

---

## 1. Infrastructure Overview

### 1.1 Supported Platforms
- Azure VMs (Standard_B2s or larger)
- AWS EC2 (t3.medium or larger)
- On-premises Hyper-V/VMware
- AWS Outposts (hybrid scenarios)

### 1.2 Hardware Specifications

| Requirement | Minimum | Recommended | Production |
|---|---|---|---|
| **Processor** | 2.0 GHz 64-bit (2 vCPU) | 2.4 GHz 64-bit (4 vCPU) | 3.0 GHz 64-bit (8+ vCPU) |
| **RAM** | 2 GB | 8 GB | 16-32 GB |
| **Storage** | 32 GB | 64 GB (SSD) | 256+ GB (NVMe SSD) |
| **Network** | Gigabit (1 Gbps) | 10 Gbps recommended | 10+ Gbps |
| **IOPS** | 3000 | 5000+ | 10000+ |

### 1.3 Operating System
- **Supported**: Windows Server 2019 Core/Desktop, Server 2022 Core/Desktop, Server 2024
- **Recommended**: Core for production (reduced attack surface)
- **Licensing**: Enterprise + Software Assurance (bulk licensing)
- **Updates**: Bi-monthly Patch Tuesday + monthly rollups

---

## 2. Pre-Deployment Configuration

### 2.1 Network Architecture
- **Isolation**: Separate VLAN for production servers
- **Access**: Bastion host / Jump box for administrative access
- **Firewall**: Network Security Groups (NSG) / Security Groups configured
- **Load Balancer**: Azure LB or AWS ALB for HA
- **NAT**: Outbound traffic routed through NATgateway/NAT instance

### 2.2 Storage Configuration
- **OS Drive (C:)**: BitLocker-encrypted
- **Data Drive (D:)**: Separate volume for logs/data
- **Backup**: Daily automated snapshots with 30-day retention
- **Replication**: Geo-redundant storage enabled

### 2.3 Monitoring Setup
- **Agent**: Azure Monitor Agent or AWS Systems Manager
- **Logging**: Diagnostic storage account configured
- **Alerts**: CPU >80%, Memory >75%, Disk >85% thresholds
- **Dashboard**: Central monitoring dashboard created

---

## 3. Operating System Hardening

### 3.1 Windows Updates & Patching
- **Automatic Updates**: Enabled and configured for maintenance window (2 AM UTC)
- **Update Type**: Critical + Security patches (monthly)
- **Quality Updates**: Installed within 48 hours of release
- **Patch Testing**: Validated in pre-prod before production deployment
- **WSUS Server**: Centralized WSUS for large deployments

**Configuration**:
```powershell
Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU" -Name "AUOptions" -Value 4
```

### 3.2 Windows Defender & Antimalware
- **Windows Defender**: Enabled with real-time protection
- **Update Frequency**: Signature updates 4x daily
- **Scan Schedule**: Full system scan weekly (Sunday 2 AM)
- **Exclusions**: Database files, virtual memory (documented)
- **Threat Response**: Automatic quarantine enabled

### 3.3 Windows Firewall Configuration
- **Domain Profile**: Enabled (Inbound: Block, Outbound: Allow)
- **Private Profile**: Enabled (Inbound: Block, Outbound: Allow)
- **Public Profile**: Enabled (Inbound: Block, Outbound: Allow)
- **Exceptions**: Explicitly defined by port/protocol/source
- **Logging**: Enabled to firewall log file, 25 MB max

**Firewall Rules**:
| Service | Port | Protocol | Source | Action |
|---|---|---|---|---|
| Remote Desktop (RDP) | 3389 | TCP | Bastion Host only | Allow |
| HTTP | 80 | TCP | Load Balancer | Allow |
| HTTPS | 443 | TCP | Load Balancer | Allow |
| WinRM (Mgmt) | 5985-5986 | TCP | Admin subnet | Allow |

### 3.4 Access Control & User Rights
- **Local Admin Group**: Empty (use AD groups)
- **Guest Account**: Disabled
- **Default Administrator**: Disabled and renamed
- **Service Accounts**: Dedicated, non-interactive accounts
- **User Rights Assignment**: Principle of least privilege
  - SeRemoteInteractiveLogonRight: Admins only
  - SeTcbPrivilege: Only SYSTEM
  - SeImpersonatePrivilege: Service accounts only

### 3.5 Password Policy
- **Minimum Length**: 14 characters
- **Complexity**: Uppercase, lowercase, numbers, symbols required
- **History**: 24 previous passwords
- **Max Age**: 90 days (service accounts: 180 days)
- **Min Age**: 1 day
- **Account Lockout**: 5 failed attempts → 30-minute lockout

**GPO Configuration**:
```
Computer Configuration > Windows Settings > Security Settings > Account Policies > Password Policy
```

### 3.6 User Account Control (UAC)
- **Level**: Always notify (elevation required for admin tasks)
- **Secure Desktop**: Enabled (protects elevation prompts)
- **Admin Approval Mode**: Enabled for administrative accounts
- **Virtualization**: Enabled (file/registry redirection)

---

## 4. Data Protection & Encryption

### 4.1 BitLocker Full-Disk Encryption
- **System Drive (C:)**: BitLocker encryption enabled (XTS-AES 128-bit)
- **Recovery Key**: Escrow to Azure Key Vault / AWS KMS
- **TPM 2.0**: Utilized for key protection
- **PIN/Password**: Not required (TPM sufficient)
- **Suspend/Resume**: None active at deployment
- **Verification**: `manage-bde -status` confirms ON

**Implementation**:
```powershell
Enable-BitLocker -MountPoint "C:" -TpmProtector
```

### 4.2 Encrypted File System (EFS)
- **Sensitive Directories**: Documents, Customer Data, PII encrypted
- **Key Storage**: Backed up and escrow to AD
- **Recovery Agent**: Configured (domain admin account)
- **Inheritance**: Enabled for new files/folders

### 4.3 TLS/SSL Configuration
- **Minimum Version**: TLS 1.2 (TLS 1.3 preferred)
- **Ciphers**: AEAD ciphers only (ChaCha20-Poly1305, AES-GCM)
- **Weak Protocols**: SSL 3.0, TLS 1.0/1.1 disabled
- **Certificate Management**: 90-day renewal schedule
- **Pinning**: Optional for high-security applications

**Registry Configuration**:
```powershell
New-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client" -Name "Enabled" -Value 1
```

---

## 5. Auditing & Logging

### 5.1 Advanced Audit Policy
- **Logon Events**: Success & Failure
- **Logoff Events**: Success
- **Privilege Use**: All privilege uses
- **Object Access**: File share/registry access
- **Policy Changes**: Audit policy, security policy changes
- **System Events**: Time change, security system changes

**Enable Auditing**:
```powershell
auditpol /set /category:* /success:enable /failure:enable
```

### 5.2 Event Log Configuration
- **Security Log Size**: 20 GB minimum
- **Retention**: 90 days minimum (180 days recommended)
- **Archive**: Daily archive to Azure Storage / S3
- **Overwrite**: Only when space needed (after archival)

### 5.3 Windows Event Forwarding (WEF)
- **Collector Server**: Central WEF collector configured
- **Subscriptions**: All servers forward to collector
- **Forwarding**: HTTPS encrypted channel
- **Log Retention**: Collector retains 1 year

### 5.4 Performance Monitoring
- **Perfmon Counters**: CPU, Memory, Disk, Network baselines
- **Alert Thresholds**: CPU >80%, Memory >75%, Disk >85%
- **Collection**: Hourly automated collection
- **Analysis**: Weekly trend analysis

---

## 6. Application & Service Hardening

### 6.1 Service Hardening
**Disabled Services** (reduces attack surface):
- Remote Registry
- Telemetry (DiagTrack)
- Connected User Experiences
- Print Spooler (if not printing)
- Bluetooth Support Service (if not needed)

**Configuration**:
```powershell
Set-Service -Name DiagTrack -StartupType Disabled -Status Stopped
```

### 6.2 PowerShell Hardening
- **Version**: PowerShell 7+ (or 5.1 with hardening)
- **Execution Policy**: RemoteSigned minimum
- **Logging**: Script block logging enabled
- **Transcription**: Enabled for all sessions
- **Audit Module**: Enabled (logs all cmdlets)

### 6.3 Internet Explorer / Edge
- **IE**: Disabled (if not business critical)
- **Edge**: Latest version, automatic updates
- **Policies**: Security baselines applied
- **Extensions**: Whitelist approved only

---

## 7. Cloud-Specific Configuration

### 7.1 Azure-Specific
- **Managed Identity**: Assigned for authentication
- **Key Vault**: Access policy configured
- **Disk Encryption**: Azure Disk Encryption enabled
- **Backup**: Azure Backup agent installed
- **Monitoring**: Azure Monitor agent deployed

### 7.2 AWS-Specific
- **IAM Role**: Attached to EC2 instance
- **Systems Manager Agent**: Installed and running
- **KMS Encryption**: EBS volumes encrypted with CMK
- **Backup**: AWS Backup plan configured
- **CloudWatch**: Agent installed for metrics/logs

### 7.3 Hybrid (Outposts)
- **Network**: Direct connection to on-premises
- **Authentication**: Hybrid AD (AD FS or AD Connect)
- **DNS**: Dual DNS (cloud + on-premises)
- **VPN**: Site-to-Site VPN backup connection

---

## 8. Security Baselines & Compliance

### 8.1 Hardening Configuration
- **CIS Benchmarks**: Level 1 & Level 2 controls applied
- **DISA STIG**: Server 2022 STIG applied
- **NIST 800-53**: CM, IA, SC, SI controls implemented

### 8.2 Compliance Validation
- **Scans**: Run automated SCAP scans monthly
- **Assessment**: Manual review quarterly
- **Remediation**: Non-compliance addressed within 30 days
- **Documentation**: Compliance reports generated monthly

### 8.3 Baseline Image
- **Master Image**: Gold image created with all hardening
- **Versioning**: Image versioned and documented
- **Deployment**: All new servers from gold image
- **Updates**: Image updated monthly with latest patches

---

## 9. Pre-Deployment Checklist

### Phase 1: Planning & Approval
- [ ] Business requirements documented
- [ ] Security requirements identified
- [ ] Capacity planning completed
- [ ] Cost estimation approved
- [ ] Change management ticket created

### Phase 2: Infrastructure Setup
- [ ] Network VLAN created
- [ ] Load Balancer configured
- [ ] Storage accounts created
- [ ] Backup policies configured
- [ ] Monitoring dashboards created

### Phase 3: OS Installation
- [ ] VM/instance created from gold image
- [ ] Hostname configured per naming standard
- [ ] Network adapter configured (static IP)
- [ ] Storage drives attached and initialized
- [ ] Antimalware scan completed

### Phase 4: Security Hardening
- [ ] Windows updates installed
- [ ] Windows Firewall configured
- [ ] BitLocker enabled and verified
- [ ] Audit policies configured
- [ ] Security baselines validated
- [ ] Antimalware signatures updated
- [ ] TLS/SSL configured

### Phase 5: Application Deployment
- [ ] Application installed from approved source
- [ ] Configuration validated
- [ ] Health checks passing
- [ ] Load balancer health check enabled
- [ ] Monitoring alerts active

### Phase 6: Validation & Testing
- [ ] Security scan completed (passed)
- [ ] Compliance audit passed
- [ ] Load/stress testing completed
- [ ] Disaster recovery tested
- [ ] Backups verified

### Phase 7: Production Release
- [ ] Change management approval
- [ ] Runbooks documented
- [ ] Escalation procedures configured
- [ ] Staff trained
- [ ] Server moved to production subnet
- [ ] DNS updated

### Phase 8: Post-Deployment
- [ ] Monitoring confirmed active
- [ ] Baseline performance documented
- [ ] Security logs reviewed
- [ ] Backup jobs verified
- [ ] Incidents/gaps documented

---

## 10. Post-Deployment Activities

### 10.1 Initial Configuration (First 24 hours)
- ✓ Full malware scan completed
- ✓ Windows updates verified installed
- ✓ Event logs reviewed (no errors)
- ✓ Performance baseline captured
- ✓ Backup test completed

### 10.2 Week 1
- ✓ Security assessment/scan completed (no critical findings)
- ✓ Compliance audit passed
- ✓ Application performance validated
- ✓ User acceptance testing completed
- ✓ Training completed for operations team

### 10.3 Ongoing Maintenance
- **Weekly**: Security log review, performance analysis
- **Monthly**: Security patch application, compliance verification
- **Quarterly**: Full security assessment, firmware updates
- **Annually**: Disaster recovery test, policy review

---

## 11. Troubleshooting & Support

| Issue | Cause | Resolution |
|---|---|---|
| BitLocker suspend | OS update/update failed | Resume BitLocker via manage-bde command |
| Event log full | Log size too small | Increase log size via Event Viewer |
| High CPU usage | Malware scan / indexing | Check Task Manager, disable WIndows Search |
| Network connectivity loss | NIC driver | Update NIC driver, check network config |
| RDP not accessible | Firewall rule | Review NSG rules, verify RDP port |

---

## 12. Approval & Deployment Authority

**Build Sheet Approval**: Chief Information Officer  
**Security Review**: Chief Information Security Officer  
**Deployment Approval**: Cloud Operations Manager  
**Documentation Owner**: Cloud Architecture Team  
**Next Review Date**: January 2027  

---

**Related Documentation**:
- Windows Server 2022 Hardening Guide
- Cloud Security Baseline
- Incident Response Procedures
- Disaster Recovery Plan
