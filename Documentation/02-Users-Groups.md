# User and Group Administration

## Overview

This section documents Microsoft Entra ID user and group administration
performed during the IAM and Security Lab.

Users and groups form the foundation of identity and access management.

The lab used dedicated test accounts and security groups to simulate
enterprise identity administration and provide controlled targets for
authentication and Conditional Access testing.

---

# Objectives

The objectives of this portion of the lab were to:

- Review Microsoft Entra users
- Configure dedicated security-lab identities
- Create security groups
- Add users to groups
- Validate group membership
- Use groups for policy targeting
- Separate administrative and standard test identities
- Demonstrate scalable access-management practices

---

# User Administration

Microsoft Entra users were reviewed through the Entra admin center.

The environment included dedicated identities created specifically for
security testing.

These accounts allowed authentication and Conditional Access scenarios to
be tested without relying on the primary administrator account.

---

# Security Lab Test Users

Test identities were used to simulate normal employee and administrative
authentication activity.

One of the primary Conditional Access test identities was:

`ca-test-user@stefon.onmicrosoft.com`

A dedicated administrative test identity was also used for privileged
access scenarios.

These accounts were used throughout the project for:

- MFA testing
- Authentication registration
- Conditional Access evaluation
- Sign-in testing
- Sign-in log investigation
- Authentication troubleshooting

---

# Group Administration

Security groups were created to organize test identities and provide
scalable targeting for security policies.

Rather than assigning every Conditional Access policy directly to
individual accounts, groups allow identities to be managed centrally.

This better represents enterprise identity administration.

---

# Conditional Access Test Group

A security group was created for Conditional Access testing.

Group:

`SG-CA-Test-Users`

The group was used to target selected Conditional Access policies to
controlled test identities.

This allowed policies to be validated without affecting the entire tenant.

---

# Group Membership Validation

After creating the security group, membership was reviewed to verify that
the correct test identities were assigned.

Validating membership is important because Conditional Access and other
identity controls frequently rely on group assignments.

An incorrect group membership can result in:

- Policies not applying
- Unexpected authentication requirements
- Access being incorrectly blocked
- Users receiving permissions they should not have

---

# Group-Based Security Targeting

Group-based policy targeting was used because it provides several
administrative advantages.

It allows administrators to:

- Add or remove users without modifying every policy
- Apply security controls consistently
- Reduce configuration duplication
- Delegate identity administration more effectively
- Scale security controls as organizations grow

---

# Identity Organization Strategy

The lab followed a simple identity organization model:

| Identity Type | Purpose |
|---|---|
| Primary administrator | Core tenant administration |
| Standard test user | Authentication and Conditional Access testing |
| Administrative test user | Privileged-access testing |
| Security group | Central policy targeting |

This structure allowed multiple security scenarios to be tested safely.

---

# Least-Privilege Considerations

Test users were not given unnecessary administrative privileges.

Administrative permissions were separated from standard user testing.

Later sections of the lab implemented Microsoft Entra RBAC roles to
demonstrate how administrative access can be limited to required
responsibilities.

---

# Evidence

Evidence is stored in:

`Screenshots/Users-Groups/`

Screenshots include:

- `01-All-Users.png`
- `02-Security-Lab-Test-Users.png`
- `03-Security-Groups.png`
- `04-CA-Test-Group-Membership.png`

These screenshots demonstrate the identity structure used throughout the
project.

---

# Skills Demonstrated

This portion of the lab demonstrates:

- Microsoft Entra user administration
- Security-group administration
- Group membership management
- Identity organization
- Group-based security targeting
- Conditional Access preparation
- Least-privilege identity design
- Microsoft cloud administration
- Technical documentation

---

# Key Takeaways

Users and groups are central to Microsoft Entra administration.

Groups provide a scalable method for assigning permissions and targeting
security controls.

Using dedicated test identities and groups also makes authentication
testing safer by limiting changes to controlled accounts rather than
applying experimental policies across an entire tenant.
