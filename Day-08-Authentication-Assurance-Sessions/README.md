# Day 8 — Authentication Assurance & Sessions

## Objective

Understand authentication assurance, sessions, tokens, session management, and step-up authentication in IAM.

## Topics Covered

- Authentication assurance
- Authentication factors
- Sessions
- Session cookies
- Credentials vs sessions
- Tokens
- Access tokens
- ID tokens
- Session lifetime
- Token expiration
- Session revocation
- Session hijacking
- Step-up authentication
- Authentication and authorization flow
- IAM troubleshooting

## Authentication Assurance

Authentication answers:

> Who are you?

Authentication assurance considers how much confidence the authentication process provides that the claimed identity is genuine.

Examples:

- Password authentication
- Password + MFA
- Phishing-resistant authentication such as passkeys/security keys

Higher assurance generally requires stronger authentication and/or additional controls.

## Authentication vs Authentication Assurance

Authentication determines whether the identity was successfully authenticated.

Authentication assurance considers the strength and reliability of that authentication process.

Successful authentication does not automatically mean strong authentication.

## Session

A session represents an ongoing authenticated interaction between a user/client and a service.

Basic flow:

```text
Login
  ↓
Authentication
  ↓
Session Established
  ↓
Multiple Requests
  ↓
Session Ends/Expires

Session Cookie
A web application can use a session cookie to associate subsequent requests with an authenticated session.
Simplified flow:
User
  ↓
Login
  ↓
Authentication
  ↓
Session Created
  ↓
Session Identifier
  ↓
Browser Requests
  ↓
Server Identifies Session

Credential vs Session
Credential:
- Used to prove or establish identity
- Examples: password, passkey, security key
Session:
- Represents an ongoing authenticated interaction


Tokens
A token is a security artifact issued by an authentication or authorization system.
Different tokens have different purposes.
Examples:
- OAuth access tokens
- OpenID Connect ID tokens
- SAML assertions
- Cloud temporary credentials


Access Token
An access token is generally used by a client to access a protected resource or API.
Client
  ↓
Authorization Server
  ↓
Access Token
  ↓
Protected API

ID Token
An ID token is defined by OpenID Connect and provides authentication-related information about the user to the OIDC client.
Common claims include:
- sub
- iss
- aud
- iat
- exp
An ID token should not generally be used as an API access token.


Session Lifetime
Sessions can have controls such as:
- Idle timeout
- Absolute lifetime
- Reauthentication
- Token expiration
These controls can reduce the period during which a stolen session or token can be abused.
Session Revocation
When an account is compromised or access needs to be terminated, organizations may revoke sessions or tokens where supported and require reauthentication.


Session Hijacking
Session hijacking occurs when an attacker obtains control of a valid authenticated session.
Potential protections include:
- HTTPS/TLS
- Secure cookie settings
- Appropriate session lifetime
- Reauthentication for sensitive operations
- MFA/step-up authentication
- Session/token revocation
- XSS and CSRF protections where applicable

Step-Up Authentication
Step-up authentication requires additional authentication when a user attempts a sensitive operation or accesses a sensitive resource.

Example:
Normal Session
      ↓
Sensitive Application
      ↓
Additional Authentication
      ↓
Access Granted

Authentication → Session → Authorization


Authentication
      ↓
Identity Verified
      ↓
Session / Token Established
      ↓
Authorization
      ↓
Permission Evaluation
      ↓
Allow / Deny
      ↓
Resource


IAM Troubleshooting
When a user repeatedly gets asked to authenticate, check:
1. Authentication success/failure
2. Session establishment
3. Token issuance
4. Token/session expiration
5. Authentication assurance requirements
6. Conditional access policies
7. Authorization permissions
8. Application and identity-provider logs


Key Takeaways
- Authentication verifies identity.
- Authentication assurance considers the strength of authentication.
- A session represents an ongoing authenticated interaction.
- Credentials and sessions are different concepts.
- Access tokens and ID tokens have different purposes.
- Sessions and tokens can expire.
- Sessions/tokens may need to be revoked during security incidents.
- Step-up authentication provides stronger authentication for sensitive operations.
- Authentication does not automatically grant authorization.