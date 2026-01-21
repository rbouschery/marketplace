---
name: search
description: Search and play music on Spotify
argument-hint: "<song, artist, album, or playlist>"
---

Search for music and play it on Spotify.

## Workflow

1. Use web search: `site:open.spotify.com <query>`
2. Extract the Spotify URL from results
3. Play using: `scripts/play-uri.sh "<spotify_url>"`

## Examples

- User: "play bohemian rhapsody"
  1. Search: `site:open.spotify.com bohemian rhapsody`
  2. Get URL: `https://open.spotify.com/track/...`
  3. Run: `scripts/play-uri.sh "https://open.spotify.com/track/..."`

Works for tracks, albums, playlists, and artists.
