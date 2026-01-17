# gog keep

Google Keep operations (Workspace only, requires service account with domain-wide delegation).

## Prerequisites

Keep API requires Google Workspace and a service account with domain-wide delegation:

```bash
# Configure service account
gog auth service-account set you@yourdomain.com --key ~/service-account.json

# Verify configuration
gog auth status --account you@yourdomain.com
```

## Commands

| Command | Description |
|---------|-------------|
| `gog keep list` | List notes |
| `gog keep get <noteId>` | Get a note |
| `gog keep search <query>` | Search notes by text (client-side filtering) |
| `gog keep attachment <attachmentName>` | Download an attachment |

## Examples

```bash
# List notes
gog keep list --account you@yourdomain.com
gog keep list --max 50

# Filter notes by creation time
gog keep list --filter 'create_time > "2024-01-01T00:00:00Z"'

# Get a specific note
gog keep get <noteId>
gog keep get notes/abc123

# Search notes (client-side text search)
gog keep search "project meeting"
gog keep search "TODO" --max 500

# Download an attachment
gog keep attachment notes/<noteId>/attachments/<attachmentId>
gog keep attachment notes/<noteId>/attachments/<attachmentId> --out ./image.jpg
gog keep attachment notes/<noteId>/attachments/<attachmentId> --mime-type image/jpeg
```

## Key Flags

### Global Keep Flags

| Flag | Description |
|------|-------------|
| `--service-account <path>` | Path to service account JSON file |
| `--impersonate <email>` | Email to impersonate (required with --service-account) |

### `gog keep list`

| Flag | Description |
|------|-------------|
| `--max <n>` | Max results (default: 100) |
| `--page <token>` | Page token |
| `--filter <expr>` | Filter expression (e.g., 'create_time > "2024-01-01T00:00:00Z"') |

### `gog keep search`

| Flag | Description |
|------|-------------|
| `--max <n>` | Max results to fetch before filtering (default: 500) |

### `gog keep attachment`

| Flag | Description |
|------|-------------|
| `--mime-type <type>` | MIME type of attachment (default: application/octet-stream) |
| `--out <path>` | Output file path |

## Notes

- Keep API is **Workspace-only** and requires domain-wide delegation
- The `search` command performs client-side filtering (fetches all notes then filters)
- Attachment names follow the format: `notes/<noteId>/attachments/<attachmentId>`
