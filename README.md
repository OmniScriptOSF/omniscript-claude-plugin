# OmniScript Plugin for Claude Code

<div align="center">

# 🤖 Claude Code Plugin for OSF

**Create, validate, lint, format & export universal documents directly from Claude Code**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)](./CHANGELOG.md)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Plugin-blueviolet.svg)](https://code.claude.com/docs/en/plugins)
[![OmniScript](https://img.shields.io/badge/OmniScript-v1.2-green.svg)](https://omniscriptosf.github.io)

[🚀 Quick Start](#-quick-start) • [📦 Installation](#-installation) •
[⚡ Commands](#-commands) • [🧠 Skills](#-skills) •
[🤖 Agents](#-agents) • [📖 Documentation](https://omniscriptosf.github.io)

</div>

---

## Overview

OmniScript (OSF) is a universal document DSL that lets you write plain-text `.osf` files and export them to **PDF**, **DOCX**, **PPTX**, **XLSX**, and **HTML**. This plugin brings full OSF capabilities directly into Claude Code conversations.

## ✨ Features

- **9 Commands** — Slash commands for all document operations
- **3 Skills** — Agent-accessible knowledge about OSF syntax and best practices
- **2 Agents** — Specialized agents for document generation and conversion
- **4 Templates** — Ready-to-use document templates
- **8 Examples** — Reference examples for all block types

---

## 🚀 Quick Start

```bash
# 1. Add the marketplace (one-time)
claude plugin marketplace add OmniScriptOSF/omniscript-claude-plugin

# 2. Install the plugin
claude plugin install osf@omniscript-marketplace

# 3. Start using!
/osf:new document
/osf:lint my-document.osf
/osf:export-pdf my-document.osf
```

---

## 📦 Installation

### Option 1: Marketplace Installation (Recommended)

```bash
# Add the OmniScript marketplace
claude plugin marketplace add OmniScriptOSF/omniscript-claude-plugin

# Install the OSF plugin
claude plugin install osf@omniscript-marketplace
```

### Option 2: Local Installation

```bash
# Clone the plugin
git clone https://github.com/OmniScriptOSF/omniscript-claude-plugin.git

# Use with plugin-dir flag
claude --plugin-dir /path/to/omniscript-claude-plugin
```

### Option 3: Project-Level Installation

```bash
# In your project root
git clone https://github.com/OmniScriptOSF/omniscript-claude-plugin.git .claude-plugins/osf
```

---

## ⚡ Commands

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

# Compare two versions
/osf:diff report-v1.osf report-v2.osf
```

---

## 🧠 Skills

The plugin provides three skills that Claude accesses automatically:

### osf-syntax

Complete OSF syntax reference including all block types, properties, and examples. Triggered when you ask about:
- OSF syntax or structure
- Block types (`@meta`, `@doc`, `@slide`, `@sheet`, `@chart`, `@diagram`, `@table`, `@code`)
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

---

## 🤖 Agents

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

---

## 📄 Templates

Ready-to-use templates in the `templates/` directory:

| Template | Purpose | Primary Blocks |
|----------|---------|----------------|
| `document.osf` | Basic document | `@meta`, `@doc` |
| `presentation.osf` | Slide deck | `@meta`, `@slide` |
| `spreadsheet.osf` | Data workbook | `@meta`, `@sheet`, `@chart` |
| `report.osf` | Combined report | `@meta`, `@doc`, `@chart`, `@table` |

---

## 📚 Examples

Example files demonstrating each block type in the `examples/` directory:

| File | Block Type | Description |
|------|------------|-------------|
| `meta-block.osf` | `@meta` | Document metadata |
| `doc-block.osf` | `@doc` | Rich text content with Markdown |
| `slide-block.osf` | `@slide` | Presentation slides with layouts |
| `sheet-block.osf` | `@sheet` | Spreadsheet data |
| `chart-block.osf` | `@chart` | Bar, line, pie charts |
| `diagram-block.osf` | `@diagram` | Mermaid/Graphviz diagrams |
| `table-block.osf` | `@table` | Styled markdown tables |
| `code-block.osf` | `@code` | Syntax-highlighted code |

---

## 📁 Directory Structure

```
omniscript-claude-plugin/
├── .claude-plugin/
│   ├── plugin.json           # Plugin manifest
│   └── marketplace.json      # Marketplace definition
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
└── examples/                  # Block examples
    ├── meta-block.osf
    ├── doc-block.osf
    ├── slide-block.osf
    ├── sheet-block.osf
    ├── chart-block.osf
    ├── diagram-block.osf
    ├── table-block.osf
    └── code-block.osf
```

---

## 🔧 Dependencies

This plugin uses the OmniScript CLI tools. For full functionality, ensure these are available:

```bash
# Core parser and CLI
/root/code/OmniScriptOSF/omniscript-core/

# Export converters
/root/code/OmniScriptOSF/omniscript-converters/
```

### Export Dependencies

For full export functionality:

```bash
cd /root/code/OmniScriptOSF/omniscript-core
bun add puppeteer     # PDF export

cd /root/code/OmniScriptOSF/omniscript-converters
bun add docx          # DOCX export
bun add pptxgenjs     # PPTX export
bun add exceljs       # XLSX export
```

---

## 💬 Getting Help

Ask Claude about OSF at any time:
- "How do I create a chart in OSF?"
- "What properties does @slide support?"
- "Why is my OSF file not parsing?"
- "What's the best way to structure a report?"

The plugin skills will automatically provide relevant information.

---

## 🤝 Contributing

Contributions welcome! The plugin follows Claude Code plugin conventions:

- Commands go in `commands/{name}/SKILL.md`
- Skills go in `skills/{name}/SKILL.md`
- Agents go in `agents/{name}.md`

See the [Claude Code Plugin Documentation](https://code.claude.com/docs/en/plugins) for details.

---

## 📜 License

MIT License - see the [OmniScriptOSF project](https://github.com/OmniScriptOSF) for details.

---

## 🔗 Links

- [OmniScript Documentation](https://omniscriptosf.github.io)
- [OmniScript Core Repository](https://github.com/OmniScriptOSF/omniscript-core)
- [OmniScript Converters](https://github.com/OmniScriptOSF/omniscript-converters)
- [OmniScript Examples](https://github.com/OmniScriptOSF/omniscript-examples)
- [Claude Code Plugin Documentation](https://code.claude.com/docs/en/plugins)
