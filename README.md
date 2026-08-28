# Microsoft Entra ID IAM & Security Lab

## Overview

This project demonstrates hands-on administration of Microsoft Entra ID in
a simulated enterprise identity and access management environment.

The lab focuses on practical IAM and identity-security tasks including
user and group administration, multifactor authentication, Conditional
Access, role-based access control, authentication-method configuration,
sign-in investigation, audit-log analysis, and identity troubleshooting.

Rather than documenting configuration alone, the project includes
screenshots, validation tests, sign-in evidence, audit records, and
troubleshooting examples to demonstrate how identity controls are
configured, tested, monitored, and documented.

---

## Technologies and Services

- Microsoft Entra ID
- Microsoft Entra admin center
- Conditional Access
- Microsoft Authenticator
- Multifactor Authentication
- Role-Based Access Control
- Microsoft Entra sign-in logs
- Microsoft Entra audit logs
- Authentication Methods
- Named Locations
- Conditional Access What If
- Microsoft 365 identity services

---

## Lab Objectives

The primary objectives of this lab were to:

- Build and manage test identities in Microsoft Entra ID
- Organize identities with security groups
- Configure multifactor authentication
- Configure Microsoft Authenticator
- Apply least-privilege administrative roles
- Create and evaluate Conditional Access policies
- Use Report-only deployment for safe policy testing
- Restrict legacy authentication
- Protect privileged access
- Create trusted network locations
- Restrict unsupported device platforms
- Protect Microsoft administrative portals
- Block device code authentication
- Validate policies with the Conditional Access What If tool
- Review authentication activity in sign-in logs
- Review administrative changes in audit logs
- Troubleshoot authentication and access issues
- Document licensing and feature limitations

---

# Environment

The lab used dedicated test identities rather than production users.

Examples included:

- CA Test User
- CA Test Admin
- Additional security-lab test users

A dedicated Conditional Access test group was created:

`SG-CA-Test-Users`

Using dedicated test identities allowed policy behavior to be evaluated
without broadly affecting other tenant users.

---

# User and Group Administration

The Microsoft Entra environment included practical identity-management
activities such as:

- Creating test user accounts
- Reviewing user account properties
- Creating security groups
- Assigning users to security groups
- Reviewing group membership
- Using groups to scope security policies

The test environment provided a controlled identity structure for MFA,
RBAC, and Conditional Access testing.

### Evidence

See:

`Screenshots/Users-Groups/`

---

# Multifactor Authentication

Multifactor authentication was configured and tested using Microsoft
Authenticator.

Lab activities included:

- Authenticator registration
- Security registration prompts
- Authentication-method configuration
- Number-matching authentication
- Successful MFA validation
- Troubleshooting expired or interrupted authentication sessions

MFA was also incorporated into multiple Conditional Access policies.

### Evidence

See:

`Screenshots/MFA/`

and:

`Screenshots/Authentication/`

---

# Authentication Methods

Authentication-method configuration was reviewed and documented within
Microsoft Entra.

Evidence includes:

- Authentication Methods baseline
- Microsoft Authenticator configuration
- Authenticator availability for users
- Security registration
- Authentication-method setup

These controls demonstrate how administrators manage the authentication
mechanisms available to organizational identities.

### Evidence

See:

`Screenshots/Authentication/`

---

# Role-Based Access Control

Administrative permissions were configured using Microsoft Entra directory
roles.

Roles evaluated included:

- Conditional Access Administrator
- Helpdesk Administrator
- Security Reader

The lab demonstrated how administrative responsibilities can be separated
instead of assigning broad Global Administrator access.

Additional testing demonstrated that a Conditional Access Administrator
could manage Conditional Access while remaining restricted from unrelated
administrative capabilities.

This reflects the principle of least privilege.

### Evidence

See:

`Screenshots/RBAC/`

---

# Conditional Access

Conditional Access was one of the primary components of this project.

Policies were intentionally maintained in:

`Report-only`

This allowed policy behavior to be evaluated without enforcing controls
that could accidentally lock out administrators or test users.

The deployment workflow followed:

**Configure → Report-only → Simulate → Validate → Investigate → Audit
→ Document**

---

## Conditional Access Policies

### Baseline — Require MFA and Compliant Device

`CA-Require-MFA-and-Compliant-Device`

Demonstrated a combined security requirement using:

- Multifactor authentication
- Compliant-device requirement
- Windows platform targeting
- Report-only evaluation

---

### CA001 — Require MFA for Test Users

`CA001-Require-MFA-Test-Users`

Purpose:

Require multifactor authentication for members of the Conditional Access
test group.

Validation included:

- What If testing
- Real sign-in activity
- Report-only Conditional Access results
- Successful MFA evaluation

---

### CA002 — Block Legacy Authentication

`CA002-Block-Legacy-Authentication`

Purpose:

Block authentication through legacy client types that may not support
modern identity-security controls such as MFA.

Client types included:

- Exchange ActiveSync clients
- Other legacy clients

Grant control:

`Block access`

---

### CA003 — Require MFA for Administrators

`CA003-Require-MFA-Admins`

Purpose:

Strengthen privileged identity security by requiring MFA for selected
administrative roles.

The policy targeted multiple administrative roles while remaining in
Report-only mode for safe evaluation.

---

### CA004 — Block Access Outside Trusted Location

`CA004-Block-Access-Outside-Trusted-Location`

Purpose:

Demonstrate network-location-based access restrictions.

A trusted named location was created:

`Trusted-Corporate-Network`

Documentation IP range:

`203.0.113.0/24`

What If validation demonstrated both sides of the policy:

- Outside trusted location → policy applies
- Trusted location → policy excluded

---

### CA005 — Block Unsupported Device Platforms

`CA005-Block-Unsupported-Device-Platforms`

Purpose:

Restrict access from unsupported device platforms.

What If testing using a simulated macOS sign-in showed that CA005 matched
the scenario and would result in:

`Block access`

The policy remained in Report-only mode.

---

### CA006 — Require MFA for Admin Portals

`CA006-Require-MFA-Admin-Portals`

Purpose:

Protect access to Microsoft administrative portals with multifactor
authentication.

The policy targeted Microsoft Admin Portals and required MFA.

Policy Details were used as configuration evidence.

---

### CA007 — Block Device Code Authentication

`CA007-Block-Device-Code-Authentication`

Purpose:

Restrict device code authentication.

Configuration included:

- Test identities
- All resources
- Device code authentication flow
- Block access
- Report-only deployment

Conditional Access What If testing successfully showed CA007 under
policies that would apply with:

`Block access`

---

# Conditional Access Validation

Conditional Access policies were not considered complete after creation.

Validation included:

- Policy Details review
- What If simulation
- Positive-match testing
- Policy-exclusion testing
- Sign-in log review
- Report-only results
- Audit-log investigation

What If testing evaluated variables such as:

- User identity
- Target resource
- Device platform
- Client application
- Network location
- Authentication flow

Reviewing both **Policies that will apply** and **Policies that will not
apply** helped identify why individual policies matched or did not match a
simulated authentication event.

### Evidence

See:

`Screenshots/Conditional-Access/`

Detailed documentation:

`Documentation/04-Conditional-Access.md`
# Sign-In Log Investigation

Microsoft Entra sign-in logs were reviewed to investigate authentication
activity from the test identities.

Information reviewed included:

- User
- Application
- Authentication requirement
- Authentication status
- MFA result
- Conditional Access evaluation
- Date and time

A successful test-user sign-in demonstrated:

- Azure Portal authentication
- Multifactor authentication requirement
- Successful authentication
- MFA requirement satisfied
- CA001 evaluated successfully in Report-only mode

The project also includes an interrupted sign-in involving an expired
password as a troubleshooting example.

Sensitive network information that was unnecessary for the portfolio was
removed or cropped from public screenshots.

---

# Audit Log Investigation

Microsoft Entra audit logs were used to verify administrative changes.

Audit evidence was captured for creation of:

`CA007-Block-Device-Code-Authentication`

The activity showed:

`Add conditional access policy`

Audit-log review demonstrates practical understanding of:

- Administrative accountability
- Configuration tracking
- Change investigation
- Security monitoring
- Troubleshooting
- Policy validation

### Evidence

See:

`Screenshots/Conditional-Access/25-Entra-ID-Audit-Logs-Directory-Activity.png`

`Screenshots/Conditional-Access/26-Audit-Log-CA007-Policy-Creation-Success.png`

`Screenshots/Conditional-Access/27-Audit-Log-CA007-Policy-Modified-Properties.png`

---

# Troubleshooting

The lab included identity and authentication troubleshooting rather than
only successful configurations.

Examples included:

- Expired authentication session
- Interrupted sign-in
- Expired password
- Conditional Access policy not applying
- Conditional Access policy exclusions
- Unsupported What If resource selection
- Feature availability limitations

Troubleshooting focused on using Microsoft Entra logs and policy
evaluation data to determine why authentication or policy behavior
differed from expectations.

### Evidence

See:

`Screenshots/Troubleshooting/`

and:

`Screenshots/Conditional-Access/`

---

# Licensing and Feature Limitations

A risk-based Conditional Access policy was evaluated during the lab.

The intended configuration would have required MFA for medium- and
high-risk sign-ins.

However, the tenant did not expose the Sign-in risk condition.

Rather than substituting an unrelated security control and presenting it
as risk-based Conditional Access, the limitation was documented and the
project continued with controls supported by the available environment.

This demonstrates the importance of understanding licensing and feature
availability when administering Microsoft cloud environments.

---

# Safe Conditional Access Deployment

Conditional Access policies can affect authentication across an entire
organization.

A poorly configured policy can result in widespread access problems or
administrative lockout.

For this reason, the lab used a staged security workflow:

1. Create dedicated test identities.
2. Scope policies to appropriate identities.
3. Configure the intended conditions.
4. Configure access controls.
5. Set the policy to Report-only.
6. Run What If simulations.
7. Review sign-in results.
8. Investigate non-applicable policies.
9. Review administrative audit activity.
10. Document the final configuration.

A production rollout could continue with:

**Report-only → Pilot Group → Monitor → Enforce**

---

# Repository Structure

```text
Microsoft-Entra-ID-IAM-Security-Lab/
│
├── Documentation/
│   ├── 01-Environment-Setup.md
│   ├── 02-Users-Groups.md
│   ├── 03-MFA-Authentication.md
│   ├── 04-Conditional-Access.md
│   ├── 05-RBAC-Permissions.md
│   ├── 06-Identity-Security.md
│   └── 07-Troubleshooting.md
│
├── Screenshots/
│   ├── Authentication/
│   ├── Conditional-Access/
│   ├── Entra-ID/
│   ├── Identity-Security/
│   ├── MFA/
│   ├── RBAC/
│   ├── Sign-In-Logs/
│   ├── Troubleshooting/
│   └── Users-Groups/
│
├── Diagrams/
├── Help-Desk-Tickets/
├── .gitignore
└── README.md
```

---

# Documentation

Detailed implementation notes are available in:

- `Documentation/01-Environment-Setup.md`
- `Documentation/02-Users-Groups.md`
- `Documentation/03-MFA-Authentication.md`
- `Documentation/04-Conditional-Access.md`
- `Documentation/05-RBAC-Permissions.md`
- `Documentation/06-Identity-Security.md`
- `Documentation/07-Troubleshooting.md`

The Conditional Access documentation contains detailed policy
configuration, validation methodology, sign-in analysis, audit evidence,
security rationale, and screenshot references.

---
# Skills Demonstrated

This project demonstrates hands-on experience with:

- Microsoft Entra ID
- Identity and Access Management
- User administration
- Group administration
- Multifactor Authentication
- Microsoft Authenticator
- Authentication Methods
- Conditional Access
- Report-only Conditional Access deployment
- Conditional Access What If
- Named Locations
- Legacy authentication restrictions
- Device-platform restrictions
- Authentication-flow restrictions
- Administrative portal protection
- Role-Based Access Control
- Least privilege
- Privileged identity security
- Sign-in log analysis
- Audit log analysis
- Identity troubleshooting
- Security-policy validation
- Change tracking
- Microsoft cloud administration
- Technical documentation

---

# Security Practices Demonstrated

Security practices applied during the lab included:

- Least-privilege administrative access
- Dedicated test identities
- Group-based policy targeting
- MFA for users and administrators
- Blocking legacy authentication
- Trusted-location design
- Device-platform restrictions
- Device code authentication restrictions
- Report-only policy deployment
- Positive and negative policy testing
- Authentication monitoring
- Administrative audit review
- Public screenshot sanitization
- Documentation of licensing limitations

---
# Key Takeaways

This lab reinforced that identity security involves more than creating
users or enabling MFA.

Effective Microsoft Entra administration requires administrators to
understand how identities, authentication methods, roles, Conditional
Access policies, device conditions, locations, applications, and
authentication flows interact.

It also demonstrated that security policies should be tested and monitored
before enforcement.

The combination of configuration evidence, What If simulation, real
sign-in investigation, Report-only validation, RBAC testing,
troubleshooting, and audit-log analysis provides a practical demonstration
of Microsoft Entra ID IAM and security administration.

---

## Portfolio Purpose

This project was created as a hands-on portfolio lab to demonstrate
practical skills relevant to roles such as:

- IT Support Specialist
- Help Desk Technician
- Microsoft 365 Support Specialist
- Identity and Access Management Support
- Cloud Support Technician
- Junior Systems Administrator
- Microsoft Entra ID Administrator
- Technical Support Specialist
