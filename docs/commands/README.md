# Command Reference

Per-tool documentation for `gog` CLI commands.

## Tools

| Tool | Description |
|------|-------------|
| [auth](auth.md) | Authentication and credential management |
| [gmail](gmail.md) | Gmail: search, send, labels, drafts, settings |
| [calendar](calendar.md) | Google Calendar: events, invitations, free/busy |
| [classroom](classroom.md) | Google Classroom: courses, rosters, coursework |
| [drive](drive.md) | Google Drive: files, folders, sharing |
| [docs](docs.md) | Google Docs: create, export, read |
| [slides](slides.md) | Google Slides: create, export |
| [sheets](sheets.md) | Google Sheets: read, write, format |
| [contacts](contacts.md) | Google Contacts: search, create, directory |
| [tasks](tasks.md) | Google Tasks: task lists and tasks |
| [people](people.md) | Google People: profile information |
| [keep](keep.md) | Google Keep: notes (Workspace only) |
| [groups](groups.md) | Google Groups: membership (Workspace only) |

## Global Flags

All commands support these flags:

| Flag | Description |
|------|-------------|
| `--account <email>` | Account to use (overrides `GOG_ACCOUNT`) |
| `--json` | Output JSON to stdout |
| `--plain` | Output stable TSV to stdout (no colors) |
| `--color <mode>` | Color mode: auto\|always\|never |
| `--force` | Skip confirmations for destructive commands |
| `--no-input` | Never prompt; fail instead |
| `--verbose` | Enable verbose logging |
| `--help` | Show help |

## Environment Variables

| Variable | Description |
|----------|-------------|
| `GOG_ACCOUNT` | Default account email |
| `GOG_JSON=1` | Default JSON output |
| `GOG_PLAIN=1` | Default plain output |
| `GOG_COLOR` | Color mode: auto\|always\|never |
| `GOG_KEYRING_BACKEND` | Keyring backend: auto\|keychain\|file |
| `GOG_KEYRING_PASSWORD` | Password for file keyring (non-interactive) |

## Quick Reference

```bash
# Get help
gog --help
gog gmail --help
gog gmail search --help

# Full expanded command list
GOG_HELP=full gog --help
```
