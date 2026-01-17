# gog classroom

Google Classroom operations: courses, rosters, coursework, and announcements.

## Commands

| Command | Description |
|---------|-------------|
| `gog classroom courses` | List courses |
| `gog classroom students <courseId>` | List course students |
| `gog classroom teachers <courseId>` | List course teachers |
| `gog classroom roster <courseId>` | List full roster (students + teachers) |
| `gog classroom coursework <courseId>` | List coursework |
| `gog classroom materials <courseId>` | List coursework materials |
| `gog classroom submissions <courseId> <courseworkId>` | List student submissions |
| `gog classroom announcements <courseId>` | List announcements |
| `gog classroom topics <courseId>` | List topics |
| `gog classroom invitations` | List/manage invitations |
| `gog classroom guardians` | List/manage guardians |
| `gog classroom guardian-invitations` | List/manage guardian invitations |
| `gog classroom profile <userId>` | Get user profile |

## Examples

```bash
# List courses
gog classroom courses
gog classroom courses --state ACTIVE

# Get course roster
gog classroom students <courseId>
gog classroom teachers <courseId>
gog classroom roster <courseId>

# View coursework and submissions
gog classroom coursework <courseId>
gog classroom submissions <courseId> <courseworkId>

# Announcements
gog classroom announcements <courseId>

# Topics
gog classroom topics <courseId>
```

## Key Flags

### `gog classroom courses`

| Flag | Description |
|------|-------------|
| `--state <state>` | Filter by course state (ACTIVE, ARCHIVED, etc.) |
| `--max <n>` | Max results |
| `--page <token>` | Page token |

### Common Flags

| Flag | Description |
|------|-------------|
| `--max <n>` | Max results |
| `--page <token>` | Page token for pagination |
