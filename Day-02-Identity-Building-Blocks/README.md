# Day 02 — Identity Building Blocks

## Topics Covered

- Identity
- Account
- Credential
- Session
- Token
- Permission
- Resource

## Identity

An identity represents an entity that can be recognized by a system.

Examples:
- Human user
- Application
- Service
- Workload
- Device

Example:

`alice@company.com`

## Account

An account is a representation of an identity within a particular system or service.

Example:

Alice may have separate accounts in:
- Corporate IdP
- AWS
- GitHub
- HR application

## Credential

A credential is information or an authentication factor used to prove an identity.

Examples:
- Password
- Passkey
- Security key
- Certificate
- Access key
- Authentication token

### Identity vs Credential

Identity = Who the entity is

Credential = What is used to prove/authenticate that identity

Example:

Identity: `alice@company.com`  
Credential: `Password + MFA`

## Session

A session represents an active interaction between an authenticated identity and a system.

Example:

```text
User
 ↓
Authentication
 ↓
Authenticated Identity
 ↓
Session
 ↓
Application

Token
A token is data used as part of an authenticated or authorized interaction.
Examples:
- Access token
- ID token
- Session token
- Temporary credentials
Permission
A permission defines what an identity is allowed to do.
A useful model:

WHO
+
CAN DO WHAT
+
TO WHICH RESOURCE

Resource
A resource is something an identity attempts to access.
Examples:
- Database
- S3 bucket
- File
- Application
- API
- Virtual machine
- HR record


Identity Access Chain

Person
 ↓
Identity
 ↓
Account
 ↓
Credential
 ↓
Session / Token
 ↓
Permission
 ↓
Resource

Identity:
alice@company.com

Credential:
Password + MFA

Session:
Authenticated application session

Permission:
READ Finance Reports

Resource:
Finance Report

Authentication → SUCCESS
Authorization → ALLOW


Authentication → SUCCESS
Authorization → DENY

IAM Troubleshooting Chain

Identity
 ↓
Account
 ↓
Credential / Authentication
 ↓
Session / Token
 ↓
Role / Group / Permission
 ↓
Policy
 ↓
Requested Action
 ↓
Resource
 ↓
Allow / Deny


Human vs Non-Human Identity
Human

Employee
 ↓
Corporate Identity
 ↓
Authentication
 ↓
Application

Non-Human
Application / Service / Workload
 ↓
Service Identity
 ↓
Credential / Token
 ↓
API / Resource


Identity represents an entity.
Account represents an identity within a system.
Credentials are used to authenticate an identity.
Sessions represent active interactions.
Tokens can be used during authenticated/authorized interactions.
Permissions define allowed actions.
Resources are the objects being accessed.
Identity and credential are not the same thing.