# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

gogcli is a unified Go CLI (`gog`) for interacting with Google services: Gmail, Calendar, Classroom, Drive, Docs, Slides, Sheets, Contacts, Tasks, People, Groups, and Keep. It supports multiple accounts, secure keyring credential storage, and domain-wide delegation for Workspace.

## Build & Development Commands

```bash
make              # Build ./bin/gog
make tools        # Install pinned dev tools into .tools/
make fmt          # Format with goimports + gofumpt
make lint         # Run golangci-lint
make test         # Run unit tests
make ci           # Full local gate: fmt-check, lint, test

# Build and run in one step
make gog -- gmail search "from:me"
```

### Running a Single Test

```bash
go test -v ./internal/cmd -run TestGmailSearch
```

### Integration Tests (Live Google APIs)

Opt-in tests requiring stored credentials:

```bash
GOG_IT_ACCOUNT=you@gmail.com go test -tags=integration ./internal/integration
```

To avoid macOS Keychain prompts: `GOG_KEYRING_BACKEND=file GOG_KEYRING_PASSWORD=...`

## Architecture

### Project Structure

- `cmd/gog/main.go` - Entry point, calls `internal/cmd.Execute()`
- `internal/cmd/` - All command implementations (140+ files), uses Kong CLI framework
  - `root.go` - CLI struct, Execute(), global flags
  - `exit.go` - ExitError type with exit code mapping
  - Service commands: `gmail.go`, `calendar.go`, `classroom.go`, `drive.go`, `contacts.go`, `tasks.go`, `sheets.go`, `docs.go`, `people.go`, `keep.go`, `groups.go`
- `internal/googleauth/` - OAuth2 flows and auth logic
- `internal/googleapi/` - Google API client wrappers
- `internal/secrets/` - Keyring storage for tokens
- `internal/outfmt/` - Output format handling (JSON/TSV/text)
- `internal/ui/` - Color output and UI helpers
- `internal/config/` - Configuration paths and credential handling

### Key Patterns

**CLI Framework**: [alecthomas/kong](https://github.com/alecthomas/kong) with declarative nested command structs.

**Output Design**: Stdout for parseable data (JSON/TSV or human text), stderr for hints/progress/errors. Respect `--json` and `--plain` flags.

**Error Handling**: `ExitError` type in `internal/cmd/exit.go` maps errors to exit codes.

**Global Flags**: `--json`, `--plain`, `--color`, `--account`, `--force`, `--no-input`, `--verbose`

## Coding Style

- Format: `make fmt` uses goimports (local prefix `github.com/steipete/gogcli`) + gofumpt
- Keep stdout parseable; send human hints/progress to stderr
- Tests colocated as `*_test.go` next to implementation

## Commit Guidelines

- Follow Conventional Commits: `feat(service): description`, `fix(gmail): description`
- Group related changes; avoid bundling unrelated refactors
- Use `gh pr view/diff` for PR review (don't switch branches)

## Configuration Paths

- macOS: `~/Library/Application Support/gogcli/`
- Linux: `~/.config/gogcli/` (respects `$XDG_CONFIG_HOME`)
- Windows: `%AppData%\gogcli\`

Files: `config.json` (JSON5), `credentials.json` (OAuth client), `keyring/` (encrypted tokens when file backend used)

## Environment Variables

- `GOG_ACCOUNT` - Default account email
- `GOG_JSON=1` / `GOG_PLAIN=1` - Default output mode
- `GOG_COLOR=auto|always|never`
- `GOG_KEYRING_BACKEND=auto|keychain|file`
- `GOG_KEYRING_PASSWORD` - For non-interactive keyring access
