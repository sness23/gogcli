# gog calendar

Google Calendar operations: events, invitations, free/busy, and team calendars.

## Commands

| Command | Description |
|---------|-------------|
| `gog calendar calendars` | List calendars |
| `gog calendar acl <calendarId>` | List calendar ACL rules |
| `gog calendar events <calendarId>` | List events from a calendar |
| `gog calendar events --all` | List events from all calendars |
| `gog calendar event <calendarId> <eventId>` | Get a specific event |
| `gog calendar search <query>` | Search events by text |
| `gog calendar create <calendarId>` | Create an event |
| `gog calendar update <calendarId> <eventId>` | Update an event |
| `gog calendar delete <calendarId> <eventId>` | Delete an event |
| `gog calendar respond <calendarId> <eventId>` | Respond to an invitation |
| `gog calendar freebusy` | Get free/busy information |
| `gog calendar conflicts` | Find scheduling conflicts |
| `gog calendar colors` | Show calendar/event colors |
| `gog calendar time` | Show server time with timezone |
| `gog calendar users` | List Workspace users (for calendar IDs) |
| `gog calendar team <groupEmail>` | Show events for all group members |
| `gog calendar focus-time` | Create a Focus Time block |
| `gog calendar out-of-office` | Create an Out of Office event |
| `gog calendar working-location` | Set working location (home/office/custom) |

## Examples

```bash
# List calendars
gog calendar calendars

# List events with time filters
gog calendar events primary --today
gog calendar events primary --tomorrow
gog calendar events primary --week
gog calendar events primary --days 3
gog calendar events primary --from today --to friday
gog calendar events primary --from 2025-01-01T00:00:00Z --to 2025-01-08T00:00:00Z

# List events from all calendars
gog calendar events --all --today

# Search events
gog calendar search "meeting" --today
gog calendar search "standup" --days 30

# Create event
gog calendar create primary \
  --summary "Team Sync" \
  --from 2025-01-15T14:00:00Z \
  --to 2025-01-15T15:00:00Z \
  --attendees "alice@example.com,bob@example.com" \
  --location "Zoom"

# Update event
gog calendar update primary <eventId> \
  --summary "Updated Meeting" \
  --from 2025-01-15T11:00:00Z \
  --to 2025-01-15T12:00:00Z

# Add attendees without replacing existing ones
gog calendar update primary <eventId> \
  --add-attendee "alice@example.com,bob@example.com"

# Respond to invitation
gog calendar respond primary <eventId> --status accepted
gog calendar respond primary <eventId> --status declined
gog calendar respond primary <eventId> --status tentative

# Check availability
gog calendar freebusy --calendars "primary,work@example.com" \
  --from 2025-01-15T00:00:00Z \
  --to 2025-01-16T00:00:00Z

# Find conflicts
gog calendar conflicts --calendars "primary" --today

# Team calendar (requires Cloud Identity API)
gog calendar team engineering@company.com --today
gog calendar team engineering@company.com --week
gog calendar team engineering@company.com --freebusy
```

## Key Flags

### Time Range Flags (used by events, search, freebusy, conflicts)

| Flag | Description |
|------|-------------|
| `--from <time>` | Start time (RFC3339, date, or relative: today, tomorrow, monday) |
| `--to <time>` | End time |
| `--today` | Today only (timezone-aware) |
| `--tomorrow` | Tomorrow only |
| `--week` | This week (uses --week-start) |
| `--days <n>` | Next N days |
| `--week-start <day>` | Week start day for --week (sun, mon, etc.) |

### `gog calendar create`

| Flag | Description |
|------|-------------|
| `--summary <text>` | Event title |
| `--from <time>` | Start time (RFC3339) |
| `--to <time>` | End time (RFC3339) |
| `--attendees <emails>` | Comma-separated attendee emails |
| `--location <text>` | Event location |
| `--description <text>` | Event description |

### `gog calendar events`

| Flag | Description |
|------|-------------|
| `--max <n>` | Max results (default: 10) |
| `--page <token>` | Page token |
| `--query <text>` | Free text search |
| `--all` | Fetch from all calendars |
