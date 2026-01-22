---
description: Export OmniScript document to PowerPoint (PPTX)
argument-hint: "<file.osf> [--theme default|corporate|minimal] [--output filename.pptx]"
disable-model-invocation: true
allowed-tools: Bash, Read
---

# /osf:export-pptx - Export to PowerPoint

Export an OSF document to Microsoft PowerPoint (PPTX) format. Ideal for presentations with `@slide` blocks.

## Arguments

- `$ARGUMENTS` - File path and options:
  - `<file.osf>` - Path to OSF file (required)
  - `--theme <theme>` - Visual theme (optional, default: "default")
  - `--output <file.pptx>` - Output filename (optional, defaults to input name)

## Available Themes

| Theme | Description |
|-------|-------------|
| `default` | Clean presentation with standard colors |
| `corporate` | Professional business styling |
| `minimal` | Simple white background, minimal design |

## Steps

1. **Parse arguments**:
   - Extract file path, theme, and output options
   - Validate the OSF file exists

2. **Run the export command**:
   ```bash
   cd /root/code/OmniScriptOSF/omniscript-core && bun run cli/src/osf.ts render "$FILE" --format pptx --theme "$THEME" --output "$OUTPUT"
   ```

3. **Report results**:
   - Confirm successful export
   - Show slide count
   - Show output file path and size

## Example Usage

```
/osf:export-pptx presentation.osf
/osf:export-pptx slides.osf --theme corporate
/osf:export-pptx deck.osf --output quarterly-review.pptx
```

## Slide Layouts

OSF `@slide` blocks support these layouts:

| Layout | Description |
|--------|-------------|
| `title` | Title slide with optional subtitle |
| `content` | Title with bullet points |
| `two-column` | Side-by-side content |
| `image` | Full-slide image with caption |
| `blank` | Empty slide for custom content |

## Block Type Mapping

| Block | PPTX Rendering |
|-------|----------------|
| `@meta` | Title slide properties |
| `@slide` | Individual slides |
| `@doc` | Text content on slides |
| `@chart` | Embedded charts |
| `@diagram` | Embedded diagrams |
| `@table` | Slide tables |
| `@code` | Code blocks with highlighting |
| `@sheet` | Data tables |

## Tips

- For best results, use `@slide` blocks for presentation content
- `@meta` properties set deck title and author
- Non-slide blocks are rendered as additional content slides
- Charts and diagrams are rendered as images

## CLI Location

Export CLI: `/root/code/OmniScriptOSF/omniscript-core/cli/src/osf.ts`
Converter: `/root/code/OmniScriptOSF/omniscript-converters/`
