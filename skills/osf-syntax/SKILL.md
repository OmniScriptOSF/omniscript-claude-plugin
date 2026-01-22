---
name: osf-syntax
description: OmniScript format syntax reference. Use when users ask about OSF, .osf files, block types, document structure, or how to write OmniScript documents.
---

# OmniScript (OSF) Syntax Reference

OmniScript (OSF) is a universal document DSL for creating PDFs, DOCX, PPTX, XLSX, and HTML from plain text files.

## Document Structure

An OSF document consists of blocks. Each block starts with `@` followed by the block type:

```osf
@meta {
  title: "My Document";
  author: "Jane Smith";
  date: "2026-01-22";
}

@doc {
  # Introduction

  This is the document content using **Markdown**.
}
```

## Block Types

### @meta - Document Metadata (Required)

Every OSF document should start with a `@meta` block:

```osf
@meta {
  title: "Document Title";
  author: "Author Name";
  date: "2026-01-22";
  version: "1.0";
}
```

**Properties:**
- `title` (required): Document title
- `author`: Author name
- `date`: Publication date (YYYY-MM-DD)
- `version`: Document version

### @doc - Document Content

Rich text content using Markdown:

```osf
@doc {
  # Heading 1

  Regular paragraph with **bold** and *italic* text.

  ## Heading 2

  - Bullet list item 1
  - Bullet list item 2

  1. Numbered item
  2. Another item

  > Blockquote text

  [Link text](https://example.com)
}
```

### @slide - Presentation Slides

Create presentation slides:

```osf
@slide {
  layout: "title";
  title: "Presentation Title";
  subtitle: "Subtitle here";
}

@slide {
  layout: "content";
  title: "Key Points";
  bullets {
    "First point";
    "Second point";
    "Third point";
  }
}
```

**Layout options:** `title`, `content`, `two-column`, `image`, `blank`, `section`

### @sheet - Spreadsheet Data

Create data tables:

```osf
@sheet {
  name: "Sales Data";
  cols: ["Month", "Revenue", "Expenses"];
}
```

### @chart - Data Visualizations

Create charts using data arrays:

```osf
@chart {
  type: "bar";
  title: "Monthly Revenue";
  data: [
    { label: "Q1"; values: [100, 120, 110]; },
    { label: "Q2"; values: [130, 140, 125]; }
  ];
  options: {
    legend: true;
    yAxis: "Revenue ($K)";
  };
}
```

**Chart types:** `bar`, `line`, `pie`, `scatter`, `area`

### @diagram - Diagrams

Create diagrams using Mermaid or Graphviz:

```osf
@diagram {
  type: "flowchart";
  engine: "mermaid";
  title: "Process Flow";
  code: "graph TD
    A[Start] --> B{Decision}
    B -->|Yes| C[Action 1]
    B -->|No| D[Action 2]";
}

@diagram {
  type: "sequence";
  engine: "graphviz";
  code: "digraph G {
    A -> B -> C;
  }";
}
```

**Diagram types:** `flowchart`, `sequence`, `gantt`, `mindmap`
**Engines:** `mermaid`, `graphviz`

### @table - Styled Tables (Markdown syntax)

Create formatted tables using markdown pipe syntax:

```osf
@table {
  caption: "Team Members";
  style: "striped";
  alignment: ["left", "center", "right"];

  | Name | Role | Salary |
  | --- | --- | --- |
  | Alice | Engineer | $95,000 |
  | Bob | Designer | $85,000 |
  | Carol | Manager | $105,000 |
}
```

**Style options:** `bordered`, `striped`, `minimal`

### @code - Code Blocks

Syntax-highlighted code:

```osf
@code {
  language: "typescript";
  caption: "Example function";
  lineNumbers: true;
  highlight: [3, 4, 5];
  code: "function greet(name: string): string {
  return `Hello, ${name}!`;
}";
}
```

### @include - File Includes

Include other OSF files:

```osf
@include {
  path: "./chapters/chapter1.osf";
}
```

## Syntax Rules

1. **Block declaration**: `@blocktype { ... }`
2. **Properties**: `name: value;` (semicolon required)
3. **Strings**: Use double quotes `"value"` or multiline strings
4. **Arrays**: `[item1, item2, item3]`
5. **Objects**: `{ key: value; key2: value2; }`
6. **Comments**: `// single line` or `/* multi-line */`

## Quick Reference

| Block | Purpose | Export Formats |
|-------|---------|----------------|
| @meta | Document metadata | All |
| @doc | Rich text content | PDF, DOCX, HTML |
| @slide | Presentation slides | PDF, PPTX |
| @sheet | Spreadsheet data | XLSX, HTML |
| @chart | Data visualizations | All |
| @diagram | Diagrams | PDF, DOCX, PPTX, HTML |
| @table | Styled tables | All |
| @code | Code with highlighting | PDF, DOCX, HTML |
| @include | File includes | All (resolved at parse) |

For detailed block documentation, see [blocks-reference.md](blocks-reference.md).
