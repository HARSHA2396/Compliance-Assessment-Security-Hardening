# Cloud Access Security Broker (CASB) Analysis & Implementation

**Document ID**: CASB-ANALYSIS-001  

## Executive Summary

This document analyzes the organization's cloud application landscape and provides recommendations for implementing a Cloud Access Security Broker (CASB) solution to:
- **Gain visibility** into unauthorized cloud app usage
- **Protect sensitive data** from exposure in cloud services
- **Detect and respond** to advanced threats
- **Ensure compliance** with regulatory requirements

**Current Risk Level**: **MEDIUM** (without CASB controls)

---

## 1. Current Cloud Services Inventory

### 1.1 Authorized SaaS Applications

| Application | Classification | Users | Data Sensitivity | Risk Level |
|---|---|---|---|---|
| **Microsoft Office 365** | Tier 1 (Core) | All | High | Low |
| **Google Workspace** | Tier 1 (Core) | 80% | Medium | Low |
| **AWS Services** | Tier 1 (Core) | IT/Dev | High | Low |
| **Salesforce** | Tier 2 (Business) | Sales/Mkt | High | Medium |
| **Box** | Tier 2 (Business) | Marketing | Medium | Medium |
| **Slack** | Tier 2 (Business) | All | Low-Medium | Medium |
| **ServiceNow** | Tier 2 (Business) | IT/HR | High | Medium |
| **GitHub** | Tier 2 (Business) | Dev/DevOps | High | Low |

### 1.2 Shadow IT Risks
**Estimated unauthorized cloud apps**: 200+ (identified via network monitoring)
- Personal cloud storage (OneDrive, Google Drive, Dropbox)
- Communication apps (WhatsApp, Telegram, Discord)
- File sharing (WeTransfer, 4Shared)
- Collaboration (Notion, Asana, Monday.com)

**Risk**: Unmanaged data sharing, compliance violations, DLP bypass

---

## 2. CASB Functions & Requirements

### 2.1 Visibility & Discovery
**Function**: Identify all cloud applications, users, and usage patterns

**Capabilities Required**:
- ✓ Cloud app catalog (5000+ pre-defined apps)
- ✓ Shadow IT discovery (network traffic analysis)
- ✓ User activity tracking
- ✓ Department/Cost center allocation
- ✓ Risk scoring per application
- ✓ Compliance mapping (HIPAA, GDPR, SOC2)

**Business Value**:
- Reduce security gaps from unmanaged cloud apps
- Understand true SaaS spending (40-60% savings potential)
- Identify risky applications for policy action

### 2.2 Data Loss Prevention (DLP)
**Function**: Prevent sensitive data from leaving corporate control

**Capabilities Required**:
- ✓ Pattern matching (SSN, CC#, API keys)
- ✓ Custom DLP rules per data classification
- ✓ Watermarking for sensitive documents
- ✓ Blocking/alerting on policy violations
- ✓ Logging of all DLP events (1 year retention)
- ✓ Integration with cloud storage (OneDrive, Box, Dropbox)

**Policy Examples**:
- Block external sharing of customer PII
- Watermark confidential documents
- Alert on bulk file downloads
- Restrict access to restricted apps

### 2.3 Threat Protection
**Function**: Detect compromised accounts, malware, and suspicious behavior

**Capabilities Required**:
- ✓ Anomaly detection (user behavior analytics)
- ✓ Malware detection (file scanning)
- ✓ Ransomware detection (encryption patterns)
- ✓ Insider threat detection (unauthorized access)
- ✓ Compromised account detection (impossible travel, mass download)
- ✓ Real-time alerting and response

**Detection Scenarios**:
- User downloads 1GB of files (unusual activity)
- Login from 2 countries within 30 minutes
- Attempt to access 50+ files in 10 minutes
- Unauthorized external sharing enabled
- Sensitive file access from VPN/suspicious network

### 2.4 Compliance & Governance
**Function**: Ensure cloud services meet regulatory/policy requirements

**Capabilities Required**:
- ✓ Pre-built compliance frameworks (HIPAA, PCI, GDPR, SOC2)
- ✓ Policy enforcement (auto-block/remediate)
- ✓ Audit logging (immutable records)
- ✓ Compliance reporting (monthly/quarterly)
- ✓ Access control based on user role
- ✓ Data residency enforcement

**Compliance Requirements**:
- Only US-based data storage (US data residency)
- Limited access to health records (HIPAA)
- Restricted shared external access (GDPR)
- 90-day log retention minimum

### 2.5 Advanced Controls
**Function**: Advanced protection and administration

**Capabilities Required**:
- ✓ Conditional access policies
- ✓ Session-based access control (CAE)
- ✓ Encryption in transit/at rest
- ✓ API integration with cloud apps
- ✓ Admin quarantine & remediation
- ✓ Custom playbook/automation

---

## 3. CASB Solution Comparison

### 3.1 Microsoft Cloud App Security (MCAS) / Defender for Cloud Apps

**Strengths**:
- ✓ Native Office 365 integration (E5 license included)
- ✓ Native Azure AD / Conditional Access integration
- ✓ Automatic threat response actions
- ✓ Cost-effective for Microsoft-centric organizations
- ✓ 30-day shadow IT data retention

**Weaknesses**:
- ✗ Limited advanced analytics vs competitors
- ✗ Setup requires Azure AD Premium
- ✗ Best for Microsoft ecosystem (GCP/AWS less integrated)

**Recommendation**: **EXCELLENT** for Office 365-first environment

### 3.2 Netskope

**Strengths**:
- ✓ Full proxy architecture (better threat detection)
- ✓ Cloud-native (handles 10,000+ apps)
- ✓ Advanced DLP with OCR/keyboard logging
- ✓ Multi-cloud support (AWS, Azure, GCP, Salesforce)
- ✓ Advanced threat prevention (0-day)
- ✓ Real-time reporting dashboard

**Weaknesses**:
- ✗ Higher licensing cost ($150-300 per user/year)
- ✗ Requires network integration (firewall, proxy, PAC)
- ✗ Steeper learning curve

**Recommendation**: **EXCELLENT** for advanced threat protection & multi-cloud

### 3.3 Palo Alto Networks Prisma Cloud / Cortex

**Strengths**:
- ✓ Best-in-class threat intelligence
- ✓ Multi-cloud coverage (AWS, Azure, GCP)
- ✓ SIEM integration
- ✓ Insider threat detection

**Weaknesses**:
- ✗ Premium pricing ($200-400 per user/year)
- ✗ Complex deployment
- ✗ Requires Palo Alto firewall for best integration

**Recommendation**: **GOOD** for organizations with existing Palo Alto investment

### 3.4 Comparison Matrix

| Feature | MCAS | Netskope | Prisma | Proofpoint |
|---|---|---|---|---|
| **Visibility** | 9/10 | 10/10 | 9/10 | 8/10 |
| **DLP** | 8/10 | 10/10 | 8/10 | 9/10 |
| **Threat Detection** | 7/10 | 10/10 | 10/10 | 8/10 |
| **Compliance** | 9/10 | 8/10 | 9/10 | 9/10 |
| **Cost** | $6-15/user/mo | $15-25/user/mo | $25-40/user/mo | $10-20/user/mo |
| **Ease of Deployment** | 9/10 | 5/10 | 6/10 | 7/10 |
| **Integration** | Office 365 | Multi-Cloud | Multi-Cloud | Email-centric |

---

## 4. Recommended Implementation: Microsoft CASB (MCAS)

### 4.1 Rationale
- Existing Microsoft 365 E5 licenses include CASB
- Native Azure AD integration for conditional access
- 80% of organization uses Office 365
- Lower implementation complexity & cost
- Sufficient for current risk profile

### 4.2 Deployment Architecture

```
Cloud Applications (SaaS)
    ↓
MCAS (API integration)
    ↓
Azure AD (Identity)
    ↓
Conditional Access Policies
    ↓
Admin Console / SIEM Integration
```

### 4.3 Phase-by-Phase Implementation

#### **Phase 1: Foundation & Visibility (Months 1-2)**

**Objectives**:
- Deploy MCAS infrastructure
- Connect to cloud apps (Office 365, Salesforce, Google Workspace, Box)
- Gain visibility into cloud activity
- Identify shadow IT applications

**Activities**:
- [ ] Purchase MCAS licenses (included in E5)
- [ ] Provision CASB tenant
- [ ] Configure Office 365 connector (API integration)
- [ ] Configure Salesforce, Box, Google Workspace connectors
- [ ] Configure Azure AD integration
- [ ] Create admin roles and access policies
- [ ] Deploy log collector (optional, for on-prem apps)

**Success Criteria**:
- All 4 major cloud apps connected and showing activity
- 200+ shadow IT apps identified
- Dashboard displaying user activity/file operations
- Admin team trained on console

**Timeline**: 4-6 weeks

---

#### **Phase 2: Policy Enforcement (Months 3-4)**

**Objectives**:
- Implement DLP policies
- Configure access controls
- Enable threat detection
- Begin automated remediation

**Activities**:
- [ ] Create DLP policies:
  - PII/SSN detection → Block external share
  - Credit card detection → Block download
  - Confidential documents → Watermark
- [ ] Configure access policies:
  - Block unfamiliar IP addresses → Require MFA
  - Block impossible travel → Session termination
  - Block legacy protocols (SMTP) → Require OAuth
- [ ] Enable threat alerts
- [ ] Create custom playbooks for auto-remediation
  - Disable compromised user account
  - Quarantine suspicious files
  - Revoke external sharing

**Success Criteria**:
- 10+ active DLP policies
- 5+ access control policies active
- Zero false positives in first month
- 95%+ policy compliance rate

**Timeline**: 4-6 weeks

---

#### **Phase 3: Advanced Threat Protection (Months 5-6)**

**Objectives**:
- Deploy anomaly detection
- Integrate with SIEM (Sentinel/Splunk)
- Implement insider threat detection
- Enable session-based access control

**Activities**:
- [ ] Enable behavioral analytics
- [ ] Deploy Defender for Identity (if available)
- [ ] Integrate with Azure Sentinel for SIEM
- [ ] Configure alerting rules
- [ ] Implement session control (limited users initially)
- [ ] Enable file monitoring/quarantine

**Success Criteria**:
- 20+ behavioral detection rules
- 100% SIEM integration
- Average detection time <15 minutes
- Session control with 99% uptime

**Timeline**: 4-8 weeks

---

#### **Phase 4: Continuous Monitoring & Optimization (Months 7-8)**

**Objectives**:
- Fine-tune policies based on tuning
- Implement quarterly compliance reviews
- Establish incident response procedures
- Plan for multi-cloud expansion

**Activities**:
- [ ] Monthly CASB policy reviews
- [ ] Quarterly threat report generation
- [ ] Incident response procedure testing
- [ ] Staff training and certification
- [ ] Evaluate additional CASB features
- [ ] Plan Phase 2 expansion (Netskope for advanced threats)

**Success Criteria**:
- <5% policy exceptions
- <2 false positives per week
- Compliance audit passing
- Staff certified on CASB administration

**Timeline**: 2-4 weeks

---

## 5. Policy Implementation Examples

### 5.1 DLP Policies

```
Policy: Block PII Sharing
├─ Condition: File contains SSN/Health Record/PII
├─ Action: Block external share + Alert admin
└─ Exception: Only HR dept, with approval

Policy: Watermark Confidential
├─ Condition: File marked 'Confidential'
├─ Action: Add watermark when downloaded
└─ Scope: All users

Policy: Block Legacy Auth
├─ Condition: Login via SMTP, POP3, IMAP
├─ Action: Block immediately
└─ Exception: Service accounts (whitelist)
```

### 5.2 Access Control Policies

```
Policy: MFA for Suspicious Activity
├─ Condition: Login from new country
├─ Action: Require MFA
└─ Duration: 24 hours

Policy: Session Control for VPN
├─ Condition: Access from VPN + cloud app
├─ Action: Force re-authentication, limit file download
└─ Scope: Finance dept only

Policy: Block Mass Downloads
├─ Condition: Download >500 files in 5 minutes
├─ Action: Terminate session
└─ Alert: Security team
```

---

## 6. Success Metrics & KPIs

| Metric | Target | Timeline |
|---|---|---|
| **Shadow IT Discovery** | >90% of apps discovered | Month 2 |
| **DLP Blocks per Month** | 5-20 (no FP) | Months 3-8 |
| **Policy Compliance Rate** | >95% | Month 4 |
| **MTTR (Mean Time to Respond)** | <15 minutes | Month 6 |
| **User Awareness** | 100% training completion | Month 2 |
| **Threats Detected/Month** | 10-50 | Month 6 |
| **Incidents Resolved** | 98% automated | Month 8 |

---

## 7. Risk Assessment & Mitigation

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| **User Productivity Impact** | Medium | High | Start with shadow IT, use audit-only mode for 2 weeks |
| **False Positive Alerts** | High | Medium | Tuning phase (Month 2), whitelist exceptions |
| **Integration Issues** | Low | Medium | Test in staging, pilot with 100 users first |
| **Insider Threats** | Low | Critical | Advanced analytics + SIEM integration |
| **Compliance Gap** | Low | High | Map CASB policies to compliance framework |

---

## 8. Recommended Next Steps

1. **Immediate** (Week 1):
   - Conduct CASB requirements workshop
   - Evaluate MCAS vs Netskope final decision
   - Allocate budget and resources

2. **Short-term** (Months 1-2):
   - Begin Phase 1 deployment
   - Identify shadow IT applications
   - Train initial admin team

3. **Medium-term** (Months 3-6):
   - Deploy policies and automation
   - Fine-tune based on feedback
   - Prepare for Phase 2 expansion

4. **Long-term** (Months 7-12):
   - Evaluate Netskope for advanced threats
   - Multi-cloud expansion (AWS, GCP)
   - Integrate with enterprise SIEM

---

## Conclusion

Implementing a CASB solution is essential to:
- **Reduce shadow IT risk** (200+ unmanaged apps)
- **Prevent data loss** (DLP automation)
- **Detect threats faster** (behavioral analytics)
- **Ensure compliance** (regulatory alignment)

**Recommended Solution**: Microsoft Cloud App Security (MCAS) for Phase 1-2, with evaluation of **Netskope** for Phase 3 advanced threat protection.

---
