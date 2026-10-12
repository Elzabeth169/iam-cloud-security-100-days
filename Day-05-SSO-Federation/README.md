# Day 5 — SSO & Federation

## Objective

Understand Single Sign-On (SSO), Identity Providers, Service Providers, identity federation, and how authentication information is exchanged between enterprise applications.

## Topics Covered

- Single Sign-On (SSO)
- Identity Provider (IdP)
- Service Provider (SP)
- Identity Federation
- SSO vs Federation
- SAML
- SAML Assertions
- SP-Initiated SSO
- IdP-Initiated SSO
- JIT Provisioning
- SSO and Authorization
- SSO Security Considerations
- SSO Troubleshooting

---

## 1. What is SSO?

Single Sign-On (SSO) allows a user to authenticate once with a trusted Identity Provider and access multiple applications without separately authenticating to each application.

```text
User
 ↓
Identity Provider
 ↓
Authentication
 ↓
Multiple Applications

SSO improves user experience and allows centralized authentication controls.

2. Identity Provider (IdP)
An Identity Provider is a system responsible for authenticating users and providing identity information to applications.

Examples:
- Microsoft Entra ID
- Okta
- Google Identity
- AD FS

The IdP can handle:
- Authentication
- MFA
- Password policies
- Conditional Access
- Session management
- Identity information

3. Service Provider (SP)
A Service Provider is the application or service that the user wants to access.
Example:
IdP → Microsoft Entra ID
SP  → Salesforce

The application trusts the IdP to authenticate the user.


4. Basic SSO Flow
User
 ↓
Application
 ↓
Redirect to Identity Provider
 ↓
User authenticates
 ↓
IdP verifies identity
 ↓
Authentication information sent to application
 ↓
Application validates it
 ↓
User gets access

5. Identity Federation
Identity federation is a trust relationship that allows identities authenticated by one Identity Provider or organization to be recognized by another system or organization.
Company A
    ↓
Company A Identity Provider
    ↓
Federation / Trust
    ↓
Company B Application

The application trusts the external Identity Provider to authenticate the user.

6. SSO vs Federation
SSO
Focuses on:
Authenticate once and access multiple applications.

Federation
Focuses on:
Establishing trust between identity systems or domains.

SSO       → Single authentication experience
Federation → Trust between identity systems

Federation can enable SSO, but SSO and federation are not the same thing.


7. SAML
SAML stands for:
Security Assertion Markup Language
SAML is a protocol commonly used for enterprise SSO and federation.
Example:
Microsoft Entra ID
        ↓
      SAML
        ↓
    Salesforce

SAML allows the Identity Provider to communicate authentication and identity information to the application.


8. SAML Assertion
A SAML assertion is a digitally signed XML-based statement from the Identity Provider containing information about the authenticated user and/or authentication event.

It may contain information such as:
- Username
- Email
- Name
- Groups
- Roles
- Authentication information

Basic flow:
IdP
 ↓
Authenticates user
 ↓
Creates SAML Assertion
 ↓
Signs Assertion
 ↓
Sends to Application
 ↓
Application validates Assertion
 ↓
User authenticated


9. Why is the SAML Assertion Signed?
The digital signature allows the application to verify that the assertion came from the trusted Identity Provider and has not been modified.
IdP
 ↓
SAML Assertion
 ↓
Digital Signature
 ↓
Application
 ↓
Signature Verification
 ↓
Trusted Assertion

10. SP-Initiated SSO
The user starts from the application.
User
 ↓
Application
 ↓
Identity Provider
 ↓
Authentication
 ↓
Application
 ↓
Access

Example:
User opens Salesforce
        ↓
Salesforce redirects to Entra ID
        ↓
User authenticates
        ↓
User returns to Salesforce


11. IdP-Initiated SSO
The user starts from the Identity Provider.
User
 ↓
Identity Provider Portal
 ↓
Select Application
 ↓
Application
 ↓
Access

Example:
Employee
 ↓
Microsoft Entra My Apps
 ↓
Salesforce


12. Just-In-Time (JIT) Provisioning

JIT provisioning can create a user account in an application when the user first logs in through the trusted Identity Provider.
Employee
 ↓
SSO
 ↓
IdP authenticates user
 ↓
Application receives identity information
 ↓
No local account exists
 ↓
Application creates account
 ↓
User gets access


13. SSO Does Not Automatically Mean Authorization
Authentication and authorization are separate.
Authentication
 ↓
Who are you?
 ↓
Identity confirmed
 ↓
Authorization
 ↓
What are you allowed to do?
 ↓
Allow / Deny

A user can successfully authenticate through SSO but still be denied access because of:
- Missing application assignment
- Incorrect role
- Missing group membership
- Insufficient permissions
- Application-side authorization rules


14. SSO Security Considerations
SSO provides centralized authentication, but the Identity Provider becomes a critical security control point.
If the IdP account is compromised:
Compromised IdP Account
        ↓
SSO
        ↓
Multiple Applications

Organizations therefore protect the IdP using:
- MFA
- Phishing-resistant authentication
- Conditional Access
- Risk-based authentication
- Privileged access controls
- Monitoring
- Session controls
- Least privilege


15. SSO + Passwordless
SSO and passwordless authentication can work together.
Employee
 ↓
Enterprise Application
 ↓
Identity Provider
 ↓
Passkey / MFA
 ↓
Authentication
 ↓
SSO
 ↓
Multiple Applications

This provides a strong authentication experience while reducing dependence on passwords.


16. SSO Troubleshooting
If a user cannot access an application through SSO:
1. Check whether the user can authenticate to the IdP.
2. Check MFA or Conditional Access requirements.
3. Check application assignment.
4. Check group membership and roles.
5. Check provisioning status.
6. Check SAML/OIDC configuration.
7. For SAML, check:
   - Issuer
   - Audience
   - Signature
   - Certificate
   - Assertion
   - Timestamps
8. Check application-side permissions.
9. Check IdP and application logs.


Key Takeaways
- SSO allows users to authenticate once and access multiple applications.
- The Identity Provider performs authentication.
- The Service Provider is the application relying on the IdP.
- Federation establishes trust between identity systems.
- SAML is a protocol commonly used for enterprise SSO and federation.
- A SAML assertion contains identity/authentication information and is digitally signed.
- SSO can be SP-initiated or IdP-initiated.
- JIT provisioning can create application accounts during first login.
- Authentication does not automatically grant authorization.
- The IdP is a critical security control point.
- SSO, MFA, passkeys, and federation can work together.


Interview Questions
1. What is SSO?
2. What is an Identity Provider?
3. What is a Service Provider?
4. What is identity federation?
5. What is the difference between SSO and federation?
6. What is SAML?
7. What is a SAML assertion?
8. Why is a SAML assertion digitally signed?
9. Explain SP-initiated SSO.
10. Explain IdP-initiated SSO.
11. What is JIT provisioning?
12. Does successful SSO authentication automatically give authorization?
13. What would you check if SSO authentication succeeds but the user cannot access the application?
14. What happens if the central Identity Provider is compromised?
15. How do MFA and passwordless authentication work with SSO?