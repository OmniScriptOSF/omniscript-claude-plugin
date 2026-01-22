---
description: Export OmniScript document to Word (DOCX)
argument-hint: "<file.osf> [--theme default|corporate|minimal] [--output filename.docx]"
disable-model-invocation: true
allowed-tools: Bash, Read
---

# /osf:export-docx - Export to Word Document

Export an OSF document to Microsoft Word (DOCX) format. Creates editable documents with proper styling.

## Arguments

- `$ARGUMENTS` - File path and options:
  - `<file.osf>` - Path to OSF file (required)
  - `--theme <theme>` - Visual theme (optional, default: "default")
  - `--output <file.docx>` - Output filename (optional, defaults to input name)

## Available Themes

| Theme | Description |
|-------|-------------|
| `default` | Standard Word document styling |
| `corporate` | Business document with formal headers |
| `minimal` | Clean, simple formatting |

## Steps

1. **Parse arguments**:
   - Extract file path, theme, and output options
   - Validate the OSF file exists

2. **Run the export command**:
   ```bash
   cd /root/code/OmniScriptOSF/omniscript-core && bun run cli/src/osf.ts render "$FILE" --format docx --theme "$THEME" --output "$OUTPUT"
   ```

3. **Report results**:
   - Confirm successful export
   - Show output file path and size
   - Note any blocks that couldn't be rendered

## Example Usage

```
/osf:export-docx document.osf
/osf:export-docx report.osf --theme corporate
/osf:export-docx manual.osf --output user-manual.docx
```

## Supported Block Types

| Block | DOCX Support |
|-------|--------------|
| `@meta` | Document properties |
| `@doc` | Full Markdown → Word conversion |
| `@slide` | Section breaks with slide content |
| `@sheet` | Word tables |
| `@chart` | Embedded chart images |
| `@diagram` | Embedded diagram images |
| `@table` | Styled Word tables |
| `@code` | Code blocks with highlighting |

## Word-Specific Features

- Heading styles (H1-H6) map to Word styles
- Lists convert to Word list formatting
- Tables include borders and styling
- Images are embedded at appropriate resolution
- Page breaks between major sections

## CLI Location

Export CLI: `/root/code/OmniScriptOSF/omniscript-core/cli/src/osf.ts`
Converter: `/root/code/OmniScriptOSF/omniscript-converters/`
