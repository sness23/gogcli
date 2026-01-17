# gog sheets

Google Sheets operations: read, write, append, format, and export spreadsheets.

## Commands

| Command | Description |
|---------|-------------|
| `gog sheets get <spreadsheetId> <range>` | Get values from a range |
| `gog sheets update <spreadsheetId> <range> <values>` | Update values in a range |
| `gog sheets append <spreadsheetId> <range> <values>` | Append values to a range |
| `gog sheets clear <spreadsheetId> <range>` | Clear values in a range |
| `gog sheets format <spreadsheetId> <range>` | Apply cell formatting to a range |
| `gog sheets metadata <spreadsheetId>` | Get spreadsheet metadata |
| `gog sheets create <title>` | Create a new spreadsheet |
| `gog sheets copy <spreadsheetId> <title>` | Copy a Google Sheet |
| `gog sheets export <spreadsheetId>` | Export a Google Sheet (pdf\|xlsx\|csv) via Drive |

## Examples

```bash
# Read values
gog sheets get <spreadsheetId> 'Sheet1!A1:B10'
gog sheets metadata <spreadsheetId>

# Update values (pipe-separated cells, comma-separated rows)
gog sheets update <spreadsheetId> 'A1' 'val1|val2,val3|val4'
gog sheets update <spreadsheetId> 'A1' --values-json '[["a","b"],["c","d"]]'

# Append values
gog sheets append <spreadsheetId> 'Sheet1!A:C' 'new|row|data'

# Copy validation from another row
gog sheets update <spreadsheetId> 'Sheet1!A1:C1' 'val1|val2|val3' --copy-validation-from 'Sheet1!A2:C2'
gog sheets append <spreadsheetId> 'Sheet1!A:C' 'val1|val2|val3' --copy-validation-from 'Sheet1!A2:C2'

# Clear values
gog sheets clear <spreadsheetId> 'Sheet1!A1:B10'

# Apply formatting
gog sheets format <spreadsheetId> 'Sheet1!A1:B2' \
  --format-json '{"textFormat":{"bold":true}}' \
  --format-fields 'userEnteredFormat.textFormat.bold'

# Create spreadsheet
gog sheets create "My Spreadsheet"
gog sheets create "My Spreadsheet" --sheets "Sheet1,Sheet2,Data"

# Copy spreadsheet
gog sheets copy <spreadsheetId> "My Copy"

# Export
gog sheets export <spreadsheetId> --format xlsx --out ./sheet.xlsx
gog sheets export <spreadsheetId> --format pdf --out ./sheet.pdf
gog sheets export <spreadsheetId> --format csv --out ./sheet.csv
```

## Key Flags

### `gog sheets get`

| Flag | Description |
|------|-------------|
| `--dimension <dim>` | Major dimension: ROWS or COLUMNS |
| `--render <option>` | Value render: FORMATTED_VALUE, UNFORMATTED_VALUE, or FORMULA |

### `gog sheets update` / `gog sheets append`

| Flag | Description |
|------|-------------|
| `--input <option>` | Value input option: RAW or USER_ENTERED (default: USER_ENTERED) |
| `--values-json <json>` | Values as JSON 2D array |
| `--copy-validation-from <range>` | Copy data validation from an A1 range |

### `gog sheets append`

| Flag | Description |
|------|-------------|
| `--insert <option>` | Insert data option: OVERWRITE or INSERT_ROWS |

### `gog sheets create`

| Flag | Description |
|------|-------------|
| `--sheets <names>` | Comma-separated sheet names to create |

### `gog sheets export`

| Flag | Description |
|------|-------------|
| `--format <format>` | Export format: pdf\|xlsx\|csv (default: xlsx) |
| `--out <path>` | Output file path |

## Value Format

When providing values as arguments:
- Use `|` (pipe) to separate cells in a row
- Use `,` (comma) to separate rows

Example: `'a|b|c,d|e|f'` creates:
```
| a | b | c |
| d | e | f |
```

For complex data, use `--values-json`:
```bash
gog sheets update <id> 'A1' --values-json '[["a","b"],["c","d"]]'
```
