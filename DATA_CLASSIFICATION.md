# Hendrick Automotive Group - Data Classification Standards

## Overview

This document defines the data classification standards for Hendrick Automotive Group systems and applications. All data within Hendrick systems must be classified according to these standards to ensure appropriate security controls, access management, and compliance measures are applied.

## Data Classification Levels

### 1. Public

**Definition**: Information that can be freely shared with the general public without risk to Hendrick Automotive Group, its partners, customers, or business operations.

**Characteristics**:
- No confidentiality requirements
- No access restrictions required
- Can be published on websites, marketing materials, or public forums
- Loss or disclosure poses no risk to business operations

**Examples**:
- Marketing materials and press releases
- Published job openings and company information
- Publicly available financial reports
- General product catalogs and specifications
- Company location and contact information

**Security Requirements**:
- No special security controls required
- Standard backup and availability measures
- No access restrictions

---

### 2. Internal

**Definition**: Information intended for use within Hendrick Automotive Group that, while not publicly available, would not cause significant harm to the organization if inadvertently disclosed to external parties.

**Characteristics**:
- Intended for internal use only
- Limited business impact if disclosed externally
- May include operational data without sensitive details
- Requires basic access controls and protection measures

**Examples**:
- Internal operational procedures and policies
- Non-sensitive operational data and reports
- Internal training materials and documentation
- General vendor and supplier information
- Non-confidential project documentation
- **Hendrick Data API operational data** (inventory, sales, service records without PII)

**Security Requirements**:
- Access restricted to Hendrick employees and authorized partners
- Basic authentication and authorization controls
- Standard encryption in transit and at rest
- Regular access reviews
- Basic audit logging

---

### 3. Confidential

**Definition**: Sensitive information that requires protection due to legal, regulatory, contractual, or business requirements. Unauthorized disclosure could result in significant harm to Hendrick Automotive Group, its customers, partners, or business operations.

**Characteristics**:
- Significant business impact if disclosed
- May be subject to regulatory or contractual protection requirements
- Requires strong access controls and monitoring
- Limited to authorized personnel with business need

**Examples**:
- Customer personally identifiable information (PII)
- Financial data and pricing strategies
- Strategic business plans and market analysis
- Detailed vendor contracts and negotiations
- Employee personal information and HR records
- Detailed technical system configurations
- Customer financial and credit information

**Security Requirements**:
- Strong authentication and authorization controls
- Multi-factor authentication for access
- Encryption in transit and at rest with strong algorithms
- Comprehensive audit logging and monitoring
- Regular access reviews and certifications
- Data loss prevention measures
- Incident response procedures

---

### 4. Restricted

**Definition**: Highly sensitive information that requires the strongest protection measures. Unauthorized disclosure could result in severe harm to Hendrick Automotive Group, legal liability, regulatory violations, or significant competitive disadvantage.

**Characteristics**:
- Severe business, legal, or regulatory impact if disclosed
- Extremely limited access on strict need-to-know basis
- Subject to the highest level of security controls
- May require special handling and storage requirements

**Examples**:
- Trade secrets and proprietary technology
- Legal proceedings and attorney-client privileged information
- Merger and acquisition information
- Senior executive compensation and board materials
- Regulatory investigation materials
- Security incident response details
- Critical system credentials and cryptographic keys

**Security Requirements**:
- Highest level authentication and authorization controls
- Multi-factor authentication mandatory
- Advanced encryption with key management
- Comprehensive monitoring and real-time alerting
- Continuous access reviews
- Advanced data loss prevention
- Specialized incident response procedures
- Air-gapped or specially secured storage when required

## Data Handling Requirements by Classification

### Access Control Requirements

| Classification | Authentication | Authorization | Access Review Frequency |
|---------------|---------------|---------------|------------------------|
| Public | None required | None required | Not applicable |
| Internal | Standard authentication | Role-based access | Annual |
| Confidential | Strong authentication + MFA | Principle of least privilege | Quarterly |
| Restricted | Advanced authentication + MFA | Strict need-to-know | Monthly |

### Technical Security Controls

| Classification | Encryption in Transit | Encryption at Rest | Key Management | Audit Logging |
|---------------|---------------------|-------------------|----------------|---------------|
| Public | Optional | Optional | Not required | Basic |
| Internal | TLS 1.2+ | AES-256 | Standard | Standard |
| Confidential | TLS 1.3 | AES-256 | Managed keys | Comprehensive |
| Restricted | TLS 1.3 + Certificate pinning | AES-256 + HSM | HSM/Key vault | Real-time monitoring |

### Data Retention and Disposal

| Classification | Retention Policy | Disposal Method | Verification Required |
|---------------|------------------|-----------------|----------------------|
| Public | As per business need | Standard deletion | No |
| Internal | As per business policy | Secure deletion | Basic verification |
| Confidential | As per regulatory requirements | Cryptographic erasure | Documented verification |
| Restricted | Minimum required period | Multi-pass secure deletion | Certified verification |

## Classification Guidelines

### Determining Data Classification

**Step 1: Identify Data Content**
- What type of information does the data contain?
- Does it include personal information, financial data, or business secrets?
- Is it subject to regulatory requirements?

**Step 2: Assess Potential Impact**
- What would be the impact if this data were disclosed to unauthorized parties?
- Consider legal, regulatory, financial, and reputational impacts
- Evaluate competitive disadvantage potential

**Step 3: Apply Classification**
- Use the highest applicable classification level
- When in doubt, err on the side of higher classification
- Consult with security team for unclear cases

**Step 4: Document and Label**
- Clearly mark data with its classification level
- Document the rationale for classification decisions
- Ensure all stakeholders understand the classification

### Mixed Data Classification

When systems or datasets contain multiple classification levels:
- Apply the **highest classification level** to the entire system/dataset
- Implement controls appropriate for the highest classification
- Consider data segregation if feasible and cost-effective
- Document the mixed classification rationale

### Reclassification

Data classification may change over time due to:
- Changes in business sensitivity
- Regulatory requirement changes
- Data aging or becoming public
- Business context changes

**Reclassification Process**:
1. Evaluate current business and regulatory context
2. Assess current potential impact of disclosure
3. Document rationale for reclassification
4. Update security controls as appropriate
5. Notify all relevant stakeholders

## Compliance and Governance

### Responsibilities

**Data Owners**:
- Determine appropriate classification for data they own
- Ensure proper controls are implemented
- Review and update classifications as needed
- Approve access to confidential and restricted data

**Data Custodians**:
- Implement technical controls based on classification
- Monitor access and usage
- Report security incidents
- Maintain audit logs and documentation

**Data Users**:
- Handle data according to its classification
- Report suspected security incidents
- Comply with access and usage policies
- Understand their responsibilities for data protection

### Monitoring and Compliance

- Regular audits of data classification implementation
- Compliance monitoring for regulatory requirements
- Security control effectiveness reviews
- Incident response and reporting procedures
- Training and awareness programs

## Related Policies and Standards

This data classification standard supports and references:
- Information Security Policy
- Data Protection and Privacy Policy
- Access Control Standards
- Incident Response Procedures
- Business Continuity and Disaster Recovery Plans

---

**Document Version**: 1.0  
**Effective Date**: July 2, 2025  
**Review Date**: July 2, 2026  
**Owner**: Information Security Team  
**Approved By**: Chief Information Security Officer