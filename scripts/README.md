# Scripts

[Back to README](../README.md)

This folder holds no scripts on purpose.

PowerShell sits outside the scope of this project. The goal was to prove every setting through the admin centers a small firm's Head of Operations will use after handover. Where an admin center offered no option, I used Graph Explorer with delegated permissions.

## Graph Explorer Queries Used

Graph Explorer: https://developer.microsoft.com/graph/graph-explorer

### Group creation restriction, naming and label support

Read the current Group.Unified setting:

```
GET https://graph.microsoft.com/v1.0/groupSettings
```

If none exists, create one from the Group.Unified template:

```
POST https://graph.microsoft.com/v1.0/groupSettings
{
  "templateId": "62375ab9-6b52-47ed-826b-58e47e0e304b",
  "values": [
    { "name": "EnableGroupCreation", "value": "false" },
    { "name": "GroupCreationAllowedGroupId", "value": "<SG-Operations object ID>" },
    { "name": "EnableMIPLabels", "value": "true" }
  ]
}
```

If one exists, update it:

```
PATCH https://graph.microsoft.com/v1.0/groupSettings/{id}
```

Permission: Directory.ReadWrite.All (consent as Global Admin through a PIM activation)

### Verification queries

| What | Query |
|---|---|
| Conditional Access policies | `GET /v1.0/identity/conditionalAccess/policies` |
| PIM eligible assignments | `GET /v1.0/roleManagement/directory/roleEligibilitySchedules` |
| Group expiration policy | `GET /v1.0/groupLifecyclePolicies` |
| SharePoint tenant sharing | `GET /v1.0/admin/sharepoint/settings` |
| Cross-tenant partners | `GET /v1.0/policies/crossTenantAccessPolicy/partners` |

## Admin Center Paths Used Instead of PowerShell

| Task | Admin center path |
|---|---|
| Shared mailboxes and permissions | Exchange admin center > Recipients > Mailboxes |
| Dynamic distribution lists | Exchange admin center > Recipients > Groups |
| Mail flow rule | Exchange admin center > Mail flow > Rules |
| DKIM | Defender portal > Email & collaboration > Policies & rules > Threat policies > Email authentication settings |
| OneDrive storage and retention | SharePoint admin center > Settings |
| Site-level sharing | SharePoint admin center > Sites > Active sites > site > Sharing |
| Sensitivity labels | Purview portal > Information protection > Sensitivity labels |
| Naming policy and expiration | Entra admin center > Groups |
