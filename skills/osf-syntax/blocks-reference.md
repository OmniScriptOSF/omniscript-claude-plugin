# OSF Block Reference

Comprehensive documentation for all OmniScript block types.

## @meta Block

The metadata block defines document properties. Should be the first block in any OSF file.

### Properties

| Property | Type | Required | Description |
|----------|------|----------|-------------|
| `title` | string | Yes | Document title |
| `author` | string | No | Author name |
| `date` | string | No | Date (YYYY-MM-DD format) |
| `version` | string | No | Document version |
| `language` | string | No | ISO 639-1 language code |
| `keywords` | array | No | Array of keyword strings |
| `description` | string | No | Brief description |
| `category` | string | No | Document category |
| `theme` | string | No | Default theme for exports |

### Example

```osf
@meta {
  title: "Quarterly Report";
  author: "Finance Team";
  date: "2026-01-22";
  version: "1.2";
  language: "en";
  keywords: ["finance", "quarterly", "2026"];
  description: "Q1 2026 financial performance summary";
  category: "reports";
  theme: "corporate";
}
```

---

## @doc Block

Document content block using Markdown syntax.

### Supported Markdown Features

- **Headings**: `# H1` through `###### H6`
- **Emphasis**: `*italic*`, `**bold**`, `***bold italic***`
- **Lists**: Ordered (`1.`) and unordered (`-`, `*`, `+`)
- **Links**: `[text](url)` and `[text](url "title")`
- **Images**: `![alt](src)` and `![alt](src "title")`
- **Blockquotes**: `> quote text`
- **Code**: Inline `` `code` `` and fenced blocks
- **Horizontal rules**: `---`, `***`, `___`
- **Tables**: GFM table syntax

### Example

```osf
@doc {
  # Executive Summary

  This report covers the **Q1 2026** performance metrics.

  ## Key Highlights

  - Revenue increased by 15%
  - Customer satisfaction at 94%
  - New product launch successful

  ## Financial Overview

  | Metric | Q1 2025 | Q1 2026 | Change |
  |--------|---------|---------|--------|
  | Revenue | $1.2M | $1.38M | +15% |
  | Expenses | $800K | $850K | +6% |
  | Profit | $400K | $530K | +33% |

  > "Outstanding quarter for the team." - CEO

  See the [detailed analysis](#analysis) below.
}
```

---

## @slide Block

Presentation slide content.

### Properties

| Property | Type | Required | Description |
|----------|------|----------|-------------|
| `layout` | string | No | Slide layout type |
| `title` | string | No | Slide title |
| `subtitle` | string | No | Slide subtitle |
| `content` | string | No | Main content (Markdown) |
| `left` | string | No | Left column (two-column) |
| `right` | string | No | Right column (two-column) |
| `image` | string | No | Image path or URL |
| `caption` | string | No | Image caption |
| `notes` | string | No | Speaker notes |
| `background` | string | No | Background color or image |

### Layout Types

| Layout | Description | Key Properties |
|--------|-------------|----------------|
| `title` | Title slide | title, subtitle |
| `content` | Title + bullets | title, content |
| `two-column` | Side-by-side | title, left, right |
| `image` | Full image | image, caption |
| `blank` | Empty slide | (any custom content) |
| `section` | Section divider | title |

### Examples

```osf
// Title slide
@slide {
  layout: "title";
  title: "Annual Review 2026";
  subtitle: "Company Performance & Outlook";
  background: "#1a365d";
}

// Content slide with bullets
@slide {
  layout: "content";
  title: "Key Achievements";
  content: '''
    - Launched 3 new products
    - Expanded to 5 new markets
    - Increased team by 50%
    - Achieved ISO certification
  ''';
  notes: "Emphasize the ISO certification as a major milestone";
}

// Two-column comparison
@slide {
  layout: "two-column";
  title: "Before & After";
  left: '''
    **2025**
    - Manual processes
    - Limited reach
    - Small team
  ''';
  right: '''
    **2026**
    - Automated workflows
    - Global presence
    - Scaled organization
  ''';
}

// Image slide
@slide {
  layout: "image";
  title: "Our New Headquarters";
  image: "./images/headquarters.jpg";
  caption: "Opening ceremony, March 2026";
}
```

---

## @sheet Block

Spreadsheet data for Excel export.

### Properties

| Property | Type | Required | Description |
|----------|------|----------|-------------|
| `name` | string | Yes | Worksheet name |
| `columns` | array | Yes | Column header strings |
| `rows` | array | Yes | 2D array of cell values |
| `formulas` | object | No | Named formula definitions |
| `styles` | object | No | Cell styling rules |

### Cell Values

Cells can contain:
- **Strings**: `"text"`
- **Numbers**: `123`, `45.67`
- **Booleans**: `true`, `false`
- **Formulas**: `"=A1+B1"`, `"=SUM(A1:A10)"`
- **Dates**: `"2026-01-22"` (ISO format)

### Example

```osf
@sheet {
  name: "Budget 2026";
  columns: ["Category", "Q1", "Q2", "Q3", "Q4", "Total"];
  rows: [
    ["Marketing", 50000, 55000, 60000, 65000, "=SUM(B2:E2)"],
    ["Engineering", 200000, 210000, 220000, 230000, "=SUM(B3:E3)"],
    ["Operations", 80000, 82000, 85000, 88000, "=SUM(B4:E4)"],
    ["Total", "=SUM(B2:B4)", "=SUM(C2:C4)", "=SUM(D2:D4)", "=SUM(E2:E4)", "=SUM(F2:F4)"]
  ];
}

@sheet {
  name: "Employee Data";
  columns: ["ID", "Name", "Department", "Start Date", "Salary"];
  rows: [
    [1001, "Alice Johnson", "Engineering", "2024-03-15", 95000],
    [1002, "Bob Smith", "Marketing", "2023-08-01", 75000],
    [1003, "Carol Williams", "Operations", "2025-01-10", 65000]
  ];
}
```

---

## @chart Block

Data visualization charts.

### Properties

| Property | Type | Required | Description |
|----------|------|----------|-------------|
| `type` | string | Yes | Chart type |
| `title` | string | No | Chart title |
| `data` | object | Yes | Chart data configuration |
| `options` | object | No | Chart options |

### Chart Types

| Type | Description | Best For |
|------|-------------|----------|
| `bar` | Vertical bars | Comparisons |
| `horizontalBar` | Horizontal bars | Long labels |
| `line` | Line chart | Trends over time |
| `area` | Filled line | Volume over time |
| `pie` | Pie chart | Part of whole |
| `doughnut` | Doughnut chart | Part of whole (hollow) |
| `scatter` | Scatter plot | Correlations |
| `radar` | Radar/spider | Multi-variable comparison |

### Data Structure

```osf
@chart {
  type: "bar";
  title: "Monthly Sales";
  data: {
    labels: ["Jan", "Feb", "Mar", "Apr", "May", "Jun"];
    datasets: [
      {
        label: "2025";
        values: [65, 59, 80, 81, 56, 55];
        color: "#3b82f6";
      },
      {
        label: "2026";
        values: [75, 69, 90, 91, 66, 70];
        color: "#10b981";
      }
    ];
  };
  options: {
    showLegend: true;
    showGrid: true;
    yAxisLabel: "Sales ($K)";
  };
}
```

### More Examples

```osf
// Pie chart
@chart {
  type: "pie";
  title: "Market Share";
  data: {
    labels: ["Product A", "Product B", "Product C", "Other"];
    datasets: [
      {
        values: [35, 30, 20, 15];
        colors: ["#3b82f6", "#10b981", "#f59e0b", "#6b7280"];
      }
    ];
  };
}

// Line chart with multiple series
@chart {
  type: "line";
  title: "Website Traffic";
  data: {
    labels: ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"];
    datasets: [
      {
        label: "Visitors";
        values: [1200, 1900, 1500, 2100, 2400, 1800, 1100];
      },
      {
        label: "Page Views";
        values: [3600, 5700, 4500, 6300, 7200, 5400, 3300];
      }
    ];
  };
}
```

---

## @diagram Block

Diagrams using Mermaid or Graphviz syntax.

### Properties

| Property | Type | Required | Description |
|----------|------|----------|-------------|
| `type` | string | Yes | Diagram engine: `mermaid` or `graphviz` |
| `content` | string | Yes | Diagram source code |
| `title` | string | No | Diagram caption |

### Mermaid Examples

```osf
// Flowchart
@diagram {
  type: "mermaid";
  title: "User Registration Flow";
  content: '''
    graph TD
      A[User visits site] --> B{Has account?}
      B -->|Yes| C[Login]
      B -->|No| D[Register]
      D --> E[Verify email]
      E --> F[Complete profile]
      C --> G[Dashboard]
      F --> G
  ''';
}

// Sequence diagram
@diagram {
  type: "mermaid";
  content: '''
    sequenceDiagram
      participant U as User
      participant A as API
      participant D as Database

      U->>A: POST /login
      A->>D: Query user
      D-->>A: User data
      A-->>U: JWT token
  ''';
}

// Class diagram
@diagram {
  type: "mermaid";
  content: '''
    classDiagram
      class User {
        +String name
        +String email
        +login()
        +logout()
      }
      class Order {
        +String id
        +Date created
        +submit()
      }
      User "1" --> "*" Order : places
  ''';
}
```

### Graphviz Examples

```osf
// Simple directed graph
@diagram {
  type: "graphviz";
  content: '''
    digraph G {
      rankdir=LR;
      node [shape=box];

      Input -> Process -> Output;
      Process -> Error [style=dashed];
      Error -> Process [label="retry"];
    }
  ''';
}

// Organization chart
@diagram {
  type: "graphviz";
  content: '''
    digraph OrgChart {
      node [shape=record];

      CEO [label="CEO|Jane Smith"];
      CTO [label="CTO|Bob Johnson"];
      CFO [label="CFO|Carol Williams"];
      Eng [label="Engineering"];
      Sales [label="Sales"];

      CEO -> CTO;
      CEO -> CFO;
      CTO -> Eng;
      CFO -> Sales;
    }
  ''';
}
```

---

## @table Block

Styled HTML/document tables.

### Properties

| Property | Type | Required | Description |
|----------|------|----------|-------------|
| `caption` | string | No | Table caption |
| `headers` | array | Yes | Column header strings |
| `rows` | array | Yes | 2D array of cell values |
| `style` | string | No | Table style preset |
| `alignment` | array | No | Column alignments |

### Style Options

| Style | Description |
|-------|-------------|
| `default` | Standard borders and spacing |
| `striped` | Alternating row colors |
| `bordered` | Full cell borders |
| `minimal` | No borders, minimal styling |
| `compact` | Reduced padding |

### Alignment Options

- `left` (default)
- `center`
- `right`

### Example

```osf
@table {
  caption: "Product Comparison";
  headers: ["Feature", "Basic", "Pro", "Enterprise"];
  rows: [
    ["Users", "5", "25", "Unlimited"],
    ["Storage", "10 GB", "100 GB", "1 TB"],
    ["Support", "Email", "Priority", "24/7 Phone"],
    ["Price", "$10/mo", "$50/mo", "Contact us"]
  ];
  style: "striped";
  alignment: ["left", "center", "center", "center"];
}
```

---

## @code Block

Syntax-highlighted code snippets.

### Properties

| Property | Type | Required | Description |
|----------|------|----------|-------------|
| `language` | string | Yes | Programming language |
| `content` | string | Yes | Code content |
| `showLineNumbers` | boolean | No | Show line numbers |
| `highlightLines` | array | No | Lines to highlight |
| `title` | string | No | Code block title/filename |

### Supported Languages

Common languages: `javascript`, `typescript`, `python`, `java`, `csharp`, `go`, `rust`, `ruby`, `php`, `swift`, `kotlin`, `sql`, `html`, `css`, `json`, `yaml`, `bash`, `markdown`

### Example

```osf
@code {
  language: "typescript";
  title: "api/users.ts";
  showLineNumbers: true;
  highlightLines: [5, 6, 7];
  content: '''
    import { Router } from 'express';

    const router = Router();

    router.get('/users', async (req, res) => {
      const users = await User.findAll();
      res.json(users);
    });

    export default router;
  ''';
}

@code {
  language: "python";
  content: '''
    def greet(name: str) -> str:
        """Return a greeting message."""
        return f"Hello, {name}!"
  ''';
}
```

---

## @include Block

Include content from other OSF files.

### Properties

| Property | Type | Required | Description |
|----------|------|----------|-------------|
| `path` | string | Yes | Relative or absolute path |

### Path Resolution

- Relative paths resolve from the current file's directory
- Absolute paths start with `/`
- Circular includes are detected and prevented

### Example

```osf
// Main document
@meta {
  title: "Complete Manual";
}

@include {
  path: "./chapters/introduction.osf";
}

@include {
  path: "./chapters/getting-started.osf";
}

@include {
  path: "./chapters/advanced-topics.osf";
}

@include {
  path: "./appendix/glossary.osf";
}
```

### Included File Example

```osf
// chapters/introduction.osf
@doc {
  # Introduction

  Welcome to the manual. This guide covers...
}
```

---

## Comments

OSF supports single-line and multi-line comments:

```osf
// This is a single-line comment

/*
  This is a
  multi-line comment
*/

@meta {
  title: "Document";  // Inline comment
}
```
