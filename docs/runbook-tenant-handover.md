# Northwood Architects Tenant Handover

[Back to README](../README.md)

Prepared for: Head of Operations, Northwood Architects
Prepared by: Samuel Afeni, Microsoft 365 Consultant
Date: (handover date)
Version: 1.0

Target length: 5 pages when exported to PDF.

## Page 1: Tenant at a Glance

- Tenant name, primary domain, licence count and renewal date
- Admin roles and who holds them (eligible only)
- Break-glass account: name, where the credentials are stored, when to use it
- Support contacts

## Page 2: Daily and Weekly Operations

### New starter
1. Create user, set Department attribute
2. Add to the department security group
3. Assign Business Premium licence
4. Confirm MFA registration on first sign-in

### Leaver
1. Block sign-in and revoke sessions
2. Convert mailbox to shared if needed
3. Remove licence
4. Note the 90-day OneDrive retention window and assign access to the manager

### Weekly checks
- Reviewer mailbox for redirected file-transfer messages
- Sign-in logs for blocked sign-ins
- PIM activation history

## Page 3: Admin Access and Security

- How to activate an admin role in PIM, step by step
- What each Conditional Access policy does and who is excluded
- What to do when a user loses their MFA device

## Page 4: Collaboration and External Sharing

- How to request a new Team (Operations only)
- How to create a new client project site from the template
- Which label to apply and what each label allows
- How to invite a guest, and why Finance refuses new guests
- How the shared channel with the engineering partner works

## Page 5: Maintenance Calendar and Known Limits

| Task | Frequency | Owner |
|---|---|---|
| Review guest accounts | Quarterly | Operations |
| Review PIM eligible assignments | Quarterly | Operations |
| Respond to group expiration emails | As received | Team owners |
| Move DMARC policy towards reject | After 30 days of clean reports | Operations |

Known limits:
- Group expiration applies one lifetime value. Finance sits outside the policy.
- No PowerShell automation. All tasks use admin centers.
