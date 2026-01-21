---
name: read
description: Read and search emails in Apple Mail
argument-hint: "[search query] or [mailbox]"
---

Read and search emails in Apple Mail.

## Commands

| Action | Script |
|--------|--------|
| List accounts | `scripts/list-accounts.sh` |
| List mailboxes | `scripts/list-mailboxes.sh [account]` |
| Get emails | `scripts/get-emails.sh [account] [mailbox] [limit] [include_content] [unread_only]` |
| Get by ID | `scripts/get-email-by-id.sh <id> [account] [mailbox] [include_content]` |
| Search | `scripts/search-emails.sh <query> [account] [mailbox] [limit]` |
| Unread count | `scripts/get-unread-count.sh [account] [mailbox]` |

## Output Format

Records separated by `|||`, fields by `<<>>`:
`id<<>>subject<<>>sender<<>>to<<>>cc<<>>bcc<<>>dateSent<<>>isRead<<>>content`
