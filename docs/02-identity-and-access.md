# Identity and Access

[Back to README](../README.md)

## Objective

Every user belongs to a department group. No admin holds a standing role. Every sign-in meets the Conditional Access baseline. Only Operations creates Teams, and every new group follows the naming policy.

## 1. Users and Security Groups

Populate the **Department** attribute on all 45 test users first. The naming policy and the dynamic distribution lists both read it.

| Group | Type | Membership | Purpose |
|---|---|---|---|
| SG-Design | Security | Assigned | Design staff |
| SG-ProjectManagement | Security | Assigned | PM staff |
| SG-Finance | Security | Assigned | Finance staff |
| SG-BusinessDevelopment | Security | Assigned | BD staff |
| SG-Operations | Security | Assigned | Admins and Team creators |

Admin center path: Entra admin center > Groups > All groups > New group

Evidence: `screenshots/01-entra/01-entra-security-groups.png`

## 2. Privileged Identity Management

| Role | Assignment | Max activation | MFA | Justification |
|---|---|---|---|---|
| Global Administrator | Eligible | 4 hours | Required | Required |
| Teams Administrator | Eligible | 4 hours | Required | Required |
| SharePoint Administrator | Eligible | 4 hours | Required | Required |
| Exchange Administrator | Eligible | 4 hours | Required | Required |

Admin center path: Entra admin center > ID Governance > Privileged Identity Management > Microsoft Entra roles

Notes:
- Keep one break-glass Global Admin account with a permanent assignment, excluded from Conditional Access. Record where its credentials are stored in the runbook.

Evidence:
- `screenshots/01-entra/02-entra-pim-role-settings-global-admin.png`
- `screenshots/01-entra/03-entra-pim-eligible-assignments.png`

## 3. Conditional Access Baseline

| Policy name | Users | Condition | Grant / block |
|---|---|---|---|
| CA01-AllUsers-RequireMFA | All users, exclude break-glass | All cloud apps | Require MFA |
| CA02-AllUsers-BlockLegacyAuth | All users, exclude break-glass | Client apps: Exchange ActiveSync, other clients | Block |
| CA03-UntrustedCountries-RequireCompliantDevice | All users, exclude break-glass | Locations: all except trusted countries | Require compliant device |
| CA04-AdminActivation-RequireMFA | All users | Authentication context used by PIM | Require MFA |

Rollout: start each policy in **Report-only**, check sign-in logs, then switch to **On**.

Admin center path: Entra admin center > Protection > Conditional Access > Policies

Evidence: `screenshots/01-entra/04-entra-ca-policy-list.png` and one screenshot per policy

## 4. Group Creation Restriction

Setting: only members of SG-Operations create Microsoft 365 groups. Teams follows this setting.

Method: Graph Explorer, Group.Unified directory setting. Steps in [scripts/README.md](../scripts/README.md).

Evidence: `screenshots/01-entra/05-entra-group-creation-setting.png`

## 5. Naming Policy

| Setting | Value |
|---|---|
| Prefix | `[Department]-` (reads the creator's Department attribute) |
| Blocked words | Add the list you used here |

Admin center path: Entra admin center > Groups > Naming policy

Evidence: `screenshots/01-entra/06-entra-naming-policy.png`

## Decisions and Trade-offs

Record here what you changed from the brief and why.
