# gog slides

Google Slides operations: create, copy, export, and view presentations.

## Commands

| Command | Description |
|---------|-------------|
| `gog slides info <presentationId>` | Get Google Slides presentation metadata |
| `gog slides create <title>` | Create a Google Slides presentation |
| `gog slides copy <presentationId> <title>` | Copy a Google Slides presentation |
| `gog slides export <presentationId>` | Export a Google Slides presentation (pdf\|pptx) |

## Examples

```bash
# Get presentation info
gog slides info <presentationId>

# Create a new presentation
gog slides create "My Deck"
gog slides create "My Deck" --parent <folderId>

# Copy a presentation
gog slides copy <presentationId> "My Deck Copy"
gog slides copy <presentationId> "Copy" --parent <folderId>

# Export to different formats
gog slides export <presentationId> --format pptx --out ./deck.pptx
gog slides export <presentationId> --format pdf --out ./deck.pdf
```

## Key Flags

### `gog slides export`

| Flag | Description |
|------|-------------|
| `--format <format>` | Export format: pdf\|pptx (default: pptx) |
| `--out <path>` | Output file path |

### `gog slides create` / `gog slides copy`

| Flag | Description |
|------|-------------|
| `--parent <folderId>` | Destination folder ID |
