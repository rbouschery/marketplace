---
name: manage
description: Manage emails (archive, delete, mark read/unread)
argument-hint: "<message_id> [action]"
---

Manage emails in Apple Mail.

## Commands

| Action | Script |
|--------|--------|
| Archive | `scripts/archive-email.sh <message_id> [account] [mailbox] [archive_mailbox]` |
| Delete | `scripts/delete-email.sh <message_id> [account] [mailbox]` |
| Mark read | `scripts/mark-read.sh <message_id> [account] [mailbox]` |
| Mark unread | `scripts/mark-unread.sh <message_id> [account] [mailbox]` |

## Usage

Get the message ID first using `/apple-mail:read`, then run the management action.
