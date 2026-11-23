# Northwood Architects: A Governed Microsoft 365 Tenant from Scratch

### Identity-first Microsoft 365 Business Premium build for a 45-person architecture practice opening its second office.

## Index

This repository documents a full tenant build: identity and privileged access, mail, document management and collaboration, with governance applied from day one. Every configuration step comes with screenshot evidence and a validation test.

**Architecture Foundation**

- [Architecture](docs/01-architecture.md): workloads, connections and external touchpoints
- [Identity and Access](docs/02-identity-and-access.md): security groups, PIM, Conditional Access, group creation and naming policy

**Workload Build**

- [Exchange Online](docs/03-exchange-online.md): shared mailboxes, dynamic distribution lists, threat policies, email authentication, mail flow rule
- [SharePoint and OneDrive](docs/04-sharepoint-onedrive.md): intranet, hub, project template, storage, retention, external sharing
- [Teams and Sensitivity Labels](docs/05-teams-and-sensitivity-labels.md): department teams, labels, shared channel, expiration

**Proof and Handover**

- [Validation](docs/06-validation.md): every success criterion tested, with evidence
- [Tenant Handover Runbook](docs/runbook-tenant-handover.md): the operations guide for Northwood's Head of Operations
- [Reflection](docs/reflection.md): trade-offs made and what I would change
- [Sample Consulting Invoice](docs/sample-invoice.md)

## Overview

Northwood Architects grew from 12 to 45 staff in three years. The founders ran the firm on Dropbox and personal Gmail. With a second office opening, the new Head of Operations asked for Microsoft 365 Business Premium, configured properly from the first day.

The firm has four departments: Design, Project Management, Finance and Business Development. Staff collaborate every day with planning consultants, structural engineers, interior designers and clients. Two rules shaped the design. Design IP stays inside the firm. Finance stays internal.

## Project Summary

| Area | Details |
|---|---|
| Project type | Greenfield tenant build and governance baseline |
| Platform | Microsoft 365 Business Premium, Entra ID P2 (trial), Exchange Online, SharePoint, OneDrive, Teams, Purview |
| Scenario | Fictional firm, built in a real trial tenant |
| Users | 45 staff across 4 departments, plus an Operations admin group |
| Security model | Eligible admin roles through PIM, Conditional Access baseline, label-driven collaboration |
| Difficulty | Beginner to Intermediate |
| Build time | 10 to 15 hours over 2 weeks |
| Tooling | Admin centers and Graph Explorer only (no PowerShell, see [/scripts](scripts/README.md)) |

## Objectives

1. Map every user to a department security group and drive access from those groups.
2. Remove standing admin access. Every admin role is eligible, time-bound and justified.
3. Block legacy authentication and require MFA for every sign-in.
4. Stop Team sprawl before it starts with creation limits, a naming policy and expiration.
5. Protect the firm's mail domain with SPF, DKIM and DMARC, and catch risky file-transfer links.
6. Let external partners collaborate on design work while keeping Finance closed to new guests.
7. Hand the firm a runbook its Head of Operations follows without me.

## Architecture Overview

### Tenant Architecture

![Northwood tenant architecture](diagrams/northwood-architecture.png)

Microsoft Entra ID sits at the top as the control point. Every sign-in from staff and external guests passes through the Conditional Access baseline before a token reaches any workload. Operations admins hold eligible roles only and activate them through PIM. Security groups and group policies in Entra drive membership, Team creation rights and naming across the workloads below.

Exchange Online receives mail from the internet and relies on public DNS records for SPF, DKIM and DMARC. SharePoint holds the intranet, department sites and project sites. Teams stores its files in SharePoint, and Purview sensitivity labels set guest and sharing rules on each Team and site. The partner tenant connects through a single shared channel.

Source: [northwood-architecture.drawio](diagrams/northwood-architecture.drawio)

### Identity Flow

![Northwood identity flow](diagrams/northwood-identity-flow.png)

The left lane shows how Conditional Access evaluates a sign-in. Legacy authentication stops at the first check. Sign-ins from untrusted countries need a compliant device. Every user then completes MFA before Entra issues a token.

The right lane shows PIM activation. A signed-in admin requests a role, passes an MFA step-up, enters a business justification and receives the role for four hours at most. The role then returns to eligible.

Source: [northwood-identity-flow.drawio](diagrams/northwood-identity-flow.drawio)

## Design Principles

- **Groups first.** Access, mailbox delegation, distribution lists and Teams all follow department security groups. A new starter joins one group and inherits the rest.
- **No standing privilege.** Admin roles are eligible, never permanently active.
- **Govern at creation.** Creation rights, naming and labels apply before a Team exists, not after a clean-up.
- **Share by exception.** Guests reach the work they need. Finance accepts no new guests.
- **Built for handover.** Every setting traces to an admin center path in the runbook.

## Validation Results

| # | Success criterion | Result | Evidence |
|---|---|---|---|
| 1 | A guest invited to the Finance site fails with the expected error | Pending | [screenshot](screenshots/05-validation/) |
| 2 | A standard user cannot create a Team | Pending | [screenshot](screenshots/05-validation/) |
| 3 | External email with a WeTransfer link lands in the reviewer mailbox | Pending | [screenshot](screenshots/05-validation/) |
| 4 | The shared channel works in both directions | Pending | [screenshot](screenshots/05-validation/) |
| 5 | SPF, DKIM and DMARC pass on mail-tester.com | Pending | [screenshot](screenshots/05-validation/) |
| 6 | PIM activation for Global Admin requires MFA and justification | Pending | [screenshot](screenshots/05-validation/) |
| 7 | Diagrams render in both .drawio and .png | Pending | [/diagrams](diagrams/) |

Full test steps: [docs/06-validation.md](docs/06-validation.md)

## Licensing and Lab Setup

| Component | Source | Why |
|---|---|---|
| Microsoft 365 Business Premium | Trial tenant | Core workloads, Entra ID P1, Intune |
| Entra ID P2 | Trial add-on | PIM needs P2. Business Premium includes P1 only |
| Second tenant | Separate trial | Plays the structural engineering partner for the shared channel |
| Custom domain | Purchased domain | SPF, DKIM, DMARC and the mail-tester.com check |
| Test device | One enrolled Windows device | Proves the compliant-device policy |

## Repository Structure

```
northwood-m365-governed-tenant/
├── README.md
├── docs/
│   ├── 01-architecture.md
│   ├── 02-identity-and-access.md
│   ├── 03-exchange-online.md
│   ├── 04-sharepoint-onedrive.md
│   ├── 05-teams-and-sensitivity-labels.md
│   ├── 06-validation.md
│   ├── runbook-tenant-handover.md
│   ├── reflection.md
│   └── sample-invoice.md
├── diagrams/
│   ├── northwood-architecture.drawio / .png
│   └── northwood-identity-flow.drawio / .png
├── screenshots/
│   ├── 01-entra/
│   ├── 02-exchange/
│   ├── 03-sharepoint-onedrive/
│   ├── 04-teams/
│   └── 05-validation/
└── scripts/
    └── README.md
```

## Scope

**In scope**

- Entra ID groups, PIM, Conditional Access, group creation and naming policy
- Exchange Online mailboxes, distribution lists, threat policies, email authentication and mail flow
- SharePoint intranet, hub, project template, OneDrive storage and retention, external sharing
- Teams, sensitivity labels, cross-tenant shared channel, group expiration

**Out of scope**

- PowerShell automation (see [scripts/README.md](scripts/README.md))
- Data migration from Dropbox and Gmail
- Full Intune device rollout (one test device only)
- Defender for Endpoint and Purview DLP

## Intended Audience

- Microsoft 365 Engineers and Administrators
- IT leads at small and mid-size firms planning a first Microsoft 365 rollout
- Hiring managers reviewing practical Microsoft 365 work

## Disclaimer

Northwood Architects is a fictional company. I built every configuration in this repository myself, in Microsoft 365 trial tenants created for this project. Names, domains and users are test data. Screenshots contain no real customer information.

## Author

Samuel Afeni, Microsoft 365 Engineer
[linkedin.com/in/samafeni](https://www.linkedin.com/in/samafeni)
