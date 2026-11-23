# Teams and Sensitivity Labels

[Back to README](../README.md)

## Objective

Give each department a Team tied to its security group, let labels decide guest access, connect Design to the structural engineering partner through one shared channel and expire unused Teams.

## 1. Department Teams

| Team | Membership source | Label |
|---|---|---|
| Design-Studio | SG-Design | Confidential |
| ProjectManagement-Delivery | SG-ProjectManagement | Internal |
| Finance-Team | SG-Finance | Confidential |
| BusinessDevelopment-Pipeline | SG-BusinessDevelopment | Internal |

Record the final names the naming policy produced.

Evidence: `screenshots/04-teams/01-teams-department-teams.png`

## 2. Sensitivity Labels for Containers

Enable labels for groups and sites first (EnableMIPLabels). Steps in [scripts/README.md](../scripts/README.md).

| Label | Privacy | Guest access | External sharing |
|---|---|---|---|
| Public | Public | Allowed | New and existing guests |
| Internal | Private | Allowed | Existing guests |
| Confidential | Private | Blocked | Only people in the organisation |

Admin center path: Microsoft Purview portal > Information protection > Sensitivity labels

Evidence: `screenshots/04-teams/02-purview-labels.png`, `03-purview-label-policy.png`

## 3. Shared Channel with Partner Tenant

| Step | Tenant | Setting |
|---|---|---|
| 1 | Northwood | Cross-tenant access: add partner tenant, allow B2B direct connect inbound and outbound |
| 2 | Partner | Same settings pointing back to Northwood |
| 3 | Northwood | Teams admin center: shared channels allowed in the Teams policy |
| 4 | Northwood | Create shared channel in Design-Studio, invite partner user |

Admin center path: Entra admin center > External Identities > Cross-tenant access settings

Evidence: `screenshots/04-teams/04-entra-cross-tenant-northwood.png`, `05-entra-cross-tenant-partner.png`, `06-teams-shared-channel.png`

## 4. Group Expiration

| Setting | Value |
|---|---|
| Lifetime | 180 days |
| Applies to | Selected groups (all department groups except Finance) |
| Notification email | Operations mailbox |

The brief asked for 365 days on Finance. Entra supports one lifetime value per tenant, so Finance sits outside the policy. See [reflection](reflection.md).

Admin center path: Entra admin center > Groups > Expiration

Evidence: `screenshots/04-teams/07-entra-group-expiration.png`

## Decisions and Trade-offs

Record here what you changed from the brief and why.
