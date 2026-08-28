# Multifactor Authentication and Authentication Methods

## Overview

This section documents authentication security configuration and
Multifactor Authentication testing in Microsoft Entra ID.

The lab focused on strengthening account authentication using Microsoft
Authenticator and validating successful MFA registration and sign-in
behavior.

---

# Objectives

The objectives were to:

- Review Microsoft Entra authentication methods
- Configure Microsoft Authenticator
- Register authentication methods
- Validate MFA enrollment
- Test MFA during authentication
- Review number-matching behavior
- Investigate authentication results
- Document authentication-related troubleshooting

---

# Multifactor Authentication

Multifactor Authentication adds an additional verification requirement
beyond a password.

Authentication can combine multiple factors such as:

- Something the user knows
- Something the user possesses
- Something the user is

In this lab, Microsoft Authenticator was used as the primary additional
authentication factor.

---

# Microsoft Authenticator

Microsoft Authenticator was configured as an available authentication
method.

The configuration was reviewed within Microsoft Entra to verify that the
method was enabled for the intended users.

Microsoft Authenticator supports stronger authentication workflows than
password-only authentication.

---

# Authentication Method Registration

A test identity completed the security-information registration process.

The registration process included:

1. Signing in with the test identity
2. Receiving the security registration prompt
3. Beginning Microsoft Authenticator setup
4. Linking the account with the Authenticator application
5. Completing authentication verification
6. Confirming successful registration

---

# Authentication Methods Baseline

Before and during configuration, authentication-method settings were
reviewed to understand which authentication options were available to
users.

Reviewing the baseline is important because authentication behavior
depends on both:

- User registration
- Tenant authentication-method configuration

An authentication application installed on a phone does not by itself
guarantee that the method is enabled for the user in Microsoft Entra.

---

# MFA Number Matching

MFA number matching was tested as part of the Microsoft Authenticator
authentication workflow.

Number matching requires the user to respond to an authentication request
using the number displayed during sign-in.

This improves security compared with simple approval prompts because it
reduces the likelihood that a user will accidentally approve an unexpected
authentication request.

---

# Successful Registration

The test identity successfully completed Microsoft Authenticator
registration.

This provided evidence that:

- The authentication method was available
- The user could enroll
- Microsoft Authenticator was linked successfully
- MFA challenges could be completed

---

# Conditional Access Integration

MFA was later integrated with Conditional Access policies.

Conditional Access policies included requirements such as:

- Require MFA for test users
- Require MFA for administrators
- Require MFA for Microsoft administrative portals

This demonstrates how authentication methods and Conditional Access work
together.

Conditional Access determines when stronger authentication is required,
while configured authentication methods provide the mechanism used to
satisfy the requirement.

---

# Sign-In Validation

Microsoft Entra sign-in logs were used to validate MFA behavior.

Successful sign-in evidence demonstrated that MFA requirements could be
evaluated during authentication.

One sign-in showed:

`MFA requirement satisfied by claim in the token`

This demonstrated that Microsoft Entra recognized an existing MFA claim
associated with the authentication session.

---

# Authentication Security Benefits

MFA significantly reduces the risk associated with password compromise.

If a password is stolen, an attacker must still satisfy the additional
authentication requirement.

MFA is particularly important for:

- Administrative accounts
- Remote access
- Microsoft administrative portals
- Sensitive applications
- High-value identities

---

# Authentication Troubleshooting

Authentication registration and sign-in testing also produced
troubleshooting scenarios.

One example involved an expired registration session.

Authentication troubleshooting requires administrators to determine
whether an issue originates from:

- Password state
- Authentication registration
- Authentication-method configuration
- Conditional Access
- Session state
- User assignment
- Licensing
- Device or application conditions

---

# Evidence

Authentication evidence is stored in:

`Screenshots/Authentication/`

Screenshots include:

- `01-CA-Admin-Security-Registration-Prompt.png`
- `02-Authenticator-App-Setup.png`
- `03-Authentication-Methods-Baseline.png`
- `04-Authenticator-Configuration.png`
- `05-Authenticator-All-Users-Enabled.png`

Additional MFA evidence is stored in:

`Screenshots/MFA/`

Screenshots include:

- `01-MFA-Number-Matching-Test.png`
- `02-Authenticator-Registration-Success.png`

---

# Skills Demonstrated

This portion of the lab demonstrates:

- Multifactor Authentication
- Microsoft Authenticator
- Authentication-method administration
- User authentication registration
- MFA number matching
- Authentication testing
- Conditional Access integration
- Authentication troubleshooting
- Sign-in investigation
- Microsoft Entra administration

---

# Key Takeaways

Authentication security requires more than simply enabling MFA.

Administrators must understand authentication methods, user registration,
policy targeting, sign-in behavior, and troubleshooting.

The lab demonstrated the complete process from authentication
configuration through successful user registration and MFA validation.
