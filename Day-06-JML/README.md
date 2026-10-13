Day 06 

identity lifecycle and how IAM manages user access when employees join, change roles, and leave an organization.

- Joiner, Mover, Leaver (JML)
- Identity lifecycle
- Provisioning
- Deprovisioning
- Role/access changes
- Least privilege
- Privilege accumulation
- Reconciliation
- Orphaned accounts
- Dormant accounts
- JML troubleshooting


1. Identity Lifecycle

JML represents three major stages of the identity lifecycle:
JOINER
   ↓
Employee joins
   ↓
MOVER
   ↓
Employee changes role/department
   ↓
LEAVER
   ↓
Employee leaves


2. Joiner
A Joiner is a new employee or user entering an organization who requires access.
Typical activities:
- Create identity/account
- Assign required groups
- Assign applications
- Assign licenses
- Configure authentication
- Provide required access
HR System
    ↓
Employee Created
    ↓
Identity Created
    ↓
Account Provisioned
    ↓
Groups / Roles / Applications
    ↓
Required Access


3. Mover
A Mover is an existing employee whose role, department, or responsibilities change.
Example:
Developer
    ↓
Role Change
    ↓
Security Analyst

IAM should:
- Add newly required access
- Review existing access
- Remove access that is no longer required
This helps prevent privilege accumulation.
Old Access + New Access
        ↓
Excessive Privileges

4. Leaver
A Leaver is a user who no longer requires organizational access.
Examples:
- Resignation
- Termination
- Retirement
- End of contractor engagement
Typical actions:
Employee Leaves
      ↓
Disable Account
      ↓
Remove Application Access
      ↓
Remove Group Memberships
      ↓
Remove Licenses / Access

The goal is to prevent unnecessary access from remaining active.


5. Provisioning
Provisioning is the process of creating or configuring a user's account and required access.
New Employee
     ↓
Account Creation
     ↓
Groups / Roles
     ↓
Applications
     ↓
Required Access



6. Deprovisioning
Deprovisioning is the process of removing or disabling access when it is no longer required.
Employee Leaves
     ↓
Disable Account
     ↓
Remove Access
     ↓
Remove Groups / Licenses



7. JML and Least Privilege
JML helps maintain least privilege throughout the identity lifecycle.
JOINER
Give required access

MOVER
Add required access
+
Remove unnecessary old access

LEAVER
Remove access


8. Privilege Accumulation
Privilege accumulation occurs when users retain old permissions after their responsibilities change.
Example:
Developer
    ↓
Developer Access
    ↓
Moves to Finance
    ↓
Finance Access Added
    ↓
Developer Access Remains

The user now has more access than required.


9. Reconciliation
Reconciliation involves comparing the expected identity/access state with the actual state in a target system.
Example:
IAM System
Expected: Account Disabled
        ↓
      Compare
        ↓
Application
Actual: Account Active

A mismatch should be investigated and remediated.


10. Orphaned Accounts
An orphaned account is an account that no longer has a valid associated owner or identity.
Example:
Employee Leaves
      ↓
Employee Identity Removed
      ↓
Application Account Remains
      ↓
Orphaned Account


11. Dormant Accounts
A dormant account is an account that exists but has not been used for a significant period.
Example:
Account: Active
Last Login: 14 Months Ago

A dormant account may still have a legitimate owner.
Therefore:
Dormant ≠ Orphaned


12. JML Example
Joiner
Employee joins as Developer
        ↓
Identity created
        ↓
Developer groups assigned
        ↓
Required applications assigned

Mover
Developer
    ↓
Becomes Security Analyst
    ↓
Remove unnecessary developer access
    ↓
Add required security access

Leaver
Employee leaves
    ↓
Disable account
    ↓
Remove application access
    ↓
Remove groups
    ↓
Remove unnecessary privileges


13. JML Troubleshooting
If an employee changes departments but still has access to the old department's application:
1. Check whether HR updated the employee
2. Check whether IAM received the change
3. Check whether the Mover workflow triggered
4. Check whether the old access should have been removed
5. Check whether the removal task succeeded
6. Check whether the target application received the change
7. Check whether another group or role is providing the access

Key Takeaways
- Joiner → Provision required access
- Mover → Modify access
- Leaver → Remove access
- Provisioning creates/configures access.
- Deprovisioning removes/disables access.
- JML supports least privilege.
- Movers can cause privilege accumulation if old access isn't removed.
- Orphaned accounts have no valid associated owner.
- Dormant accounts exist but have not been used for a significant period.
- Reconciliation helps identify mismatches between expected and actual account/access states.