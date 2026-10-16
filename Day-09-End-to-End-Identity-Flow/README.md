# Day 9 — End-to-End Identity Flow

## Objective

Understand how authentication, authorization, SSO, federation, MFA, sessions, tokens, claims, and identity lifecycle work together in a real enterprise identity flow.

## Topics Covered

- End-to-end identity flow
- Identity Provider (IdP)
- Service Provider (SP)
- SSO
- Federation
- SAML
- SAML assertions
- Authentication vs Authorization
- MFA and authentication assurance
- Sessions
- Tokens and claims
- SSO troubleshooting
- IAM lifecycle

---

## 1. End-to-End Identity Flow

Typical enterprise identity flow:

User → Identity Provider (IdP) → Authentication + MFA → SAML/OIDC Assertion or Token → Application/SP → Authorization → Resource Access

---

## 2. Main Actors

### User
The person attempting to access an application or resource.

### Identity Provider (IdP)
The system responsible for authenticating the user and providing identity information.

Examples:
- Microsoft Entra ID
- Okta
- Keycloak

### Service Provider (SP)
The application or service the user wants to access.

Examples:
- Salesforce
- ServiceNow
- Enterprise applications

### Resource
The actual data, application function, API, or system the user wants to access.

---

## 3. SSO Flow

Example:

1. User attempts to access an application.
2. Application redirects the user to the IdP.
3. User authenticates with the IdP.
4. MFA may be required.
5. IdP issues a SAML response/assertion or other protocol message.
6. Application validates the response.
7. Application identifies the user.
8. Application applies authorization.
9. Access is granted or denied.

---

## 4. Authentication vs Authorization

### Authentication

Answers:

> Who are you?

### Authorization

Answers:

> What are you allowed to do?

A successful login does not automatically mean the user has permission to perform every action.

Example:

Authentication → Successful  
Authorization → Failed  
Result → Access Denied

---

## 5. SAML Assertion

A SAML assertion is information issued by the IdP and consumed by the application.

It can contain:

- Authentication information
- User attributes
- Identity/subject information
- Other statements used by the application

SAML responses/assertions are commonly protected with digital signatures in enterprise deployments so the receiving application can verify their origin and integrity.

---

## 6. MFA and Authentication Assurance

MFA adds additional authentication factors.

Example:

Password + Authenticator App → Stronger Authentication → Application Access

Authentication context can influence access decisions, especially when stronger authentication is required for sensitive resources.

---

## 7. Sessions

After successful authentication, an application may establish a session.

Authentication → Session Established → User Requests Resources → Application Checks Session → Authorization

A session allows the user to continue interacting with the application without repeatedly performing the complete authentication process.

---

## 8. Tokens and Claims

Tokens can carry information between systems depending on the protocol and architecture.

Claims are pieces of information contained in tokens or assertions.

Examples:

- User ID
- Email
- Groups
- Roles
- Authentication information
- Other attributes

Applications can use relevant claims as inputs to their authorization logic.

---

## 9. Password Handling in SSO

In a typical federated SSO architecture:

User → IdP → Authentication → Assertion/Token → Application

The application does not normally receive the user's IdP password.

This allows authentication and security controls to be centralized at the IdP.

---

## 10. Common SSO Failure Points

When SSO fails, investigate:

- IdP authentication failure
- MFA failure
- Incorrect application configuration
- Invalid SAML response/assertion
- Signature validation failure
- Incorrect issuer
- Incorrect audience
- Incorrect redirect/ACS configuration
- Incorrect claims/attributes
- User not provisioned in the application
- Incorrect group/role mapping
- Authorization failure
- Expired or invalid session

---

## 11. SSO Troubleshooting Example

### Problem

User can successfully log in to the corporate IdP but receives "Access Denied" in an application.

### Investigation

1. Was authentication successful?
2. Was the SSO response accepted?
3. Was the correct user identified?
4. Was the user provisioned?
5. Were the correct claims/groups sent?
6. Were groups mapped to the correct application role?
7. Does the user have the required permission?
8. Is there a session or token issue?

Key point:

> Successful authentication does not guarantee authorization.

---

## 12. IAM Lifecycle Connection

JML connects with the overall identity lifecycle:

Joiner → Identity Created → Account Provisioned → Authentication → Authorization → Access Review → Mover → Access Updated → Leaver → Access Removed/Disabled

IAM is not only about login. It also covers the identity and access lifecycle.

---

## Key Takeaways

- The IdP authenticates the user.
- The SP/application consumes identity information and enforces application access.
- SSO allows users to access multiple applications without repeatedly authenticating.
- Federation establishes trust between separate identity/security domains.
- SAML can carry authentication and attribute information between systems.
- MFA strengthens authentication.
- Authentication and authorization are separate decisions.
- Sessions maintain an authenticated interaction.
- Tokens/assertions can carry claims.
- Successful IdP login does not guarantee application access.
- SSO troubleshooting should follow the identity flow from authentication → federation → provisioning → claims → authorization.

