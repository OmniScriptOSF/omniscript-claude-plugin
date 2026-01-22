# OmniScript Plugin for Claude Code

A comprehensive Claude Code plugin providing full OmniScript (OSF) support for creating, validating, formatting, and exporting universal documents.

## Overview

OmniScript (OSF) is a universal document DSL that lets you write plain-text `.osf` files and export them to **PDF**, **DOCX**, **PPTX**, **XLSX**, and **HTML**. This plugin brings OSF capabilities directly into Claude Code conversations.

## Features

- **Commands**: User-invoked slash commands for document operations
- **Skills**: Agent-accessible knowledge about OSF syntax and best practices
- **Agents**: Specialized agents for document generation and conversion
- **Templates**: Ready-to-use document templates
- **Examples**: Reference examples for all block types

## Installation

### Option 1: Local Installation

```bash
# Clone or copy the plugin to your plugins directory
cp -r omniscript-claude-plugin ~/.claude/plugins/

# Or use the plugin-dir flag
claude --plugin-dir /path/to/omniscript-claude-plugin
```

### Option 2: Project-Level Installation

Add the plugin directory to your project:

```bash
# In your project root
cp -r /path/to/omniscript-claude-plugin ./.claude-plugins/osf
```

## Commands

| Command | Description | Example |
|---------|-------------|---------|
| `/osf:new` | Create new document from template | `/osf:new presentation` |
| `/osf:parse` | Parse and display AST | `/osf:parse doc.osf` |
| `/osf:lint` | Validate syntax | `/osf:lint doc.osf` |
| `/osf:format` | Format for consistency | `/osf:format doc.osf --write` |
| `/osf:diff` | Compare two files | `/osf:diff v1.osf v2.osf` |
| `/osf:export-pdf` | Export to PDF | `/osf:export-pdf doc.osf` |
| `/osf:export-docx` | Export to Word | `/osf:export-docx doc.osf` |
| `/osf:export-pptx` | Export to PowerPoint | `/osf:export-pptx slides.osf` |
| `/osf:export-xlsx` | Export to Excel | `/osf:export-xlsx data.osf` |

### Command Examples

```bash
# Create a new presentation
/osf:new presentation

# Validate an OSF file
/osf:lint my-report.osf

# Export to PDF with corporate theme
/osf:export-pdf report.osf --theme corporate --output quarterly-report.pdf
```

## Skills

The plugin provides three skills that Claude can access automatically:

### osf-syntax

Complete OSF syntax reference including all block types, properties, and examples. Triggered when you ask about:
- OSF syntax or structure
- Block types (@meta, @doc, @slide, etc.)
- How to write OSF documents

### osf-troubleshooting

Common errors and solutions. Triggered when you encounter:
- Parse errors
- Validation failures
- Export problems

### osf-best-practices

Document patterns and guidelines. Triggered when:
- Creating new documents
- Organizing document structure
- Optimizing for specific export formats

## Agents

### osf-generator

Generate complete OSF documents from natural language descriptions.

```
"Create a presentation about machine learning basics"
"Make a quarterly sales report template"
"Generate a project proposal document"
```

### osf-converter

Convert existing documents to OSF format.

```
"Convert this markdown to OSF"
"Transform this CSV into an OSF spreadsheet"
"Turn this text into an OSF document"
```

## Templates

Ready-to-use templates in the `templates/` directory:

| Template | Purpose | Primary Blocks |
|----------|---------|----------------|
| `document.osf` | Basic document | @meta, @doc |
| `presentation.osf` | Slide deck | @meta, @slide |
| `spreadsheet.osf` | Data workbook | @meta, @sheet, @chart |
| `report.osf` | Combined report | @meta, @doc, @chart, @table |

## Examples

Example files demonstrating each block type:

- `examples/meta-block.osf` - Document metadata
- `examples/doc-block.osf` - Rich text content
- `examples/slide-block.osf` - Presentation slides
- `examples/sheet-block.osf` - Spreadsheet data
- `examples/chart-block.osf` - Data visualizations
- `examples/diagram-block.osf` - Mermaid/Graphviz diagrams
- `examples/table-block.osf` - Styled tables
- `examples/code-block.osf` - Syntax-highlighted code

## Directory Structure

```
omniscript-claude-plugin/
├── .claude-plugin/
│   └── plugin.json           # Plugin manifest
├── commands/                  # Slash commands
│   ├── new/SKILL.md
│   ├── parse/SKILL.md
│   ├── lint/SKILL.md
│   ├── format/SKILL.md
│   ├── diff/SKILL.md
│   ├── export-pdf/SKILL.md
│   ├── export-docx/SKILL.md
│   ├── export-pptx/SKILL.md
│   └── export-xlsx/SKILL.md
├── skills/                    # Agent skills
│   ├── osf-syntax/
│   │   ├── SKILL.md
│   │   └── blocks-reference.md
│   ├── osf-troubleshooting/SKILL.md
│   └── osf-best-practices/SKILL.md
├── agents/                    # Custom agents
│   ├── osf-generator.md
│   └── osf-converter.md
├── templates/                 # Document templates
│   ├── document.osf
│   ├── presentation.osf
│   ├── spreadsheet.osf
│   └── report.osf
├── examples/                  # Block examples
│   ├── meta-block.osf
│   ├── doc-block.osf
│   ├── slide-block.osf
│   ├── sheet-block.osf
│   ├── chart-block.osf
│   ├── diagram-block.osf
│   ├── table-block.osf
│   └── code-block.osf
└── README.md
```

## Dependencies

This plugin requires the OmniScript CLI to be installed and available:

```bash
# Required: omniscript-core with CLI
/root/code/OmniScriptOSF/omniscript-core/

# For export functionality: omniscript-converters
/root/code/OmniScriptOSF/omniscript-converters/
```

### Export Dependencies

For full export functionality, ensure these packages are installed:

```bash
cd /root/code/OmniScriptOSF/omniscript-core
bun add puppeteer     # PDF export

cd /root/code/OmniScriptOSF/omniscript-converters
bun add docx          # DOCX export
bun add pptxgenjs     # PPTX export
bun add exceljs       # XLSX export
```

## Quick Start

1. **Create a new document**:
   ```
   /osf:new document
   ```

2. **Edit the generated file** with your content

3. **Validate the syntax**:
   ```
   /osf:lint my-document.osf
   ```

4. **Export to your desired format**:
   ```
   /osf:export-pdf my-document.osf
   ```

## Getting Help

Ask Claude about OSF at any time:
- "How do I create a chart in OSF?"
- "What properties does @slide support?"
- "Why is my OSF file not parsing?"
- "What's the best way to structure a report?"

The plugin skills will automatically provide relevant information.

## Contributing

Contributions welcome! The plugin follows Claude Code plugin conventions:
- Commands go in `commands/{name}/SKILL.md`
- Skills go in `skills/{name}/SKILL.md`
- Agents go in `agents/{name}.md`

## License

MIT License - see the OmniScriptOSF project for details.

## Links

- [OmniScript Documentation](https://omniscriptosf.github.io)
- [OmniScript Core Repository](https://github.com/omniscriptosf/omniscript-core)
- [Claude Code Plugin Documentation](https://code.claude.com/docs/en/plugins)
