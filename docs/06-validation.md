# Validation

[Back to README](../README.md)

Each test runs as a named test user, not as an admin. Record the date, the result and the screenshot file for each.

| # | Test | Steps | Expected result | Actual result | Evidence |
|---|---|---|---|---|---|
| 1 | Guest blocked on Finance | Sign in as a Finance member. Share a Finance file with a new external address | Sharing fails. The new guest receives no invitation | | `05-validation/01-finance-guest-blocked.png` |
| 2 | Team creation restricted | Sign in as a standard user. Teams > Join or create a team | No option to create a Team | | `05-validation/02-standard-user-no-create.png` |
| 3 | WeTransfer link redirected | From an external mailbox, send a message containing a wetransfer.com link | Message lands in the reviewer mailbox | | `05-validation/03-wetransfer-redirected.png` |
| 4 | Shared channel both ways | Post from Northwood user, reply from partner user, then reverse | Both posts visible on both sides | | `05-validation/04-shared-channel-two-way.png` |
| 5 | Email authentication | Send to the mail-tester.com address | SPF, DKIM and DMARC all pass | | `05-validation/05-mail-tester-score.png` |
| 6 | PIM activation controls | As an eligible admin, activate Global Admin | MFA prompt, justification required, 4-hour maximum | | `05-validation/06-pim-activation.png` |
| 7 | Legacy auth blocked | Check sign-in logs for a legacy client attempt, or use the What If tool | Blocked by CA02 | | `05-validation/07-ca-legacy-blocked.png` |
| 8 | Diagrams render | Open both .drawio files in draw.io and both GIFs on GitHub | All four render. GIFs animate in the README | Pass | `diagrams/` |

## Issues Found During Testing

| Issue | Cause | Fix |
|---|---|---|
| | | |
