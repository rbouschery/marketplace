# Apple Mail Plugin for Claude Code

A Claude Code plugin that enables interaction with Apple Mail on macOS. Read, send, search, and manage emails directly through Claude.

## Features

- **Read emails** - Get recent emails, search by query, fetch by ID
- **Send emails** - Compose and send emails with CC/BCC support
- **Drafts** - Create drafts, reply drafts, and send from compose window
- **Manage** - Archive, delete, mark read/unread
- **Accounts** - List accounts, mailboxes, and unread counts

## Requirements

- macOS (uses AppleScript via `osascript`)
- Apple Mail configured with at least one email account
- Claude Code CLI

## Installation

### Option 1: Marketplace (Easiest)

```bash
# Add the Sempervirens Labs marketplace
/plugin marketplace add rbouschery/marketplace

# Install the Apple Mail plugin
/plugin install apple-mail@rbouschery-marketplace
```

### Option 2: Direct Install

```bash
/plugin install rbouschery/marketplace:apple-mail
```

### Option 3: Manual Clone

```bash
mkdir -p ~/.claude/plugins
cd ~/.claude/plugins
git clone https://github.com/rbouschery/marketplace.git
# Plugin available at plugins/apple-mail
```

## First Run

On first use, macOS will prompt for Automation permissions. Go to:

**System Settings > Privacy & Security > Automation**

And allow Terminal (or your terminal app) to control Apple Mail.

## Usage

Once installed, Claude Code will automatically use this skill when you ask about email. Examples:

```
"Show me my recent emails"
"Check my unread emails in iCloud"
"Send an email to john@example.com about the meeting"
"Search for emails from Amazon"
"Archive all newsletters"
"Create a draft reply to the last email"
"Delete the spam emails"
```

## Available Scripts

| Script | Purpose |
|--------|---------|
| `list-accounts.sh` | List all email accounts |
| `list-mailboxes.sh` | List mailboxes/folders |
| `get-unread-count.sh` | Count unread emails |
| `get-emails.sh` | Get recent emails |
| `get-email-by-id.sh` | Get specific email by ID |
| `search-emails.sh` | Search emails |
| `send-email.sh` | Send an email |
| `create-draft.sh` | Create a draft |
| `create-reply-draft.sh` | Create a reply draft |
| `send-draft.sh` | Send front-most draft |
| `archive-email.sh` | Archive an email |
| `delete-email.sh` | Delete an email |
| `mark-read.sh` | Mark as read |
| `mark-unread.sh` | Mark as unread |

## Manual Script Usage

Scripts can also be run directly from the plugin directory:

```bash
# List accounts
./scripts/list-accounts.sh

# Get 10 recent emails from INBOX
./scripts/get-emails.sh "iCloud" "INBOX" 10 false false

# Send an email
./scripts/send-email.sh "to@example.com" "Subject" "Body text"

# Search emails
./scripts/search-emails.sh "meeting notes" "" "" 20
```

## Output Format

Scripts use delimiters for structured output:
- `<<>>` separates fields within a record
- `|||` separates multiple records

Email format: `id<<>>subject<<>>sender<<>>to<<>>cc<<>>bcc<<>>dateSent<<>>isRead<<>>content|||`

## Project Structure

```
apple-mail/
├── .claude-plugin/
│   ├── plugin.json           # Plugin manifest
│   └── marketplace.json      # Marketplace catalog
├── skills/
│   └── apple-mail/
│       └── SKILL.md          # Skill definition
├── scripts/                  # Executable shell scripts
│   ├── list-accounts.sh
│   ├── get-emails.sh
│   └── ...
├── reference/
│   └── applescript-patterns.md
├── README.md
└── LICENSE
```

## Troubleshooting

### "Mail got an error: Can't get mailbox"
Specify the account name: `./scripts/get-emails.sh "iCloud" "INBOX" 10`

### Permission denied
Make scripts executable: `chmod +x scripts/*.sh`

### Automation permission errors
Grant Terminal access to Mail in System Settings > Privacy & Security > Automation

### Timeout on large mailboxes
The scripts have default timeouts. For large operations, the AppleScript may need more time.

## Contributing

Contributions welcome! Please feel free to submit issues and pull requests.

## License

MIT License - see LICENSE file for details.

## Credits

Created by [Robert Bouschery](https://github.com/rbouschery)
