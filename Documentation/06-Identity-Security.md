# Identity Security and Monitoring

## Overview

This section summarizes the identity-security controls implemented
throughout the Microsoft Entra ID IAM and Security Lab.

The project combined authentication security, Conditional Access, least
privilege, monitoring, and audit investigation to create a layered
identity-security approach.

---

# Identity Security Objectives

The lab focused on protecting identities through:

- Stronger authentication
- Multifactor Authentication
- Administrative MFA
- Conditional Access
- Blocking legacy authentication
- Device-platform restrictions
- Location-based controls
- Authentication-flow restrictions
- Least-privilege RBAC
- Sign-in monitoring
- Audit-log review

---

# Layered Security Approach

Identity security is most effective when multiple controls work together.

The lab implemented multiple security layers rather than relying on a
single policy.

These included:

**Identity → Authentication → Authorization → Access Policy →
Monitoring → Audit**

---

# Strong Authentication

Microsoft Authenticator and MFA were configured and tested.

MFA reduces the risk associated with compromised passwords by requiring an
additional authentication factor.

Administrative identities were given particular attention because
privileged accounts represent higher-value targets.

---

# Conditional Access

Conditional Access was used to evaluate authentication context before
allowing access.

Policies addressed:

- Test-user MFA
- Administrator MFA
- Legacy authentication
- Trusted network locations
- Device platforms
- Microsoft administrative portals
- Device code authentication

All lab policies remained in Report-only mode during testing.

This allowed policy behavior to be validated safely.

---

# Legacy Authentication Protection

Legacy authentication methods can bypass or fail to support modern
identity-security controls.

A Conditional Access policy was created to block legacy client
authentication.

This demonstrated how organizations can reduce exposure to older
authentication mechanisms.

---

# Location-Based Security

A named location was created to represent a trusted corporate network.

Conditional Access was then configured to distinguish between trusted and
untrusted network locations.

The lab validated both:

- Access originating outside the trusted location
- Access originating from the trusted location

Testing both conditions confirmed that the location logic behaved as
intended.

---

# Device Platform Controls

Conditional Access was configured to evaluate device platform conditions.

The lab demonstrated how organizations can restrict authentication from
unsupported platforms.

What If testing was used to validate the expected policy behavior before
enforcement.

---

# Device Code Authentication Protection

Device code authentication can be useful for devices with limited input
capabilities, but it can also be abused in phishing and token-theft
scenarios.

A Conditional Access policy was created to block device code
authentication for the test environment.

What If testing demonstrated that the authentication flow matched the
intended policy.

---

# Administrative Portal Protection

Microsoft administrative portals provide access to sensitive cloud
configuration.

A Conditional Access policy was configured to require MFA when accessing
Microsoft administrative resources.

This provides an additional security layer around privileged
administration.

---

# Least-Privilege Administration

Microsoft Entra RBAC was used to separate administrative responsibilities.

Roles included:

- Conditional Access Administrator
- Helpdesk Administrator
- Security Reader

Role testing confirmed that administrators could perform intended
responsibilities without receiving unnecessary tenant-wide privileges.

---

# Sign-In Monitoring

Microsoft Entra sign-in logs were reviewed to investigate authentication
activity.

The logs provided information such as:

- User
- Application
- Authentication status
- MFA status
- Conditional Access results
- Failure or interruption information

Sign-in monitoring provides operational visibility into user
authentication.

---

# Audit Monitoring

Microsoft Entra audit logs were reviewed to validate administrative
changes.

Audit records were used to identify activity such as:

- Conditional Access policy creation
- Security configuration changes
- Modified policy properties

This provides accountability and change tracking.

---

# Security Validation

The lab emphasized validation rather than assuming that configuration
alone meant a security control was functioning.

Validation included:

- MFA authentication testing
- Conditional Access What If testing
- Report-only evaluation
- Sign-in log analysis
- RBAC permission testing
- Audit-log review

---

# Licensing Awareness

Risk-based Conditional Access was investigated during the project.

The Sign-in risk condition required additional Microsoft Entra ID
Protection capabilities that were not exposed in the lab tenant.

The limitation was documented instead of representing an unsupported
feature as completed.

Understanding licensing limitations is part of real Microsoft cloud
administration.

---

# Public Evidence Security

Portfolio screenshots should avoid exposing unnecessary sensitive
information.

Evidence was reviewed with attention to removing or avoiding:

- Real public IP addresses when unnecessary
- Personal information
- Sensitive identifiers
- Unrelated tenant data

Documentation-only network ranges can be used when demonstrating security
concepts.

---

# Identity Security Model

The overall identity-security approach demonstrated in this project can be
summarized as:

**Verify the identity**

→ Use MFA

**Limit privileges**

→ Apply RBAC

**Evaluate access context**

→ Use Conditional Access

**Restrict risky authentication**

→ Block legacy and device-code flows

**Monitor authentication**

→ Review sign-in logs

**Monitor administration**

→ Review audit logs

---

# Skills Demonstrated

This portion of the lab demonstrates:

- Microsoft Entra security administration
- Identity protection concepts
- Authentication hardening
- MFA
- Conditional Access
- Least privilege
- RBAC
- Legacy authentication protection
- Device security controls
- Location-based access controls
- Authentication-flow restrictions
- Sign-in monitoring
- Audit investigation
- Security validation

---

# Key Takeaways

Identity security requires multiple coordinated controls.

Strong authentication alone is not enough.

Organizations also need restricted administrative permissions, contextual
access policies, authentication monitoring, and administrative auditing.

The lab demonstrated how these Microsoft Entra capabilities work together
to protect cloud identities and access.
