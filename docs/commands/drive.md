# gog drive

Google Drive operations: list, search, upload, download, share, and organize files.

## Commands

| Command | Description |
|---------|-------------|
| `gog drive ls` | List files in a folder (default: root) |
| `gog drive search <query>` | Full-text search across Drive |
| `gog drive get <fileId>` | Get file metadata |
| `gog drive download <fileId>` | Download a file (exports Google Docs formats) |
| `gog drive upload <localPath>` | Upload a file |
| `gog drive copy <fileId> <name>` | Copy a file |
| `gog drive mkdir <name>` | Create a folder |
| `gog drive rename <fileId> <newName>` | Rename a file or folder |
| `gog drive move <fileId> --parent <folderId>` | Move a file to a different folder |
| `gog drive delete <fileId>` | Delete a file (moves to trash) |
| `gog drive share <fileId>` | Share a file or folder |
| `gog drive unshare <fileId> <permissionId>` | Remove a permission |
| `gog drive permissions <fileId>` | List permissions on a file |
| `gog drive url <fileId>` | Print web URL for a file |
| `gog drive comments <fileId>` | Manage comments on files |
| `gog drive drives` | List shared drives (Team Drives) |

## Examples

```bash
# List files
gog drive ls
gog drive ls --parent <folderId>
gog drive ls --max 50

# Search
gog drive search "invoice"
gog drive search "project filetype:pdf"

# Get file info
gog drive get <fileId>
gog drive url <fileId>

# Download
gog drive download <fileId>
gog drive download <fileId> --out ./downloaded.pdf
gog drive download <fileId> --format pdf   # Export Google Doc as PDF
gog drive download <fileId> --format docx  # Export Google Doc as DOCX

# Upload
gog drive upload ./document.pdf
gog drive upload ./document.pdf --parent <folderId>
gog drive upload ./document.pdf --name "New Name.pdf"

# Organize
gog drive mkdir "New Folder"
gog drive mkdir "Subfolder" --parent <parentFolderId>
gog drive rename <fileId> "New Name"
gog drive move <fileId> --parent <destinationFolderId>
gog drive copy <fileId> "Copy Name"

# Delete (moves to trash)
gog drive delete <fileId>

# Sharing
gog drive permissions <fileId>
gog drive share <fileId> --email user@example.com --role reader
gog drive share <fileId> --email user@example.com --role writer
gog drive share <fileId> --anyone --role reader
gog drive unshare <fileId> <permissionId>

# Shared drives
gog drive drives --max 100
```

## Key Flags

### `gog drive ls`

| Flag | Description |
|------|-------------|
| `--max <n>` | Max results (default: 20) |
| `--page <token>` | Page token |
| `--query <filter>` | Drive query filter |
| `--parent <folderId>` | Folder ID to list (default: root) |

### `gog drive download`

| Flag | Description |
|------|-------------|
| `--out <path>` | Output file path |
| `--format <format>` | Export format for Google Docs: pdf\|csv\|xlsx\|pptx\|txt\|png\|docx |

### `gog drive upload`

| Flag | Description |
|------|-------------|
| `--name <name>` | Override filename |
| `--parent <folderId>` | Destination folder ID |

### `gog drive share`

| Flag | Description |
|------|-------------|
| `--email <email>` | Share with specific user |
| `--anyone` | Make publicly accessible |
| `--role <role>` | Permission: reader\|writer (default: reader) |
| `--discoverable` | Allow file discovery in search (anyone/domain only) |
