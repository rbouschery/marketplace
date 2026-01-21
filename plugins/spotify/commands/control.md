---
name: control
description: Control Spotify playback (play, pause, next, previous, volume)
argument-hint: "[play|pause|next|prev|volume <0-100>]"
---

Control Spotify playback on macOS. Run scripts from the plugin's scripts directory.

## Commands

| Action | Script |
|--------|--------|
| Play | `scripts/play.sh` |
| Pause | `scripts/pause.sh` |
| Toggle | `scripts/toggle-playback.sh` |
| Next track | `scripts/next-track.sh` |
| Previous | `scripts/previous-track.sh` |
| Get volume | `scripts/get-volume.sh` |
| Set volume | `scripts/set-volume.sh <0-100>` |
| Volume up | `scripts/volume-up.sh` |
| Volume down | `scripts/volume-down.sh` |

## Usage

Interpret the user's request and run the appropriate script.
