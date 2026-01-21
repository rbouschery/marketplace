---
name: send
description: Send or compose emails in Apple Mail
argument-hint: "<to> <subject>"
---

Send and compose emails in Apple Mail.

## Commands

| Action | Script |
|--------|--------|
| Send email | `scripts/send-email.sh <to> <subject> <body> [cc] [bcc] [from]` |
| Create draft | `scripts/create-draft.sh <subject> <body> [to] [cc] [bcc] [from]` |
| Reply to email | `scripts/create-reply-draft.sh <message_id> <body> [reply_all] [account] [mailbox]` |
| Send draft | `scripts/send-draft.sh` |

## Usage

Help the user compose their email, then run the appropriate script.
