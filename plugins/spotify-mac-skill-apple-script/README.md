# Spotify Mac Agent Skill

An agent skill for agentic coding systems that enables control of Spotify on macOS. Play, pause, skip tracks, and get playback information directly through your AI coding assistant.

## What is an Agent Skill?

Agent skills are self-contained packages that extend AI coding assistants with specialized capabilities. This skill follows the [Agent Skills open standard](https://github.com/anthropics/agent-skills), making it compatible with multiple agentic coding tools including Claude Code, OpenAI Codex CLI, Cursor, and Google Gemini CLI.

Unlike general context files, skills are loaded dynamically when the agent identifies a relevant task—keeping your context window clean while providing on-demand expertise.

## Features

- **Search** - Open Spotify search visually, or use agent-assisted web search to find and play content
- **Playback control** - Play, pause, skip, previous track
- **Play by URI/URL** - Play specific tracks, albums, or playlists by Spotify URI or URL
- **Track info** - Get current track details (name, artist, album, artwork)
- **Volume control** - Get, set, increase, decrease volume
- **Position control** - Seek, fast-forward, rewind
- **Mode control** - Toggle shuffle and repeat
- **App control** - Launch, quit, check if running

## Requirements

- macOS (uses AppleScript via `osascript`)
- Spotify Desktop app installed
- Spotify account (free or premium - no Premium required!)

## Installation

### Claude Code (Plugin)

The easiest way to install for Claude Code users:

```bash
# Option A: Via marketplace
/plugin marketplace add rbouschery/marketplace
/plugin install spotify-mac-skill-apple-script@rbouschery-marketplace

# Option B: Direct install
/plugin install rbouschery/marketplace:spotify-mac-skill-apple-script
```

<details>
<summary>Manual installation</summary>

```bash
mkdir -p ~/.claude/plugins
cd ~/.claude/plugins
git clone https://github.com/rbouschery/marketplace.git
# Skill available at plugins/spotify-mac-skill-apple-script/skills/spotify-mac-skill-apple-script/
```

</details>

### OpenAI Codex CLI

Install as a [user-scoped skill](https://developers.openai.com/codex/skills/):

```bash
mkdir -p ~/.codex/skills
cd ~/.codex/skills
git clone https://github.com/rbouschery/marketplace.git temp-marketplace
mv temp-marketplace/plugins/spotify-mac-skill-apple-script/skills/spotify-mac-skill-apple-script ./spotify
rm -rf temp-marketplace
```

The skill will be available as `$spotify` or invoked automatically when you ask about music.

### Cursor

Cursor [automatically discovers skills](https://cursor.com/docs/context/skills) from `~/.claude/skills/`, so if you've already installed a Claude Code skill, Cursor will auto-load it (requires Nightly channel).

To install manually:

```bash
mkdir -p .cursor/skills  # or ~/.cursor/skills for global
cd .cursor/skills
git clone https://github.com/rbouschery/marketplace.git temp-marketplace
mv temp-marketplace/plugins/spotify-mac-skill-apple-script/skills/spotify-mac-skill-apple-script ./spotify
rm -rf temp-marketplace
```

Enable Agent Skills in Cursor Settings > Beta > Nightly channel.

### Google Gemini CLI

Install as a [workspace or user skill](https://geminicli.com/docs/cli/skills/):

```bash
# For user-global
mkdir -p ~/.gemini/skills
cd ~/.gemini/skills

git clone https://github.com/rbouschery/marketplace.git temp-marketplace
mv temp-marketplace/plugins/spotify-mac-skill-apple-script/skills/spotify-mac-skill-apple-script ./spotify
rm -rf temp-marketplace
```

Enable Agent Skills via `/settings` in Gemini CLI.

## First Run

On first use, macOS will prompt for Automation permissions. Go to:

**System Settings > Privacy & Security > Automation**

And allow your terminal app to control Spotify.

## Usage

Once installed, your AI assistant will automatically use this skill when you ask about Spotify. Examples:

```
"Play some music"
"Pause Spotify"
"Skip to the next song"
"What song is playing?"
"Turn the volume down"
"Play this playlist: spotify:playlist:37i9dQZF1DXcBWIGoYBM5M"
"Enable shuffle"
"Fast forward 30 seconds"
"Is Spotify running?"
```

## Available Scripts

| Script | Purpose |
|--------|---------|
| `play.sh` | Resume playback |
| `pause.sh` | Pause playback |
| `toggle-playback.sh` | Toggle play/pause |
| `next-track.sh` | Skip to next track |
| `previous-track.sh` | Go to previous track |
| `play-uri.sh` | Play specific URI or URL |
| `search.sh` | Open Spotify search visually |
| `get-current-track.sh` | Get current track info |
| `get-player-state.sh` | Get player state |
| `get-volume.sh` | Get current volume |
| `set-volume.sh` | Set volume (0-100) |
| `volume-up.sh` | Increase volume by 10 |
| `volume-down.sh` | Decrease volume by 10 |
| `get-position.sh` | Get playback position |
| `set-position.sh` | Seek to position |
| `fast-forward.sh` | Forward 10 seconds |
| `rewind.sh` | Rewind 10 seconds |
| `toggle-shuffle.sh` | Toggle shuffle |
| `toggle-repeat.sh` | Toggle repeat |
| `get-modes.sh` | Get shuffle/repeat status |
| `is-running.sh` | Check if Spotify running |
| `launch.sh` | Launch Spotify |
| `quit.sh` | Quit Spotify |
| `open-playlists.sh` | Open your playlists |
| `open-library.sh` | Open your library |
| `open-liked-songs.sh` | Play your liked songs |

## Manual Script Usage

Scripts can also be run directly:

```bash
# Visual search (opens Spotify app)
./scripts/search.sh "bohemian rhapsody"
./scripts/search.sh "artist:queen"
./scripts/search.sh "playlist:hot country"

# Play by URI or URL
./scripts/play-uri.sh "spotify:track:4uLU6hMCjMI75M1A2tKUQC"
./scripts/play-uri.sh "https://open.spotify.com/track/6l8GvAyoUZwWDgF1e4822w"
./scripts/play-uri.sh "spotify:playlist:37i9dQZF1DXcBWIGoYBM5M"

# Basic playback
./scripts/play.sh
./scripts/pause.sh
./scripts/next-track.sh

# Get track info
./scripts/get-current-track.sh

# Volume control
./scripts/set-volume.sh 50
./scripts/volume-up.sh

# Seeking
./scripts/set-position.sh 30
./scripts/fast-forward.sh
```

## Agent-Assisted Search

To search and play automatically, the agent uses web search to find Spotify URLs:

1. Agent searches: `site:open.spotify.com [query]` (e.g., "site:open.spotify.com bohemian rhapsody")
2. Gets the URL from results (e.g., `https://open.spotify.com/track/6l8GvAyoUZwWDgF1e4822w`)
3. Plays it: `./scripts/play-uri.sh "https://open.spotify.com/track/..."`

This works for tracks, albums, playlists, and artists. Just ask your AI assistant to "play [song name]" and it will handle the search automatically.

## Output Format

Scripts use delimiters for structured output:
- `<<>>` separates fields within a record
- `ERROR:` prefix indicates an error

Track format: `name<<>>artist<<>>album<<>>albumArtist<<>>duration<<>>position<<>>trackNumber<<>>discNumber<<>>id<<>>spotifyUrl<<>>artworkUrl<<>>popularity`

## Spotify URI Format

Play specific content using Spotify URIs:
- **Tracks**: `spotify:track:<track_id>`
- **Albums**: `spotify:album:<album_id>`
- **Playlists**: `spotify:playlist:<playlist_id>`

Get URIs from Spotify: Right-click > Share > Copy Spotify URI

## Limitations

The AppleScript API does **NOT** support:
- Adding to playlists
- Viewing or managing queue
- Liking/saving tracks
- Browsing library
- Searching private/personal playlists (use URI instead)

For these features, you would need the Spotify Web API (requires Premium + OAuth). This skill works without Premium or any authentication.

## Project Structure

```
spotify-mac-skill-apple-script/
├── .claude-plugin/
│   └── plugin.json           # Claude Code plugin manifest
├── skills/
│   └── spotify-mac-skill-apple-script/
│       └── SKILL.md          # Skill definition (Agent Skills standard)
├── scripts/                  # Executable shell scripts
│   ├── play.sh
│   ├── pause.sh
│   └── ...
├── reference/
│   └── applescript-patterns.md
├── README.md
└── LICENSE
```

## Troubleshooting

### "Spotify got an error"
Make sure Spotify is running: `./scripts/launch.sh`

### Permission denied
Make scripts executable: `chmod +x scripts/*.sh`

### Automation permission errors
Grant Terminal access to Spotify in System Settings > Privacy & Security > Automation

### No track info returned
Check that a track is playing, not just paused. Some operations require active playback.

## Contributing

Contributions welcome! Please feel free to submit issues and pull requests.

## License

MIT License - see LICENSE file for details.

## Credits

Created by [Robert Bouschery](https://github.com/rbouschery)

## References

- [Agent Skills Standard](https://github.com/anthropics/agent-skills)
- [spotify-node-applescript](https://github.com/andrehaveman/spotify-node-applescript)
- [SpotifyControl](https://github.com/dronir/SpotifyControl)
