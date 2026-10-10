
---

## Day 3 — `README.md`

```markdown
# Day 03 — RBAC, ABAC & Least Privilege

## Topics Covered

- RBAC
- ABAC
- Role Assignment
- Attributes
- Deny-by-Default
- Least Privilege

## RBAC

Role-Based Access Control (RBAC) assigns permissions to roles.

Users receive permissions through their assigned roles.

Example:

Developer Role
 ↓
Read/Write Source Code
 ↓
Access Development Environment

ABAC
Attribute-Based Access Control (ABAC) makes access decisions using attributes.

User Attributes
- Department
- Job Title
- Location

Resource Attributes
- Classification
- Department
- Sensitivity

Environmental Attributes
- Time
- Network
- Device State

Example:
Department = Finance
AND
Device = Managed
AND
Resource = Internal
        ↓
      ALLOW

| RBAC                              | ABAC                              |
|---                                |---                                |
| Based mainly on roles             | Based on attributes               |
| Simpler for stable job functions  | More flexible for dynamic rules   |
| Permissions assigned to roles     | Policies evaluate attributes      |
| Easier to manage initially        | Can become more complex           |    

When is RBAC simpler than ABAC?
RBAC is simpler when access requirements are mostly determined by stable job functions.
Example:
Developers → Development Resources
Finance → Finance Applications
HR → HR Applications

ABAC is more useful when access decisions need to consider dynamic factors such as:
Department
+
Location
+
Device State
+
Resource Classification
+
Time


Least Privilege

Least privilege means giving an identity only the access required to perform its legitimate responsibilities.
Example:
A developer who needs to read production logs should not automatically have:

Production Database DELETE
Production Server ADMIN
IAM ADMIN

Instead, the developer should receive only the required permissions.
Why Least Privilege Matters
Excessive permissions increase the potential impact of:
- Compromised accounts
- Stolen credentials
- Insider threats
- Misconfiguration
- Accidental actions
Least privilege helps reduce unnecessary access and potential blast radius.


Deny-by-Default

Deny-by-default means access should not be granted unless the identity has the required authorization.

Access Request
     ↓
Required Permission?
   /       \
 YES       NO
  ↓         ↓
ALLOW      DENY

Access Design — 20-Person Company
Roles
- Employee
- Developer
- Manager
- Admin

Access Matrix

Resource	            Employee	Developer	Manager	    Admin
Company Portal	        Read	    Read	    Read	    Admin
HR Application	        OwnData	    Limited	    Team Data	Admin
Source Code	            No	        Read/Write	 Read	    Admin
Development Environment	No	        Read/Write	Read	    Admin
Financial Reports	    No	        No	        Read	    Admin
Production Systems	    No	        Limited	    No	        Admin
IAM Administration	    No	        No	        No	        Admin

Example Role Assignments
Employee
Alice
 ↓
Employee Role
 ↓
Company Portal
Own HR Information

Developer
Bob
 ↓
Developer Role
 ↓
Source Code
Development Environment

Manager
Carol
 ↓
Manager Role
 ↓
Team Information
Management Reports

Admin
David
 ↓
Admin Role
 ↓
Administrative Resources

Least Privilege Example
A developer needs:
READ/WRITE → Development Source Code
READ → Development Logs

The developer does not automatically need:
DELETE → Production Database
ADMIN → IAM
ADMIN → Production Servers

RBAC vs ABAC Example
RBAC
User
 ↓
Developer Role
 ↓
Development Permissions

ABAC
User Attributes
+
Resource Attributes
+
Environmental Conditions
 ↓
Authorization Policy
 ↓
Allow / Deny

Key Takeaways
- RBAC assigns permissions through roles.
- ABAC makes access decisions using attributes.
- RBAC is simpler when access maps clearly to job functions.
- ABAC is useful for dynamic and context-dependent access.
- Least privilege means granting only the access required.
- Deny-by-default prevents unnecessary access.
- Excessive permissions increase security risk.