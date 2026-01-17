# gog contacts

Google Contacts operations: search, list, create, update, and delete contacts.

## Commands

| Command | Description |
|---------|-------------|
| `gog contacts list` | List contacts |
| `gog contacts search <query>` | Search contacts by name/email/phone |
| `gog contacts get <resourceName>` | Get a contact |
| `gog contacts create` | Create a contact |
| `gog contacts update <resourceName>` | Update a contact |
| `gog contacts delete <resourceName>` | Delete a contact |
| `gog contacts directory list` | List Workspace directory contacts |
| `gog contacts directory search <query>` | Search Workspace directory |
| `gog contacts other list` | List "other" contacts (people you've interacted with) |
| `gog contacts other search <query>` | Search "other" contacts |

## Examples

```bash
# List contacts
gog contacts list
gog contacts list --max 100

# Search contacts
gog contacts search "John"
gog contacts search "john@example.com"

# Get a specific contact
gog contacts get people/<resourceName>
gog contacts get user@example.com  # Get by email

# Create a contact
gog contacts create \
  --given-name "John" \
  --family-name "Doe" \
  --email "john@example.com" \
  --phone "+1234567890"

# Update a contact
gog contacts update people/<resourceName> \
  --given-name "Jane" \
  --email "jane@example.com"

# Delete a contact
gog contacts delete people/<resourceName>

# Other contacts (people you've emailed)
gog contacts other list
gog contacts other search "Jane"

# Workspace directory (requires Google Workspace)
gog contacts directory list
gog contacts directory search "Engineering"
```

## Key Flags

### `gog contacts search` / `gog contacts list`

| Flag | Description |
|------|-------------|
| `--max <n>` | Max results (default: 50) |

### `gog contacts create`

| Flag | Description |
|------|-------------|
| `--given-name <name>` | First name |
| `--family-name <name>` | Last name |
| `--email <email>` | Email address |
| `--phone <phone>` | Phone number |

### `gog contacts update`

| Flag | Description |
|------|-------------|
| `--given-name <name>` | First name |
| `--family-name <name>` | Last name |
| `--email <email>` | Email address |
| `--phone <phone>` | Phone number |
