# Apple Mail Agent Skill

An agent skill for agentic coding systems that enables interaction with Apple Mail on macOS. Read, send, search, and manage emails directly through your AI coding assistant.

## What is an Agent Skill?

Agent skills are self-contained packages that extend AI coding assistants with specialized capabilities. This skill follows the [Agent Skills open standard](https://github.com/anthropics/agent-skills), making it compatible with multiple agentic coding tools including Claude Code, OpenAI Codex CLI, Cursor, and Google Gemini CLI.

Unlike general context files, skills are loaded dynamically when the agent identifies a relevant task—keeping your context window clean while providing on-demand expertise.

## Features

- **Read emails** - Get recent emails, search by query, fetch by ID
- **Send emails** - Compose and send emails with CC/BCC support
- **Drafts** - Create drafts, reply drafts, and send from compose window
- **Manage** - Archive, delete, mark read/unread
- **Accounts** - List accounts, mailboxes, and unread counts

## Requirements

- macOS (uses AppleScript via `osascript`)
- Apple Mail configured with at least one email account

## Installation

### Claude Code (Plugin)

The easiest way to install for Claude Code users:

```bash
# Option A: Via marketplace
/plugin marketplace add rbouschery/marketplace
/plugin install apple-mail@rbouschery-marketplace

# Option B: Direct install
/plugin install rbouschery/marketplace:apple-mail
```

<details>
<summary>Manual installation</summary>

```bash
mkdir -p ~/.claude/plugins
cd ~/.claude/plugins
git clone https://github.com/rbouschery/marketplace.git
# Skill available at plugins/apple-mail/skills/apple-mail/
```

</details>

### OpenAI Codex CLI

Install as a [user-scoped skill](https://developers.openai.com/codex/skills/):

```bash
# Clone to your Codex skills directory
mkdir -p ~/.codex/skills
cd ~/.codex/skills
git clone https://github.com/rbouschery/marketplace.git temp-marketplace
mv temp-marketplace/plugins/apple-mail/skills/apple-mail ./apple-mail
rm -rf temp-marketplace

# Restart Codex to pick up the new skill
```

The skill will be available as `$apple-mail` or invoked automatically when you ask about email.

### Cursor

Cursor [automatically discovers skills](https://cursor.com/docs/context/skills) from `~/.claude/skills/`, so if you've already installed a Claude Code skill, Cursor will auto-load it (requires Nightly channel).

To install manually:

```bash
# Clone to your project or user skills directory
mkdir -p .cursor/skills  # or ~/.cursor/skills for global
cd .cursor/skills
git clone https://github.com/rbouschery/marketplace.git temp-marketplace
mv temp-marketplace/plugins/apple-mail/skills/apple-mail ./apple-mail
rm -rf temp-marketplace
```

Enable Agent Skills in Cursor Settings > Beta > Nightly channel.

### Google Gemini CLI

Install as a [workspace or user skill](https://geminicli.com/docs/cli/skills/):

```bash
# For workspace-specific (committed to repo)
mkdir -p .gemini/skills
cd .gemini/skills

# Or for user-global
mkdir -p ~/.gemini/skills
cd ~/.gemini/skills

# Clone the skill
git clone https://github.com/rbouschery/marketplace.git temp-marketplace
mv temp-marketplace/plugins/apple-mail/skills/apple-mail ./apple-mail
rm -rf temp-marketplace
```

Enable Agent Skills via `/settings` in Gemini CLI, then toggle "Agent Skills" to true.

## First Run

On first use, macOS will prompt for Automation permissions. Go to:

**System Settings > Privacy & Security > Automation**

And allow your terminal app to control Apple Mail.

## Usage

Once installed, your AI assistant will automatically use this skill when you ask about email. Examples:

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

Scripts can also be run directly:

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
│   └── plugin.json           # Claude Code plugin manifest
├── skills/
│   └── apple-mail/
│       └── SKILL.md          # Skill definition (Agent Skills standard)
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

## References

- [Agent Skills Standard](https://github.com/anthropics/agent-skills)
- [OpenAI Codex Skills](https://developers.openai.com/codex/skills/)
- [Cursor Agent Skills](https://cursor.com/docs/context/skills)
- [Gemini CLI Skills](https://geminicli.com/docs/cli/skills/)
