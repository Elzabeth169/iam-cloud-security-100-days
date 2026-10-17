# Day 10 — IAM Fundamentals Checkpoint

## Objective

Review Days 1–9 and test understanding of core IAM concepts, identity lifecycle, authentication, authorization, SSO, federation, and IAM troubleshooting.

---

# Q1 — Authentication vs Authorization

### Question

What is the difference between authentication and authorization?

### Ideal Answer

Authentication verifies the identity of a user or entity.

Authorization determines what that authenticated identity is allowed to access or perform.

Example:

A user successfully logs into an application.

- Authentication → confirms who the user is.
- Authorization → determines whether the user can view, modify, or delete a resource.

A user can therefore be authenticated but not authorized.

---

# Q2 — Identity vs Credential

### Question

Is a username a credential?

### Ideal Answer

No. A username is normally an identifier, not a credential.

- Identity → who the person or entity is.
- Identifier → information used to identify that identity, such as a username.
- Account → a system-specific representation of an identity.
- Credential → something used to authenticate or prove control of an identity, such as a password, passkey, or security key.

Example:

Person → Identity → Username → Account → Credential

---

# Q3 — RBAC vs ABAC

### Question

What is the difference between RBAC and ABAC?

### Ideal Answer

RBAC stands for Role-Based Access Control. Permissions are assigned to roles, and users receive permissions through those roles.

ABAC stands for Attribute-Based Access Control. Access decisions are based on attributes of the subject, resource, action, or environment.

Example:

RBAC:

```text
User → Developer Role → Read Source Code

ABAC:
Department = Engineering
AND
DeviceCompliant = True
AND
Action = Read
AND
Resource = Source Code
→ Allow

RBAC is generally simpler when access requirements are based on stable job responsibilities. ABAC is useful when access needs to depend on dynamic or contextual conditions.


Q4 — Least Privilege
Question
What is least privilege and why is it important?
Ideal Answer
Least privilege means giving an identity only the permissions required to perform its legitimate tasks.
It reduces unnecessary access and limits the potential blast radius if an account or credential is compromised.
Example:
A developer who only needs to read production logs should not automatically receive permission to delete production databases.


Q5 — Passkeys
Question
What makes passkeys different from traditional passwords, and why are they phishing-resistant?
Ideal Answer
Passkeys use public-key cryptography.
During registration, an authenticator creates a public/private key pair. The public key is registered with the relying party, while the private key remains protected by the authenticator.
During authentication, the relying party sends a challenge. The authenticator signs the challenge using the protected private key, and the relying party verifies the signature using the public key.
Passkeys are phishing-resistant because the credential is cryptographically bound to the legitimate relying party/origin rather than being a reusable password that a phishing website can simply collect.


Q6 — SSO vs Federation
Question
What is the difference between SSO and federation?
Ideal Answer
SSO, or Single Sign-On, allows a user to access multiple applications without repeatedly performing authentication.
Federation establishes trust between separate identity or security domains so that one system can provide identity information that another system trusts.
SAML and OIDC are protocols commonly used in identity and federation architectures.
Example:
Company IdP
    ↓
Federation / Trust
    ↓
SaaS Application

SSO focuses primarily on the user's authentication experience, while federation focuses on trust between identity/security domains.


Q7 — JML Mover
Question
An employee moves from Finance to Engineering. What should happen to their access?
Ideal Answer
The employee is a Mover.
Their access should be reassessed based on their new role.
Required Engineering access should be provisioned, while Finance access that is no longer required should be removed.
Simply adding Engineering permissions without removing unnecessary Finance permissions can cause privilege accumulation and increase the potential blast radius if the account is compromised.


Q8 — Authentication vs Authorization Failure
Question
A user successfully logs into the corporate IdP but receives "Access Denied" in an application. What would you investigate?
Ideal Answer
I would investigate systematically:
1. Confirm that authentication succeeded.
2. Confirm that SSO/federation succeeded.
3. Confirm that the correct user identity was mapped.
4. Check whether the user is provisioned in the application.
5. Check groups, roles, and relevant claims.
6. Check application authorization policies.
7. Check whether contextual conditions are satisfied.
8. Check session/token issues.
9. Review IdP and application logs.
The important distinction is that successful authentication does not guarantee authorization.


Q9 — End-to-End SSO Flow
Question
Explain what happens when an employee opens an enterprise application using SSO.
Ideal Answer
The application may redirect the user to the Identity Provider.
The IdP authenticates the user and may require MFA.
After successful authentication, the IdP provides identity information to the application using a federation protocol such as SAML or OIDC.
The application validates the response, identifies the user, and applies authorization policies based on roles, groups, claims, or other conditions.
The application may then establish an authenticated session, often represented by a session cookie.
The overall flow is:
User
 ↓
Application / SP
 ↓
Identity Provider
 ↓
Authentication + MFA
 ↓
SAML / OIDC
 ↓
Identity / Claims
 ↓
Application
 ↓
Authorization
 ↓
Session
 ↓
Resource Access

Authentication proves who the user is, while authorization determines what the user is allowed to do.


Q10 — IAM Troubleshooting
Question
An employee says:
"I was able to log in yesterday, but today I can't access the application."
How would you troubleshoot it?
Ideal Answer
I would troubleshoot systematically.
1. Confirm the exact error
Determine whether it is:
- Authentication failure
- Access denied
- MFA failure
- Session problem
- Application error
2. Check authentication
Confirm that the user can successfully authenticate to the IdP.
3. Check the account
Verify that the account is:
- Enabled
- Not disabled
- Not locked
- Not expired
4. Check application assignment
Verify that the user still has access to the application.
5. Check groups and roles
Determine whether group membership, role assignment, or claims have changed.
6. Check authorization policies
Check whether a policy or contextual condition is preventing access.
Examples:
- Device compliance
- Location
- MFA requirement
- Risk
- Role
- Conditional access
7. Check federation/session/token issues
If authentication succeeded, investigate the SAML/OIDC response, claims, token, or application session.
8. Check logs
Correlate IdP and application logs to determine exactly where the request failed.
Day 10 Key Takeaways
- Authentication verifies identity.
- Authorization determines allowed actions.
- A username is normally an identifier, not a credential.
- RBAC assigns permissions through roles.
- ABAC uses attributes and policy conditions.
- Least privilege limits unnecessary access and blast radius.
- Passkeys use public-key cryptography and are designed to resist phishing.
- SSO allows access to multiple applications without repeated authentication.
- Federation establishes trust between separate identity/security domains.
- SAML and OIDC are different identity protocols.
- A successful IdP login does not guarantee application authorization.
- JML ensures access changes as employees join, move, and leave.
- IAM troubleshooting should follow the identity flow systematically.


Interview Questions & Ideal Answers

1. Can a user be authenticated but not authorized?
Yes.
Authentication verifies the user's identity, while authorization determines what that identity is allowed to do.
A user can successfully log in but still receive Access Denied because they don't have the required permission.

2. Is a username a credential?
Normally, no.
A username is an identifier. A credential is used to authenticate or prove control of an identity, such as a password, passkey, or security key.

3. Why is least privilege important?
Least privilege minimizes unnecessary access and reduces the potential blast radius if an account or credential is compromised.

4. When is RBAC simpler than ABAC?
RBAC is generally simpler when access requirements map cleanly to stable job responsibilities.
For example:
Developer → Developer Role → Development Resources

ABAC becomes more useful when access depends on dynamic attributes or context.

5. Why are passkeys phishing-resistant?
Passkeys use public-key cryptography and are bound to the legitimate relying-party origin. They don't expose a reusable password that a phishing website can simply collect.

6. What is the difference between SSO and federation?
SSO allows users to access multiple applications without repeatedly authenticating.
Federation establishes trust between separate identity/security domains so identity information from one system can be trusted by another.

7. What is an IdP?
An Identity Provider authenticates users and provides identity information to applications.
Examples include Microsoft Entra ID and Okta.

8. What is an SP?
A Service Provider is the application or service that the user wants to access.

9. What is a SAML assertion?
A SAML assertion is a structured statement issued by an identity provider that can contain information about a subject, authentication, and attributes for consumption by a service provider.

10. What would you check if a user can log into the IdP but cannot access an application?
I would check:
Authentication
↓
SSO/Federation
↓
User mapping
↓
Provisioning
↓
Groups/Roles/Claims
↓
Authorization policies
↓
Session/Token
↓
Logs

Day 10 Mock Interview Questions

Question 1
Explain IAM to a non-technical manager in 60–90 seconds.
Ideal Answer
IAM is the process of managing digital identities and controlling what those identities can access. It covers the identity lifecycle, authentication, authorization, access provisioning, access reviews, and removal of access when it is no longer required. The goal is to make sure the right person or system gets the right access at the right time while minimizing unnecessary access and security risk.

Question 2
Explain what technically happens when an employee logs into a SaaS application using SSO.
Ideal Answer
The application redirects the employee to the organization's Identity Provider. The IdP authenticates the employee and may require MFA. After successful authentication, the IdP sends identity information to the application using a protocol such as SAML or OIDC. The application validates the response, identifies the user, and applies authorization policies based on roles, groups, claims, or other conditions. It can then establish a session and allow the user to access permitted resources.

Question 3
A user can authenticate successfully to Microsoft Entra ID but gets Access Denied when opening Salesforce. How would you investigate?
Ideal Answer
First, I would confirm that authentication to Entra ID succeeded. Then I would determine whether the federation/SSO exchange with Salesforce succeeded. Next, I would check whether the correct user was mapped and whether the user is provisioned in Salesforce. I would check groups, roles, claims, and application assignments, followed by Salesforce authorization policies and any contextual conditions. Finally, I would check session/token issues and correlate Entra and Salesforce logs to identify where the request failed.