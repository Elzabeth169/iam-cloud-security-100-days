Day 7 — Identity Hygiene & Reconciliation

Objective

Understand how IAM manages access after provisioning, including deprovisioning, reconciliation, dormant accounts, orphaned accounts, and privilege accumulation.
Topics Covered
- Provisioning
- Deprovisioning
- Reconciliation
- Dormant accounts
- Orphaned accounts
- Privilege accumulation
- JML lifecycle
- IAM access hygiene
- IAM troubleshooting

1. Provisioning
Provisioning is the process of creating or updating a user's access to a system according to approved requirements.
Examples:
- Creating user accounts
- Assigning groups
- Assigning roles
- Granting application access
- Assigning licenses
Typical flow:
HR System
   ↓
IAM / IGA
   ↓
Access Rules / Approvals
   ↓
Target Applications
   ↓
Accounts + Groups + Permissions

2. Deprovisioning
Deprovisioning is the process of removing or disabling access when it is no longer required.
Common actions:
- Disable accounts
- Remove group memberships
- Remove application access
- Remove licenses
- Revoke access where appropriate
- Handle accounts according to retention policies
Deprovisioning does not always mean deleting the account.

3. Reconciliation
Reconciliation is the process of comparing the expected identity/access state with the actual state in a target system and identifying or correcting discrepancies.
Example:
Expected State
      ↓
   Compare
      ↓
Actual State
      ↓
Difference?
      ↓
Investigate / Correct

Reconciliation helps detect situations where an account has access that it should no longer have.


4. Dormant Accounts
A dormant account is an account that has not been used for a defined period.
Example:
Account: employee123
Last Login: 200 days ago
Status: Active

Dormant accounts should be reviewed according to organizational policy because unused active accounts can increase security risk.


5. Orphaned Accounts
An orphaned account is generally an account that is no longer properly associated with a valid or current owner/identity record.
Example:
Employee leaves
      ↓
HR record becomes inactive
      ↓
Application account remains
      ↓
No valid owner
      ↓
Orphaned Account

6. Dormant vs Orphaned Accounts
Dormant Account	Orphaned Account
Account has little/no activity	Account has no valid/current owner
Owner may still exist	Owner may be missing or invalid
Main concern is inactivity	Main concern is ownership
Can also be orphaned	Can also be dormant


7. Privilege Accumulation
Privilege accumulation occurs when users retain old permissions after changing roles or responsibilities.
Example:
Developer
   ↓
Developer permissions

Employee moves to Security
   ↓
Security permissions added
   ↓
Old Developer permissions remain

This creates permission creep and can violate least privilege.


8. JML + Identity Hygiene
JOINER
   ↓
Provisioning
   ↓
Access

MOVER
   ↓
Access Change
   ↓
Old Access Reviewed/Removed

LEAVER
   ↓
Deprovisioning
   ↓
Access Removed/Disabled

Continuous
   ↓
Reconciliation
   ↓
Dormant / Orphaned / Excessive Access Detection
 

9. IAM Troubleshooting Example
Scenario
An employee leaves the company, but their AWS access remains active.
Investigation
1. Check the employee's HR status.
2. Check whether the termination event reached the IAM system.
3. Check the IAM workflow execution.
4. Check connector/provisioning logs.
5. Check the AWS account and permissions.
6. Check whether the account was used after termination.
7. Disable or remove unauthorized access according to policy.
8. Document the issue.
9. Investigate why deprovisioning failed.
10. Verify that reconciliation detects similar mismatches.


10. Key Takeaways
- Provisioning gives or updates access.
- Deprovisioning removes or disables access.
- Deprovisioning does not always mean account deletion.
- Reconciliation compares expected and actual access states.
- Dormant accounts have little/no activity for a defined period.
- Orphaned accounts lack a valid/current owner or identity association.
- Privilege accumulation can create excessive access.
- JML helps manage access throughout the employee lifecycle.
- Reconciliation and access reviews help maintain least privilege.
- IAM is not only about giving access; it is also about continuously ensuring access remains appropriate.