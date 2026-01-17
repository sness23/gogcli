# gog tasks

Google Tasks operations: manage task lists and tasks.

## Commands

| Command | Description |
|---------|-------------|
| `gog tasks lists` | List task lists |
| `gog tasks lists create <title>` | Create a task list |
| `gog tasks list <tasklistId>` | List tasks in a task list |
| `gog tasks add <tasklistId> --title <title>` | Add a task |
| `gog tasks update <tasklistId> <taskId>` | Update a task |
| `gog tasks done <tasklistId> <taskId>` | Mark task as completed |
| `gog tasks undo <tasklistId> <taskId>` | Mark task as needs action |
| `gog tasks delete <tasklistId> <taskId>` | Delete a task |
| `gog tasks clear <tasklistId>` | Clear completed tasks |

## Examples

```bash
# List task lists
gog tasks lists
gog tasks lists --max 50

# Create a task list
gog tasks lists create "Work Tasks"

# List tasks in a list
gog tasks list <tasklistId>
gog tasks list <tasklistId> --max 50

# Add a task
gog tasks add <tasklistId> --title "Review documents"
gog tasks add <tasklistId> --title "Call client" --notes "Discuss project timeline"

# Update a task
gog tasks update <tasklistId> <taskId> --title "Updated title"
gog tasks update <tasklistId> <taskId> --notes "Added notes"

# Mark task as done/undone
gog tasks done <tasklistId> <taskId>
gog tasks undo <tasklistId> <taskId>

# Delete a task
gog tasks delete <tasklistId> <taskId>

# Clear all completed tasks from a list
gog tasks clear <tasklistId>
```

## Key Flags

### `gog tasks lists` / `gog tasks list`

| Flag | Description |
|------|-------------|
| `--max <n>` | Max results (default: 50) |

### `gog tasks add`

| Flag | Description |
|------|-------------|
| `--title <title>` | Task title (required) |
| `--notes <notes>` | Task notes |
| `--due <date>` | Due date |

### `gog tasks update`

| Flag | Description |
|------|-------------|
| `--title <title>` | New task title |
| `--notes <notes>` | New task notes |
| `--due <date>` | New due date |

## Command Aliases

| Command | Aliases |
|---------|---------|
| `gog tasks add` | `gog tasks create` |
| `gog tasks done` | `gog tasks complete` |
| `gog tasks undo` | `gog tasks uncomplete`, `gog tasks undone` |
| `gog tasks delete` | `gog tasks rm`, `gog tasks del` |
