# gog people

Google People API operations: access profile information.

## Commands

| Command | Description |
|---------|-------------|
| `gog people me` | Show your profile (people/me) |

## Examples

```bash
# Show your profile
gog people me

# Get JSON output
gog people me --json
```

## Output

The `gog people me` command displays:
- Name (display name)
- Email address
- Photo URL

```bash
$ gog people me
name    John Doe
email   john@example.com
photo   https://lh3.googleusercontent.com/...
```
