# gog docs

Google Docs operations: create, copy, export, and read documents.

## Commands

| Command | Description |
|---------|-------------|
| `gog docs info <docId>` | Get Google Doc metadata |
| `gog docs cat <docId>` | Print a Google Doc as plain text |
| `gog docs create <title>` | Create a Google Doc |
| `gog docs copy <docId> <title>` | Copy a Google Doc |
| `gog docs export <docId>` | Export a Google Doc (pdf\|docx\|txt) |

## Examples

```bash
# Get doc info
gog docs info <docId>

# Read doc as plain text
gog docs cat <docId>
gog docs cat <docId> --max-bytes 10000

# Create a new doc
gog docs create "My Document"
gog docs create "My Document" --parent <folderId>

# Copy a doc
gog docs copy <docId> "My Document Copy"
gog docs copy <docId> "Copy" --parent <folderId>

# Export to different formats
gog docs export <docId> --format pdf --out ./document.pdf
gog docs export <docId> --format docx --out ./document.docx
gog docs export <docId> --format txt --out ./document.txt
```

## Key Flags

### `gog docs export`

| Flag | Description |
|------|-------------|
| `--format <format>` | Export format: pdf\|docx\|txt (default: pdf) |
| `--out <path>` | Output file path |

### `gog docs cat`

| Flag | Description |
|------|-------------|
| `--max-bytes <n>` | Max bytes to read (default: 2000000, 0 = unlimited) |

### `gog docs create` / `gog docs copy`

| Flag | Description |
|------|-------------|
| `--parent <folderId>` | Destination folder ID |
