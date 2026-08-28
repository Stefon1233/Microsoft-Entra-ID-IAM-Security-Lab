# Conditional Access Implementation and Validation

## Overview

This portion of the Microsoft Entra ID lab focused on designing,
configuring, testing, and validating Conditional Access policies in a
simulated enterprise environment.

The objective was to demonstrate practical identity and access management
skills while following a safe deployment methodology. Conditional Access
policies were configured in **Report-only** mode so that policy behavior
could be evaluated without unintentionally blocking administrative or
test-account access.

The lab included:

- Multifactor authentication requirements
- Administrative access protection
- Legacy authentication blocking
- Location-based access controls
- Device-platform restrictions
- Administrative portal protection
- Device code authentication restrictions
- Named trusted locations
- Conditional Access What If testing
- Sign-in log investigation
- Conditional Access reporting
- Audit log validation

---

# Conditional Access Deployment Strategy

Conditional Access policies can affect access across an entire Microsoft
Entra environment. Incorrectly configured policies can prevent legitimate
users or administrators from accessing organizational resources.

For this reason, the policies in this lab were deployed using a controlled
process:

1. Create dedicated test users and groups.
2. Limit policy assignments to intended identities.
3. Configure policy conditions and access controls.
4. Set the policy to **Report-only**.
5. Validate expected behavior with the Conditional Access What If tool.
6. Review sign-in logs and Conditional Access evaluation results.
7. Review Microsoft Entra audit logs for administrative changes.
8. Document the policy configuration and validation results.

This approach demonstrates a staged deployment methodology that reduces
the risk of accidental account lockout.

---

# Test Environment

Conditional Access testing was performed using dedicated test identities
and groups.

Test identities included:

- CA Test User
- CA Test Admin

A dedicated security group was used for policy targeting:

`SG-CA-Test-Users`

Using dedicated test identities allowed Conditional Access behavior to be
evaluated without broadly affecting other tenant users.

---

# Conditional Access Policies

The completed environment contained a baseline policy and seven additional
Conditional Access policies.

## Baseline Policy — Require MFA and Compliant Device

Policy:

`CA-Require-MFA-and-Compliant-Device`

Purpose:

Establish a baseline policy requiring stronger authentication and device
compliance for Windows access.

Configuration included:

- Selected identities
- All resources
- Windows device platform
- Require multifactor authentication
- Require device to be marked as compliant
- Report-only deployment

This policy demonstrated how authentication requirements and
device-compliance controls can be combined within Conditional Access.

---

## CA001 — Require MFA for Test Users

Policy:

`CA001-Require-MFA-Test-Users`

Purpose:

Require multifactor authentication for users assigned to the Conditional
Access test group.

Configuration:

- Target: `SG-CA-Test-Users`
- Resources: All resources
- Grant control: Require multifactor authentication
- State: Report-only

### Validation

The policy was evaluated through both Conditional Access testing and
Microsoft Entra sign-in logs.

A successful test-user sign-in showed that the authentication requirement
was multifactor authentication.

The sign-in details also showed that the MFA requirement had been
satisfied by an existing claim in the authentication token.

The Conditional Access Report-only results showed:

`CA001-Require-MFA-Test-Users — Report-only: Success`

This provided direct evidence that the policy matched the test sign-in as
intended.

---

## CA002 — Block Legacy Authentication

Policy:

`CA002-Block-Legacy-Authentication`

Purpose:

Prevent authentication through legacy client types that do not support
modern authentication protections.

Configuration included:

- Test group assignment
- All resources
- Exchange ActiveSync clients
- Other legacy clients
- Block access
- Report-only deployment

Blocking legacy authentication is an important identity-security control
because older authentication methods may not support modern controls such
as MFA.

The policy was maintained in Report-only mode during testing to evaluate
its impact before enforcement.

---

## CA003 — Require MFA for Administrators

Policy:

`CA003-Require-MFA-Admins`

Purpose:

Apply stronger authentication requirements to privileged administrative
roles.

The policy targeted multiple administrative roles and required multifactor
authentication.

Configuration included:

- Six administrative roles
- All resources
- Require multifactor authentication
- Report-only deployment

Administrative accounts represent high-value targets because compromise of
a privileged identity can provide broad access to organizational
resources.

Requiring MFA provides an additional layer of protection for privileged
access.

---

# Named Location Configuration

A trusted named location was created:

`Trusted-Corporate-Network`

The lab used the documentation IP range:

`203.0.113.0/24`

The location was marked as trusted.

This named location was then used to demonstrate location-based
Conditional Access decisions.

Using a named location makes it possible to differentiate between trusted
organizational networks and access originating from other locations.

---

## CA004 — Block Access Outside Trusted Location

Policy:

`CA004-Block-Access-Outside-Trusted-Location`

Purpose:

Demonstrate location-based access restrictions.

Configuration included:

- Target: Conditional Access test users
- Resources: All resources
- Network/location condition
- Trusted corporate network excluded
- Block access
- Report-only deployment

### Outside Trusted Location Test

A What If evaluation was performed using an address outside the configured
trusted network.

The resulting evaluation showed that CA004 would apply and that the
resulting grant control would be:

`Block access`

This demonstrated that access originating outside the trusted location
matched the policy.

### Trusted Location Test

A second What If evaluation used an address inside:

`203.0.113.0/24`

The evaluation showed that CA004 did not apply because of the location
condition.

This demonstrated both sides of the policy logic:

- Untrusted location → policy applies
- Trusted location → policy excluded

Testing both matching and non-matching conditions provided stronger
evidence than testing only a single scenario.

---

## CA005 — Block Unsupported Device Platforms

Policy:

`CA005-Block-Unsupported-Device-Platforms`

Purpose:

Demonstrate Conditional Access controls based on the device platform used
to access organizational resources.

Configuration included:

- Conditional Access test group
- All resources
- Device-platform condition
- Supported platform exclusion
- Block access
- Report-only deployment

### What If Validation

The policy was evaluated using a macOS device-platform scenario.

The What If results showed:

`CA005-Block-Unsupported-Device-Platforms`

under the policies that would apply.

The resulting grant control was:

`Block access`

The policy remained in:

`Report-only`

This validated that an unsupported device platform matched the intended
access restriction.

The What If results were also reviewed to identify policies that did not
apply to the simulated authentication scenario.

---

## CA006 — Require MFA for Admin Portals

Policy:

`CA006-Require-MFA-Admin-Portals`

Purpose:

Protect access to Microsoft administrative portals with multifactor
authentication.

Configuration included:

- Selected test identities
- Microsoft Admin Portals resource
- Require multifactor authentication
- Report-only deployment

Administrative portals provide access to sensitive configuration and
management capabilities.

Requiring MFA for administrative portal access reduces the risk associated
with compromised passwords.

### Validation Limitation

The policy configuration was successfully verified through the Conditional
Access Policy Details interface.

During What If testing, the Microsoft Admin Portals resource was not
exposed in the resource selector in a way that allowed a reliable
equivalent test to be performed.

Rather than selecting an unrelated resource and creating misleading
validation evidence, the What If test was omitted for this policy.

The final policy configuration was retained as the supporting evidence.

---

## CA007 — Block Device Code Authentication

Policy:

`CA007-Block-Device-Code-Authentication`

Purpose:

Demonstrate protection against authentication scenarios using the device
code flow.

Configuration included:

- Conditional Access test identities
- All resources
- Authentication flow condition
- Device code flow
- Block access
- Report-only deployment

### What If Validation

A What If evaluation was performed using:

- CA Test User
- Microsoft Intune
- Windows
- Browser
- Device code flow

The resulting Conditional Access evaluation showed:

`CA007-Block-Device-Code-Authentication`

under the policies that would apply.

The grant control was:

`Block access`

The policy state remained:

`Report-only`

This demonstrated that the device code authentication condition was
correctly detected by Conditional Access.

The policies that did not apply were also reviewed to demonstrate how
multiple Conditional Access policies are evaluated against the same
authentication scenario.

---

# What If Testing

The Microsoft Entra Conditional Access What If tool was used throughout
the lab.

What If testing made it possible to simulate authentication scenarios
without requiring each condition to occur during an actual user sign-in.

Variables tested included:

- User identity
- Target resource
- Device platform
- Client application
- Network location
- IP address
- Authentication flow

The results were reviewed in two categories:

### Policies That Will Apply

These policies matched the simulated authentication scenario.

### Policies That Will Not Apply

These policies did not match one or more conditions.

Reviewing both categories helped identify exactly why policies were or
were not evaluated for a particular authentication attempt.

---

# Sign-In Log Validation

Microsoft Entra sign-in logs were used to review authentication activity
from the Conditional Access test accounts.

The logs provided information such as:

- User
- Application
- Authentication requirement
- Sign-in status
- Conditional Access evaluation
- MFA result
- Date and time

One successful CA Test User sign-in showed:

- Application: Azure Portal
- Authentication requirement: Multifactor authentication
- Status: Success
- MFA requirement satisfied by a claim in the token

The Report-only Conditional Access results showed CA001 successfully
matching the sign-in.

Other policies appeared as not applied when their assignment or conditions
did not match the authentication event.

This demonstrated the ability to distinguish between:

- Authentication success
- MFA satisfaction
- Conditional Access policy matching
- Policies excluded because their conditions were not met

---

# Audit Log Validation

Microsoft Entra audit logs were reviewed after Conditional Access
configuration.

The audit logs provided an administrative record of changes performed
within the tenant.

Audit evidence included activity associated with creating Conditional
Access policies.

A detailed audit event was reviewed for:

`CA007-Block-Device-Code-Authentication`

The activity type showed:

`Add conditional access policy`

The audit event provided evidence that the policy creation operation was
recorded by Microsoft Entra.

Modified-property information was also reviewed where available to examine
the configuration recorded as part of the administrative change.

This demonstrates the importance of audit logging for:

- Administrative accountability
- Change tracking
- Security investigations
- Troubleshooting
- Configuration validation

---

# Risk-Based Conditional Access Licensing Limitation

A risk-based Conditional Access policy was considered during the lab.

The intended policy would have required MFA for medium- and high-risk
sign-ins.

However, the tenant did not expose the Sign-in risk condition within
Conditional Access.

Because risk-based Conditional Access capabilities depend on additional
Microsoft Entra ID Protection licensing, the policy was not artificially
recreated using unrelated conditions.

Instead, the limitation was documented and the lab continued with
Conditional Access controls supported by the available environment.

This demonstrates an important real-world administration skill:
identifying licensing or feature limitations and adapting the
implementation without misrepresenting available functionality.

---

# Report-Only Deployment

All Conditional Access policies created during this portion of the lab
were maintained in:

`Report-only`

Report-only mode allows administrators to evaluate how a policy would
affect authentication without actively enforcing the policy.

This is especially useful when:

- Introducing new Conditional Access policies
- Testing broad assignments
- Evaluating administrative access policies
- Testing location restrictions
- Evaluating device restrictions
- Preventing accidental lockouts
- Reviewing policy interaction before production deployment

A production deployment could follow a staged process such as:

`Create → Report-only → Validate → Pilot → Monitor → Enforce`

This lab intentionally stopped at the validation stage rather than
enabling policies in a production-like tenant without a formal rollout and
rollback plan.

---

# Security and Privacy Considerations

Screenshots intended for the public GitHub repository were reviewed for
unnecessary sensitive information.

Real sign-in IP addresses were removed or cropped where they were not
required to demonstrate the technical objective.

Documentation-only IP ranges were retained when they were part of the
Conditional Access testing scenario.

For example:

`203.0.113.0/24`

was used to represent the trusted corporate network during the
named-location exercise.

This keeps the portfolio evidence technically useful while reducing
unnecessary exposure of environment information.

---

# Skills Demonstrated

This portion of the lab demonstrates practical experience with:

- Microsoft Entra ID
- Identity and Access Management
- Conditional Access
- Multifactor Authentication
- Administrative access protection
- Legacy authentication controls
- Device-based access controls
- Location-based access controls
- Authentication flow restrictions
- Named locations
- Conditional Access What If
- Sign-in log analysis
- Audit log analysis
- Report-only deployment
- Policy troubleshooting
- Security testing
- Licensing awareness
- Change validation
- Technical documentation

---

# Key Takeaways

Conditional Access is most effective when policies are designed, tested,
and monitored as part of a controlled deployment process.

This lab demonstrated that creating a policy is only one part of
Conditional Access administration.

A complete implementation also requires:

- Understanding the security objective
- Selecting appropriate identities and resources
- Configuring relevant conditions
- Choosing the correct access control
- Preventing administrative lockout
- Testing expected policy behavior
- Reviewing non-applicable policies
- Investigating sign-in results
- Reviewing audit activity
- Understanding licensing limitations
- Documenting the final configuration

The combination of policy configuration, What If testing, sign-in
analysis, and audit-log review provides a more complete demonstration of
Microsoft Entra Conditional Access administration than policy creation
alone.

---

# Screenshot Evidence

The following screenshots document the Conditional Access configuration,
testing, validation, and monitoring performed during this lab.

## Baseline and Policy Configuration

| Screenshot | Evidence |
|---|---|
| `01-Require-MFA-Policy-Configuration.png` | Initial Conditional Access
MFA policy configuration |
| `01-CA-Require-MFA-and-Compliant-Device-Policy-Details.png` | Baseline
policy details showing MFA and compliant-device requirements |
| `02-CA001-Require-MFA-Test-Users-Policy-Details.png` | CA001 policy
details showing MFA requirements for the Conditional Access test-user
group |
| `03-Block-Legacy-Authentication-Grant.png` | Legacy authentication
policy grant control configured to block access |
| `04-CA002-Block-Legacy-Authentication-Policy-Details.png` | CA002 policy
details showing legacy authentication restrictions |
| `05-CA003-Require-MFA-Admins-Policy-Details.png` | CA003 policy details
showing MFA requirements for administrative roles |

## MFA and Sign-In Validation

| Screenshot | Evidence |
|---|---|
| `06-What-If-MFA-Policy-Evaluation.png` | Conditional Access What If
evaluation of MFA policy behavior |
| `07-What-If-Policies-Not-Applied.png` | What If results showing
Conditional Access policies that did not match the simulated sign-in |
| `08-Sign-In-Logs-Test-Accounts.png` | Microsoft Entra sign-in activity
generated by Conditional Access test accounts |
| `09-Sign-In-MFA-Success.png` | Successful test-account authentication
showing MFA satisfaction |
| `10-Sign-In-Interrupted-Expired-Password.png` | Authentication
troubleshooting example involving an interrupted sign-in and expired
password |
| `11-CA001-Report-Only-Test-User-Evaluation.png` | CA001 Report-only
evaluation for the Conditional Access test user |
| `12-CA001-Report-Only-Success.png` | Sign-in evidence showing CA001
successfully matching in Report-only mode |

## Named Location and Location-Based Access

| Screenshot | Evidence |
|---|---|
| `13-Trusted-Corporate-Network-Named-Location.png` | Trusted named
location representing the simulated corporate network |
| `14-CA004-Block-Access-Outside-Trusted-Location-Policy-Details.png` |
CA004 configuration showing location-based access restrictions |
| `15-What-If-CA004-Outside-Trusted-Location.png` | What If validation
showing CA004 applying outside the trusted corporate location |
| `16-What-If-CA004-Trusted-Location-Excluded.png` | What If validation
showing CA004 excluded when the simulated sign-in originates from the
trusted location |

## Device Platform Restrictions

| Screenshot | Evidence |
|---|---|
| `17-CA005-Block-Unsupported-Device-Platforms-Policy-Details.png` | CA005
configuration restricting unsupported device platforms |
| `18-What-If-CA005-Unsupported-Device-Blocked.png` | What If validation
showing the unsupported device platform matching CA005 and resulting in
Block access |
| `19-What-If-CA005-Policy-Evaluation.png` | Additional CA005 What If
evaluation showing applicable and non-applicable policy behavior |

## Administrative Portal Protection

| Screenshot | Evidence |
|---|---|
| `20-CA006-Require-MFA-Admin-Portals-Policy-Details.png` | CA006
configuration requiring MFA for Microsoft administrative portal access |

## Device Code Authentication Protection

| Screenshot | Evidence |
|---|---|
| `21-CA007-Block-Device-Code-Authentication-Policy-Details.png` | CA007
configuration blocking device code authentication |
| `22-What-If-CA007-Device-Code-Flow-Blocked.png` | What If validation
showing Device code flow matching CA007 and resulting in Block access |
| `23-What-If-CA007-Policies-Not-Applied.png` | Review of other
Conditional Access policies that did not match the CA007 authentication
scenario |

## Final Policy and Audit Evidence

| Screenshot | Evidence |
|---|---|
| `24-Conditional-Access-Final-Policy-Overview.png` | Final Conditional
Access inventory showing all completed policies maintained in Report-only
mode |
| `25-Entra-ID-Audit-Logs-Directory-Activity.png` | Microsoft Entra
audit-log activity associated with identity and policy administration |
| `26-Audit-Log-CA007-Policy-Creation-Success.png` | Audit event showing
successful creation of CA007 |
| `27-Audit-Log-CA007-Policy-Modified-Properties.png` | Modified-property
audit evidence associated with the CA007 policy creation event |

## Evidence Summary

The Conditional Access evidence demonstrates the full administrative
workflow:

**Configure → Report-only → Simulate → Validate → Investigate → Audit
→ Document**

The evidence includes policy configuration, What If simulation,
authentication investigation, named-location testing, device-platform
controls, authentication-flow restrictions, sign-in log analysis, and
administrative audit tracking.

All screenshots intended for the public repository were reviewed to remove
unnecessary personal information or real network details when those values
were not required to demonstrate the technical objective.
