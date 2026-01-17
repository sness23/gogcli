# gog auth

Authentication and credential management.

## Commands

| Command | Description |
|---------|-------------|
| `gog auth credentials <path>` | Store OAuth client credentials (from Google Cloud Console) |
| `gog auth add <email>` | Authorize and store a refresh token |
| `gog auth list` | List stored accounts |
| `gog auth list --check` | Validate stored refresh tokens |
| `gog auth status` | Show auth configuration and keyring backend |
| `gog auth remove <email>` | Remove a stored refresh token |
| `gog auth keyring [backend]` | Show/set keyring backend (auto\|keychain\|file) |
| `gog auth services` | List supported auth services and scopes |
| `gog auth manage` | Open accounts manager in browser |
| `gog auth service-account set <email> --key <path>` | Configure service account (Workspace domain-wide delegation) |
| `gog auth service-account status <email>` | Show service account status |
| `gog auth service-account unset <email>` | Remove service account |
| `gog auth tokens list` | List stored tokens by key |
| `gog auth tokens delete <email>` | Delete a stored refresh token |
| `gog auth tokens export <email> --out <path>` | Export refresh token to file |
| `gog auth tokens import <path>` | Import refresh token from file |
| `gog auth keep <email> --key <path>` | Legacy: configure Keep service account |

## Examples

```bash
# Initial setup
gog auth credentials ~/Downloads/client_secret_....json
gog auth add you@gmail.com

# List accounts and verify tokens
gog auth list
gog auth list --check

# Show current auth state
gog auth status

# Authorize with specific services
gog auth add you@gmail.com --services gmail,calendar
gog auth add you@gmail.com --services drive --readonly

# Force consent screen (for re-auth or new scopes)
gog auth add you@gmail.com --force-consent

# Configure keyring backend
gog auth keyring file
gog auth keyring keychain

# Service account for Workspace
gog auth service-account set you@company.com --key ~/service-account.json
```

## Flags

### `gog auth add`

| Flag | Description |
|------|-------------|
| `--manual` | Browserless auth flow (paste redirect URL) |
| `--force-consent` | Force consent screen to obtain a refresh token |
| `--services <csv>` | Services to authorize (default: user) |
| `--readonly` | Use read-only scopes where available |
| `--drive-scope <mode>` | Drive scope: full\|readonly\|file (default: full) |

### `gog auth list`

| Flag | Description |
|------|-------------|
| `--check` | Verify refresh tokens by exchanging for access token |
| `--timeout <duration>` | Per-token check timeout (default: 15s) |
