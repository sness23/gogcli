# gog gmail

Gmail operations: search, send, labels, drafts, settings, and batch operations.

## Commands

### Read

| Command | Description |
|---------|-------------|
| `gog gmail search <query>` | Search threads using Gmail query syntax |
| `gog gmail get <messageId>` | Get a message (full\|metadata\|raw) |
| `gog gmail thread get <threadId>` | Get a thread with all messages |
| `gog gmail attachment <messageId> <attachmentId>` | Download a single attachment |
| `gog gmail url <threadId>` | Print Gmail web URL for a thread |
| `gog gmail history --since <historyId>` | Get Gmail history since a history ID |

### Organize

| Command | Description |
|---------|-------------|
| `gog gmail thread modify <threadId>` | Modify thread labels |
| `gog gmail labels list` | List all labels |
| `gog gmail labels get <labelId>` | Get label details (includes message counts) |
| `gog gmail labels create <name>` | Create a label |
| `gog gmail labels update <labelId> --name <name>` | Rename a label |
| `gog gmail labels delete <labelId>` | Delete a label |
| `gog gmail batch mark-read --query <query>` | Mark matching threads as read |
| `gog gmail batch delete --query <query>` | Delete matching threads |
| `gog gmail batch label --query <query>` | Add/remove labels on matching threads |
| `gog gmail batch archive --query <query>` | Archive matching threads |

### Write

| Command | Description |
|---------|-------------|
| `gog gmail send` | Send an email |
| `gog gmail drafts list` | List drafts |
| `gog gmail drafts create` | Create a draft |
| `gog gmail drafts update <draftId>` | Update a draft |
| `gog gmail drafts send <draftId>` | Send a draft |
| `gog gmail track setup` | Set up email open tracking |
| `gog gmail track opens <trackingId>` | Check tracking opens |
| `gog gmail track status` | View tracking status |

### Settings (Admin)

| Command | Description |
|---------|-------------|
| `gog gmail settings filters list` | List filters |
| `gog gmail settings filters create` | Create a filter |
| `gog gmail settings filters delete <filterId>` | Delete a filter |
| `gog gmail settings delegates list` | List delegates |
| `gog gmail settings delegates add --email <email>` | Add a delegate |
| `gog gmail settings delegates remove --email <email>` | Remove a delegate |
| `gog gmail settings forwarding list` | List forwarding addresses |
| `gog gmail settings forwarding add --email <email>` | Add forwarding address |
| `gog gmail settings autoforward get` | Get auto-forwarding settings |
| `gog gmail settings autoforward enable --email <email>` | Enable auto-forwarding |
| `gog gmail settings autoforward disable` | Disable auto-forwarding |
| `gog gmail settings sendas list` | List send-as addresses |
| `gog gmail settings sendas create --email <email>` | Create send-as alias |
| `gog gmail settings vacation get` | Get vacation responder |
| `gog gmail settings vacation enable` | Enable vacation responder |
| `gog gmail settings vacation disable` | Disable vacation responder |
| `gog gmail settings watch start` | Start Gmail watch (Pub/Sub push) |
| `gog gmail settings watch serve` | Serve watch webhook |

## Examples

```bash
# Search
gog gmail search 'newer_than:7d' --max 10
gog gmail search 'from:boss@example.com is:unread'
gog gmail search 'has:attachment filename:pdf'

# Get thread and download attachments
gog gmail thread get <threadId>
gog gmail thread get <threadId> --download
gog gmail thread get <threadId> --download --out-dir ./attachments

# Modify thread labels
gog gmail thread modify <threadId> --add STARRED --remove INBOX

# Send email
gog gmail send --to a@b.com --subject "Hi" --body "Hello"
gog gmail send --to a@b.com --subject "Hi" --body-file ./message.txt
gog gmail send --to a@b.com --subject "Hi" --body-html "<p>Hello</p>"
gog gmail send --to a@b.com --subject "Hi" --body "text" --body-html "<p>HTML</p>"

# Send with tracking
gog gmail send --to a@b.com --subject "Hi" --body-html "<p>Hello</p>" --track

# Drafts
gog gmail drafts create --subject "Draft" --body "Body"
gog gmail drafts send <draftId>

# Batch operations
gog gmail batch mark-read --query 'from:noreply@example.com'
gog gmail batch archive --query 'older_than:1y'
gog gmail batch label --query 'from:boss@example.com' --add-labels IMPORTANT

# Labels
gog gmail labels list
gog gmail labels create "My Label"

# Filters
gog gmail settings filters list
gog gmail settings filters create --from 'noreply@example.com' --label 'Notifications'
```

## Key Flags

### `gog gmail search`

| Flag | Description |
|------|-------------|
| `--max <n>` | Max results (default: 10) |
| `--page <token>` | Page token for pagination |
| `--oldest` | Show first message date instead of last |

### `gog gmail send`

| Flag | Description |
|------|-------------|
| `--to <email>` | Recipient email |
| `--cc <email>` | CC recipients |
| `--bcc <email>` | BCC recipients |
| `--subject <text>` | Email subject |
| `--body <text>` | Plain text body |
| `--body-html <html>` | HTML body |
| `--body-file <path>` | Read body from file (use `-` for stdin) |
| `--track` | Enable open tracking (requires HTML body, single recipient) |
| `--track-split` | Send per-recipient with individual tracking |

### `gog gmail thread get`

| Flag | Description |
|------|-------------|
| `--download` | Download attachments |
| `--out-dir <path>` | Output directory for attachments |
| `--format <format>` | Message format: full\|metadata\|raw |
