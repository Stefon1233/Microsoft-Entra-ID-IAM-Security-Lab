# Role-Based Access Control and Administrative Permissions

## Overview

This section documents Role-Based Access Control testing within Microsoft
Entra ID.

The lab focused on separating administrative responsibilities and
demonstrating the principle of least privilege.

Instead of giving every administrator unrestricted access, Microsoft Entra
directory roles were used to provide permissions appropriate to specific
administrative responsibilities.

---

# Objectives

The objectives were to:

- Review Microsoft Entra administrative roles
- Assign limited administrative permissions
- Test role capabilities
- Validate restricted access
- Demonstrate least privilege
- Separate security responsibilities
- Protect privileged identities

---

# Role-Based Access Control

Role-Based Access Control assigns permissions based on an administrator's
responsibilities.

Instead of granting Global Administrator permissions to every support
technician, narrower roles can be assigned.

This reduces unnecessary privileged access.

---

# Roles Tested

The lab included testing with roles such as:

- Conditional Access Administrator
- Helpdesk Administrator
- Security Reader

Each role provides a different level of administrative capability.

---

# Conditional Access Administrator

The Conditional Access Administrator role was used to demonstrate
delegated security-policy administration.

The role allows an administrator to work with Conditional Access without
granting unrestricted control over the entire Microsoft Entra tenant.

Testing confirmed that the delegated administrator could access
Conditional Access functionality while remaining restricted from unrelated
administrative functions.

---

# Helpdesk Administrator

The Helpdesk Administrator role represents a common IT support
responsibility.

The role provides limited user-support capabilities without granting broad
tenant-level administration.

This demonstrates how help desk employees can receive the permissions
necessary for common support tasks while maintaining separation from
high-risk security configuration.

---

# Security Reader

The Security Reader role provides read-only access to security
information.

This role is useful for:

- Security analysts
- Auditors
- Monitoring personnel
- Support staff who need visibility without configuration permissions

Read-only access reduces the risk of unintended configuration changes.

---

# Least Privilege

The principle of least privilege states that users and administrators
should receive only the permissions required to perform their
responsibilities.

This reduces the impact of:

- Account compromise
- Human error
- Accidental configuration changes
- Insider misuse

The lab applied this principle by testing specialized administrative roles
instead of relying exclusively on Global Administrator access.

---

# Administrative Separation

Administrative responsibilities can be separated across different roles.

Example:

| Role | Responsibility |
|---|---|
| Helpdesk Administrator | User support activities |
| Conditional Access Administrator | Access-policy administration |
| Security Reader | Security monitoring |
| Global Administrator | Highest-level tenant administration |

This model reduces unnecessary privileged access.

---

# Permission Validation

Permissions were not assumed based only on role assignment.

Administrative access was tested after assigning roles.

The lab verified both:

- What the delegated administrator could access
- What the delegated administrator could not access

Negative permission testing is important because it confirms that
least-privilege restrictions are actually functioning.

---

# Conditional Access Administration Test

A delegated Conditional Access administrator was able to access
Conditional Access policy management.

At the same time, the account remained limited from unrelated
administrative functionality.

This demonstrated successful role separation.

---

# Privileged Identity Security

Privileged accounts represent high-value targets.

Compromise of a highly privileged identity can affect:

- Users
- Groups
- Applications
- Security policies
- Authentication settings
- Organizational data

Limiting privileges reduces the potential impact of a compromised
administrative account.

---

# Evidence

RBAC evidence is stored in:

`Screenshots/RBAC/`

Screenshots include:

- `01-Conditional-Access-Administrator.png`
- `02-Helpdesk-Administrator.png`
- `03-Security-Reader.png`
- `04-CA-Admin-Conditional-Access.png`
- `05-CA-Admin-Limited-Permissions.png`

These screenshots demonstrate both role assignment and practical
permission validation.

---

# Skills Demonstrated

This portion of the lab demonstrates:

- Microsoft Entra RBAC
- Directory role administration
- Least privilege
- Administrative delegation
- Privileged identity security
- Permission validation
- Negative access testing
- Microsoft cloud security
- Help desk permission design
- Security administration

---

# Key Takeaways

Administrative security requires more than controlling user access.

Administrator permissions must also be restricted.

Microsoft Entra RBAC provides a way to separate responsibilities so that
support technicians, security analysts, and identity administrators
receive only the permissions necessary for their roles.

Testing both allowed and restricted actions provides stronger evidence
that least privilege is functioning correctly.
