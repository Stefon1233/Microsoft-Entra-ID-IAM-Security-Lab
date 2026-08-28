# Microsoft Entra ID Environment Setup

## Overview

This section documents the initial configuration of the Microsoft Entra ID
environment used for the IAM and Security Lab.

The goal was to establish a controlled Microsoft cloud environment where
identity administration, authentication, role-based access control,
Conditional Access, security monitoring, and troubleshooting could be
practiced without affecting production users.

The environment served as the foundation for all later lab activities.

---

# Lab Objectives

The environment was prepared to support hands-on practice with:

- Microsoft Entra ID administration
- User and group management
- Authentication methods
- Multifactor Authentication
- Microsoft Authenticator
- Conditional Access
- Role-Based Access Control
- Least-privilege administration
- Sign-in log analysis
- Audit-log investigation
- Identity security
- Authentication troubleshooting

---

# Microsoft Entra Admin Center

Administrative tasks were performed through the Microsoft Entra admin
center.

The portal provided access to the major identity-management areas used
throughout the lab, including:

- Users
- Groups
- Roles and administrators
- Authentication methods
- Conditional Access
- Sign-in logs
- Audit logs
- Identity security settings

This provided a centralized location for managing and investigating the
Microsoft cloud identity environment.

---

# Environment Validation

Before implementing security controls, the Microsoft Entra environment was
reviewed to confirm that the tenant was accessible and administrative
features required for the lab were available.

The environment validation included reviewing:

- Tenant information
- Microsoft Entra navigation
- Existing users
- Existing groups
- Administrative capabilities
- Authentication configuration
- Conditional Access availability
- Sign-in monitoring capabilities
- Audit logging

This baseline review helped ensure that later security changes could be
accurately documented and tested.

---

# Dedicated Lab Identities

Dedicated identities were used for testing rather than relying exclusively
on the primary administrative account.

Examples included:

- Conditional Access test users
- Conditional Access administrative test identities
- Standard test users

Using dedicated accounts reduced the risk of affecting the primary
administrator while allowing realistic authentication and security
testing.

---

# Test Environment Design

The lab environment was intentionally structured around separate identity
types.

## Administrative Identity

Used to configure Microsoft Entra settings and security controls.

Administrative access was later restricted using Microsoft Entra directory
roles and least-privilege principles.

## Standard Test Identities

Used to simulate normal employee authentication scenarios.

These identities were used for:

- MFA registration
- Sign-in testing
- Conditional Access validation
- Authentication troubleshooting
- Sign-in log analysis

## Administrative Test Identity

Used to validate security controls applying specifically to privileged
users and Microsoft administrative resources.

---

# Security-First Lab Approach

Security changes were implemented using controlled test identities and
staged validation.

The general workflow used throughout the project was:

**Configure → Test → Validate → Investigate → Document**

For Conditional Access, this workflow was expanded to:

**Configure → Report-only → Simulate → Validate → Investigate →
Audit**

This reduced the risk of accidental administrative lockout.

---

# Portal Areas Used

The following areas of Microsoft Entra were used during the project.

| Area | Purpose |
|---|---|
| Users | Create, review, and administer identities |
| Groups | Organize identities and target security controls |
| Roles and administrators | Implement RBAC and least privilege |
| Authentication methods | Configure supported authentication options |
| Conditional Access | Build identity-security access policies |
| Sign-in logs | Investigate authentication activity |
| Audit logs | Review administrative changes |
| Protection/Security | Review identity-security capabilities |

---

# Licensing Considerations

Some Microsoft Entra functionality depends on tenant licensing.

The lab successfully supported standard Conditional Access functionality.

During testing, risk-based Conditional Access conditions such as Sign-in
risk were not available in the tenant.

Rather than documenting a feature that could not be validated, the
limitation was recorded and the lab continued with supported Conditional
Access controls.

This reflects a real-world administrative requirement: understanding that
available security functionality can depend on licensing and tenant
configuration.

---

# Evidence

Environment evidence is stored in:

`Screenshots/Entra-ID/`

Primary screenshot:

- `01-Entra-Overview.png`

This screenshot demonstrates access to the Microsoft Entra administrative
environment used throughout the lab.

---

# Skills Demonstrated

This portion of the lab demonstrates:

- Microsoft Entra tenant navigation
- Cloud identity administration
- Lab-environment planning
- Test-account strategy
- Security change management
- Administrative risk reduction
- Microsoft cloud troubleshooting
- Licensing awareness
- Technical documentation

---

# Key Takeaways

A properly structured identity lab should separate administrative access
from test activity.

Dedicated identities make it possible to safely test authentication and
access controls while reducing the risk of disrupting the primary
administrator.

Establishing the environment before implementing security policies also
creates a reliable baseline for later troubleshooting and validation.
