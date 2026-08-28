# Microsoft Entra ID Troubleshooting

## Overview

This section documents troubleshooting methods used throughout the
Microsoft Entra ID IAM and Security Lab.

Identity problems can originate from multiple layers including passwords,
authentication registration, group membership, administrative roles,
Conditional Access, device conditions, applications, sessions, or
licensing.

The lab emphasized evidence-driven troubleshooting using Microsoft Entra
administrative tools rather than relying only on configuration
assumptions.

---

# Troubleshooting Methodology

The general troubleshooting workflow used during the project was:

**Identify → Reproduce → Investigate → Isolate → Correct → Validate
→ Document**

This method provides a structured approach to identity and authentication
problems.

---

# Authentication Registration Issue

During authentication setup, an MFA registration session expired.

This represented a realistic end-user support scenario.

Possible causes for authentication registration issues can include:

- Session expiration
- Interrupted setup
- Authentication-method configuration
- Network interruption
- Browser session problems
- User authentication state

The solution process involves restarting or continuing the registration
process and confirming that the authentication method is successfully
registered.

---

# Expired Password Sign-In

A test sign-in produced an interrupted authentication result associated
with an expired password.

Microsoft Entra sign-in logs were reviewed to investigate the event.

This demonstrated the importance of distinguishing between:

- Failed authentication
- Interrupted authentication
- Successful authentication
- Conditional Access blocking

An interrupted sign-in does not always mean that a security policy blocked
access.

---

# Conditional Access Troubleshooting

Conditional Access can produce complex authentication behavior because
multiple policies can be evaluated during the same sign-in.

The lab used the Conditional Access What If tool to determine:

- Which policies would apply
- Which policies would not apply
- Why a policy matched
- Why a policy did not match
- Which grant control would result

This provided a safer method for troubleshooting before enforcing
policies.

---

# Policies That Will Apply

The What If tool displayed policies matching the simulated authentication
conditions.

Matching factors can include:

- User
- Group membership
- Application
- Device platform
- Location
- Authentication flow
- Administrative role

Understanding the matching conditions helps administrators determine why a
policy affects a particular user.

---

# Policies That Will Not Apply

Policies that did not match were also reviewed.

This is important because a policy not applying may indicate:

- User not targeted
- Group not targeted
- Application mismatch
- Device platform mismatch
- Named location exclusion
- Authentication-flow mismatch
- Policy exclusion

Reviewing non-applied policies is often as useful as reviewing applied
policies.

---

# Group Membership Troubleshooting

Conditional Access policies targeted security groups.

If an expected policy did not apply, group membership was one of the first
items to verify.

The troubleshooting process included checking:

1. User identity
2. Group assignment
3. Policy inclusion
4. Policy exclusion
5. Conditional Access conditions
6. Policy state

---

# MFA Troubleshooting

When troubleshooting MFA, administrators should review multiple layers.

These include:

- Authentication method enabled for the user
- User registration status
- Microsoft Authenticator setup
- Conditional Access MFA requirement
- Existing MFA claims
- Authentication session state
- Sign-in log authentication details

One successful sign-in demonstrated that an MFA requirement could already
be satisfied by an MFA claim contained in the authentication token.

---

# RBAC Troubleshooting

Administrative access was tested after Microsoft Entra roles were
assigned.

If an administrator cannot perform an expected action, troubleshooting
should include:

- Confirming the correct user
- Confirming assigned directory role
- Reviewing role permissions
- Confirming the targeted administrative resource
- Signing out and signing back in if required
- Testing both allowed and restricted operations

Permission validation helps distinguish expected least-privilege behavior
from actual access problems.

---

# Sign-In Log Investigation

Microsoft Entra sign-in logs were used as a primary troubleshooting
resource.

Useful fields include:

- User
- Application
- Status
- Authentication requirement
- MFA details
- Conditional Access result
- Device information
- Location
- Failure information

These logs provide evidence of what occurred during authentication.

---

# Audit Log Investigation

Audit logs were used to investigate administrative activity.

Audit data can help answer questions such as:

- Was the policy created?
- Was the policy modified?
- Who initiated the change?
- Was the operation successful?
- Which object was affected?

This is especially useful when investigating unexpected configuration
changes.

---

# Licensing Troubleshooting

Not all missing Microsoft Entra features indicate configuration errors.

During the lab, Sign-in risk was not available as a Conditional Access
condition.

The issue was identified as a licensing or feature-availability limitation
rather than a configuration failure.

This distinction is important in Microsoft cloud support.

---

# Common Troubleshooting Decision Tree

When a user cannot access a Microsoft resource:

### Step 1 — Verify Identity

Confirm the correct account is being used.

### Step 2 — Verify Password State

Check for expired or reset-password requirements.

### Step 3 — Verify Authentication Methods

Confirm the user has the required MFA method registered.

### Step 4 — Verify Group Membership

Check whether the user belongs to groups targeted by security policies.

### Step 5 — Review Conditional Access

Use What If and sign-in logs to determine policy behavior.

### Step 6 — Review RBAC

If the issue involves administration, verify the assigned Microsoft Entra
role.

### Step 7 — Review Sign-In Logs

Identify success, failure, interruption, MFA, and Conditional Access
results.

### Step 8 — Review Audit Logs

Check whether recent administrative changes affected access.

### Step 9 — Check Licensing

Determine whether the requested feature is available in the tenant.

### Step 10 — Retest

Repeat the original scenario and verify the outcome.

---

# Evidence

Troubleshooting evidence is stored in:

`Screenshots/Troubleshooting/`

Current screenshot:

- `01-MFA-Registration-Session-Expired.png`

Additional troubleshooting evidence is included in:

`Screenshots/Conditional-Access/`

Relevant screenshots include:

- `07-What-If-Policies-Not-Applied.png`
- `10-Sign-In-Interrupted-Expired-Password.png`
- `11-CA001-Report-Only-Test-User-Evaluation.png`
- `15-What-If-CA004-Outside-Trusted-Location.png`
- `16-What-If-CA004-Trusted-Location-Excluded.png`
- `18-What-If-CA005-Unsupported-Device-Blocked.png`
- `23-What-If-CA007-Policies-Not-Applied.png`

---

# Skills Demonstrated

This portion of the project demonstrates:

- Identity troubleshooting
- MFA troubleshooting
- Password troubleshooting
- Conditional Access troubleshooting
- What If analysis
- Sign-in log investigation
- Audit-log investigation
- RBAC troubleshooting
- Group membership validation
- Licensing investigation
- Root-cause analysis
- Technical documentation

---

# Key Takeaways

Microsoft Entra troubleshooting requires administrators to investigate
multiple layers of identity and access.

A sign-in problem may originate from the user's password, authentication
method, group membership, Conditional Access policy, administrative role,
session state, or licensing.

Using What If, sign-in logs, audit logs, and controlled testing provides a
repeatable method for identifying the actual cause of identity and access
problems.
