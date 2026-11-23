# SharePoint and OneDrive

[Back to README](../README.md)

## Objective

Give the firm one intranet, connect every department site through a hub, make new client projects repeatable, set storage and retention limits, and keep Finance closed to new guests.

## 1. Intranet Communication Site

| Item | Value |
|---|---|
| Site name | Northwood Intranet |
| Sections | News, Policies, Quick links |
| Set as | Home site |

Evidence: `screenshots/03-sharepoint-onedrive/01-spo-intranet-home.png`

## 2. Hub Site

| Hub | Associated sites |
|---|---|
| Northwood Intranet | Design, Project Management, Finance, Business Development |

Admin center path: SharePoint admin center > Sites > Active sites > select site > Hub > Register as hub site

Evidence: `screenshots/03-sharepoint-onedrive/02-spo-hub-associations.png`

## 3. Project Template Team Site

Describe the libraries, folders and pages in the template, and how Operations creates a new project site from it.

Evidence: `screenshots/03-sharepoint-onedrive/03-spo-project-template.png`

## 4. OneDrive Storage and Retention

| Setting | Value | Admin center path |
|---|---|---|
| Default storage | 1 TB per user | SharePoint admin center > Settings > OneDrive storage limit |
| Retention after offboarding | 90 days | SharePoint admin center > Settings > OneDrive retention |

Evidence: `screenshots/03-sharepoint-onedrive/04-odb-storage.png`, `05-odb-retention.png`

## 5. External Sharing

| Scope | Setting |
|---|---|
| Tenant (SharePoint) | New and existing guests |
| Finance site | Existing guests only |

Admin center path: SharePoint admin center > Policies > Sharing, then Sites > Active sites > Finance > Sharing

Evidence: `screenshots/03-sharepoint-onedrive/06-spo-tenant-sharing.png`, `07-spo-finance-sharing.png`

## Decisions and Trade-offs

Record here what you changed from the brief and why.
