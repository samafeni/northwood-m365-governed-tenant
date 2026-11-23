# Architecture

[Back to README](../README.md)

## Purpose

This document explains how the Northwood tenant fits together: which workloads exist, how identity governs them and where the tenant meets the outside world.

## Tenant Architecture

![Northwood tenant architecture](../diagrams/northwood-architecture.png)

## Components

| Layer | Component | Role in the design |
|---|---|---|
| Identity | Entra ID security groups | One group per department plus Operations. Every other control reads from these groups |
| Identity | Conditional Access | MFA for all users, block legacy auth, compliant device from untrusted countries |
| Identity | Privileged Identity Management | Global, Teams, SharePoint and Exchange Admin held as eligible roles |
| Identity | Group policies | Only Operations creates Microsoft 365 groups. Naming prefix and blocked words |
| Mail | Exchange Online | Shared mailboxes, dynamic distribution lists, threat policies, mail flow rule |
| Content | SharePoint and OneDrive | Intranet, hub, department sites, project template, storage and retention |
| Collaboration | Teams | Department teams, shared channel with partner tenant |
| Protection | Purview sensitivity labels | Public, Internal, Confidential with guest and sharing settings |

## External Touchpoints

| Touchpoint | Connection | Control applied |
|---|---|---|
| External guests (planners, designers, clients) | Entra B2B | Conditional Access, label settings, Finance site closed to new guests |
| Partner tenant (structural engineers) | B2B direct connect, shared channel | Cross-tenant access settings on both tenants |
| Internet mail senders | Exchange Online inbound | Anti-spam, anti-phishing, WeTransfer/Dropbox mail flow rule |
| Public DNS | SPF, DKIM, DMARC records | Domain authentication |

## Identity Flow

![Northwood identity flow](../diagrams/northwood-identity-flow.png)

## Key Design Decisions

| Decision | Choice | Reason |
|---|---|---|
| Admin access | Eligible through PIM, 4-hour maximum | No standing privilege in a 45-person firm with one Operations team |
| Team creation | Operations group only | Prevents sprawl as the firm grows across two offices |
| Finance sharing | Existing guests only | Finance must stay internal |
| Partner collaboration | Shared channel, not guest accounts | Engineers keep their own identity. No guest accounts to clean up later |
| Group expiration | 180 days, Finance excluded | Entra allows one lifetime per tenant. See [reflection](reflection.md) |
