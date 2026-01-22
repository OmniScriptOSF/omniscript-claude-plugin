---
description: Create a new OmniScript document from template
argument-hint: "[type: document|presentation|spreadsheet|report]"
disable-model-invocation: true
allowed-tools: Read, Write, Bash, AskUserQuestion
---

# /osf:new - Create New OmniScript Document

Create a new OSF document using a template. Templates provide a starting structure for different document types.

## Available Templates

| Type | Description | Block Types Used |
|------|-------------|------------------|
| `document` | Basic text document | @meta, @doc |
| `presentation` | Slide deck | @meta, @slide |
| `spreadsheet` | Data workbook | @meta, @sheet |
| `report` | Combined document | @meta, @doc, @chart, @table |

## Arguments

- `$ARGUMENTS` - Template type (optional, defaults to "document")

## Steps

1. **Determine template type** from `$ARGUMENTS`:
   - If empty or not provided, default to "document"
   - Validate type is one of: document, presentation, spreadsheet, report

2. **Ask user for document details**:
   - Document title
   - Author name (optional)
   - Any specific customization needs

3. **Read the template** from:
   ```
   ${CLAUDE_PLUGIN_ROOT}/templates/{type}.osf
   ```

4. **Customize the template**:
   - Replace placeholder title with user's title
   - Replace placeholder author with user's name
   - Set date to today's date

5. **Write the new file**:
   - Use filename based on title (kebab-case)
   - Write to current working directory
   - Example: "My Report" → `my-report.osf`

6. **Confirm creation** and show the user the file path

## Example Usage

```
/osf:new document
/osf:new presentation
/osf:new spreadsheet
/osf:new report
```

## Template Location

Templates are located at: `${CLAUDE_PLUGIN_ROOT}/templates/`
