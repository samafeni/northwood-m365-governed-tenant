# Exchange Online

[Back to README](../README.md)

## Objective

Give each business function a shared address, keep department lists current without manual edits, tune threat protection for a professional services firm, authenticate the domain and catch risky file-transfer links.

## 1. Shared Mailboxes

| Mailbox | Full Access + Send As | Purpose |
|---|---|---|
| info@ | SG-BusinessDevelopment | General enquiries |
| careers@ | SG-Operations | Recruitment |
| projects@ | SG-ProjectManagement | Client project correspondence |
| finance@ | SG-Finance | Invoices and payments |

Admin center path: Exchange admin center > Recipients > Mailboxes > Add a shared mailbox

Evidence: `screenshots/02-exchange/01-exo-shared-mailboxes.png`

## 2. Dynamic Distribution Lists

| List | Rule |
|---|---|
| DL-Design | Department equals Design |
| DL-ProjectManagement | Department equals Project Management |
| DL-Finance | Department equals Finance |
| DL-BusinessDevelopment | Department equals Business Development |

Admin center path: Exchange admin center > Recipients > Groups > Dynamic distribution list

Evidence: `screenshots/02-exchange/02-exo-dynamic-dls.png`

## 3. Anti-spam and Anti-phishing

| Policy | Setting | Value | Reason |
|---|---|---|---|
| Anti-phishing | Impersonation protection | Founders, Head of Operations, Finance lead | Invoice fraud targets these people |
| Anti-phishing | Protected domains | Own domain plus key partner domains | |
| Anti-spam inbound | Bulk threshold | Record your value | |
| Anti-spam outbound | Limits | Record your value | |

Admin center path: Microsoft Defender portal > Email & collaboration > Policies & rules > Threat policies

Evidence: `screenshots/02-exchange/03-exo-anti-phish.png`, `04-exo-anti-spam.png`

## 4. SPF, DKIM and DMARC

| Record | Value |
|---|---|
| SPF (TXT) | `v=spf1 include:spf.protection.outlook.com -all` |
| DKIM (CNAME x2) | selector1 and selector2, values from the Defender portal |
| DMARC (TXT) | Start with `v=DMARC1; p=none; rua=mailto:...`, move to quarantine after review |

Admin center path: Defender portal > Email & collaboration > Policies & rules > Threat policies > Email authentication settings > DKIM

Evidence: `screenshots/02-exchange/05-exo-dkim-enabled.png`, `06-exo-dns-records.png`

## 5. Mail Flow Rule: File-transfer Links

| Field | Value |
|---|---|
| Name | Review external file-transfer links |
| Apply if | Sender is outside the organisation AND subject or body includes `wetransfer.com` or `dropbox.com` |
| Do the following | Redirect the message to the reviewer mailbox |
| Mode | Test first, then Enforce |

Admin center path: Exchange admin center > Mail flow > Rules

Evidence: `screenshots/02-exchange/07-exo-mail-flow-rule.png`

## Decisions and Trade-offs

Record here what you changed from the brief and why.
