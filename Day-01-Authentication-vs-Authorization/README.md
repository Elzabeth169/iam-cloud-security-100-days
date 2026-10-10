# Day 01 — Authentication vs Authorization

## Objective

Understand the difference between Authentication (AuthN) and Authorization (AuthZ), and how both work together in an Identity and Access Management (IAM) system.

---

## 1. Authentication

Authentication is the process of verifying the identity of a user, device, application, or other entity.

In simple terms:

> Authentication answers: "Who are you?"

Examples of authentication:

- Username and password
- Password + authenticator app
- Fingerprint
- Security key
- Passkey

### Example

When I log into my email account:

1. I provide my username.
2. I provide my password.
3. The service verifies my credentials.
4. If MFA is enabled, an additional authentication factor may be required.
5. The service establishes that I am the claimed user.

At this point, I have been authenticated.

---

## 2. Authorization

Authorization is the process of determining what an authenticated identity is allowed to access or perform.

In simple terms:

> Authorization answers: "What are you allowed to do?"

Authorization can determine:

- Which resources a user can access
- Which actions they can perform
- Whether they can read, write, modify or delete data
- Which applications they can use

### Example

An employee successfully logs into a company application.

They are authenticated.

However, they may only be allowed to:

- View employee information
- Not modify employee information
- Not access financial information

These access decisions are authorization decisions.

---

## 3. Authentication vs Authorization

| Authentication | Authorization |
|---|---|
| Verifies identity | Determines access |
| Answers "Who are you?" | Answers "What can you do?" |
| Happens before authorization | Usually evaluated after authentication |
| Uses credentials/factors | Uses policies, roles, permissions and attributes |
| Example: password + MFA | Example: allowing READ access to S3 |

---

## 4. Basic IAM Request Flow

```text
User
  |
  v
Authentication
  |
  | "Who are you?"
  v
Authenticated Identity
  |
  v
Authorization
  |
  | "What are you allowed to do?"
  v
Access Decision
  |
  +------> Allow
  |
  +------> Deny
  |
  v
Resource