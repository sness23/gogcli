# gog groups

Google Groups operations (Google Workspace only).

## Prerequisites

Groups commands require the Cloud Identity API and the `cloud-identity.groups.readonly` scope:

```bash
# Add groups scope to your account
gog auth add your@email.com --services groups --force-consent
```

## Commands

| Command | Description |
|---------|-------------|
| `gog groups list` | List groups you belong to |
| `gog groups members <groupEmail>` | List members of a group |

## Examples

```bash
# List groups you belong to
gog groups list
gog groups list --max 50

# List members of a group
gog groups members engineering@company.com
gog groups members all-staff@company.com --max 200
```

## Key Flags

### `gog groups list`

| Flag | Description |
|------|-------------|
| `--max <n>` | Max results (default: 100) |
| `--page <token>` | Page token |

### `gog groups members`

| Flag | Description |
|------|-------------|
| `--max <n>` | Max results (default: 100) |
| `--page <token>` | Page token |

## Output

### `gog groups list`

```
GROUP                          NAME                    RELATION
engineering@company.com        Engineering Team        direct
all-staff@company.com         All Staff               indirect
```

### `gog groups members`

```
EMAIL                          ROLE     TYPE
alice@company.com              OWNER    USER
bob@company.com                MEMBER   USER
nested-group@company.com       MEMBER   GROUP
```

## Notes

- Groups commands require Google Workspace
- The Cloud Identity API must be enabled in your Google Cloud project
- If you get permissions errors, re-authenticate with the groups scope:
  ```bash
  gog auth add your@email.com --services groups --force-consent
  ```
