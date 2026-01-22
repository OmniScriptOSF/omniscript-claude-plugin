---
description: Export OmniScript document to PDF
argument-hint: "<file.osf> [--theme default|corporate|minimal] [--output filename.pdf]"
disable-model-invocation: true
allowed-tools: Bash, Read
---

# /osf:export-pdf - Export to PDF

Export an OSF document to PDF format. Supports multiple themes and customization options.

## Arguments

- `$ARGUMENTS` - File path and options:
  - `<file.osf>` - Path to OSF file (required)
  - `--theme <theme>` - Visual theme (optional, default: "default")
  - `--output <file.pdf>` - Output filename (optional, defaults to input name)

## Available Themes

| Theme | Description |
|-------|-------------|
| `default` | Clean, professional layout with standard fonts |
| `corporate` | Business-focused with formal styling |
| `minimal` | Simple, distraction-free design |

## Steps

1. **Parse arguments**:
   - Extract file path, theme, and output options
   - Validate the OSF file exists

2. **Run the export command**:
   ```bash
   cd /root/code/OmniScriptOSF/omniscript-core && bun run cli/src/osf.ts render "$FILE" --format pdf --theme "$THEME" --output "$OUTPUT"
   ```

3. **Report results**:
   - Confirm successful export
   - Show output file path and size
   - Note any blocks that couldn't be rendered

## Example Usage

```
/osf:export-pdf document.osf
/osf:export-pdf report.osf --theme corporate
/osf:export-pdf slides.osf --output presentation.pdf
/osf:export-pdf report.osf --theme minimal --output ~/output/report.pdf
```

## Supported Block Types

All block types render to PDF:
- `@meta` - Document properties (title, author, date in header)
- `@doc` - Document content with Markdown formatting
- `@slide` - Rendered as separate pages
- `@sheet` - Tables with data
- `@chart` - Rendered visualizations
- `@diagram` - Rendered diagrams (Mermaid/Graphviz)
- `@table` - Styled tables
- `@code` - Syntax-highlighted code blocks

## Requirements

PDF export requires Puppeteer. If not installed:
```bash
cd /root/code/OmniScriptOSF/omniscript-core && bun add puppeteer
```

## CLI Location

Export CLI: `/root/code/OmniScriptOSF/omniscript-core/cli/src/osf.ts`
