---
name: osf-best-practices
description: OmniScript document patterns and best practices. Use when users are creating or improving OSF documents, asking about document organization, or wanting to learn optimal OSF usage.
---

# OmniScript Best Practices

Guidelines for creating well-structured, maintainable OSF documents.

## Document Organization

### 1. Always Start with @meta

Every document should begin with a `@meta` block:

```osf
@meta {
  title: "Project Documentation";
  author: "Development Team";
  date: "2026-01-22";
  version: "1.0";
}
```

**Minimum recommended properties:**
- `title` - Always include
- `author` - For attribution
- `date` - When last updated

---

### 2. One Purpose Per Document

Keep documents focused on a single purpose:

**Good:** Separate files for different concerns
```
reports/
├── quarterly-sales.osf      # Sales report
├── quarterly-finance.osf    # Financial report
└── quarterly-combined.osf   # Combined via @include
```

**Avoid:** Monolithic documents with unrelated sections

---

### 3. Use @include for Modular Documents

Break large documents into smaller, reusable pieces:

```osf
// main-report.osf
@meta {
  title: "Annual Report 2026";
}

@include { path: "./sections/executive-summary.osf"; }
@include { path: "./sections/financial-overview.osf"; }
@include { path: "./sections/market-analysis.osf"; }
@include { path: "./sections/outlook.osf"; }
```

**Benefits:**
- Easier to edit individual sections
- Reuse sections across documents
- Better version control diffs

---

### 4. Consistent File Naming

Use descriptive, kebab-case filenames:

```
reports/
├── 2026-q1-sales-report.osf
├── 2026-q2-sales-report.osf
├── product-roadmap.osf
└── team-onboarding.osf
```

---

## Content Best Practices

### 1. Use Semantic Block Types

Choose the right block type for your content:

| Content Type | Block | Why |
|--------------|-------|-----|
| Narrative text | `@doc` | Markdown support |
| Presentation content | `@slide` | Layout options |
| Tabular data | `@sheet` or `@table` | Data structure |
| Visualizations | `@chart` | Automatic rendering |
| Flowcharts, diagrams | `@diagram` | Diagram engines |
| Code samples | `@code` | Syntax highlighting |

---

### 2. Optimize for Export Format

Consider your primary export format when structuring:

**For PDF/DOCX (documents):**
```osf
@meta { ... }
@doc {
  # Introduction
  ...
}
@doc {
  # Main Content
  ...
}
@table { ... }
@chart { ... }
```

**For PPTX (presentations):**
```osf
@meta { ... }
@slide { layout: "title"; ... }
@slide { layout: "content"; ... }
@slide { layout: "two-column"; ... }
```

**For XLSX (spreadsheets):**
```osf
@meta { ... }
@sheet { name: "Data"; ... }
@sheet { name: "Summary"; ... }
@chart { ... }  // Can be embedded in Excel
```

---

### 3. Use Multi-line Strings for Content

For readability, use triple-quoted strings for longer content:

```osf
@doc {
  content: '''
    # Section Title

    This is a longer piece of content that spans
    multiple lines and includes **formatting**.

    - Point one
    - Point two
    - Point three
  ''';
}
```

---

### 4. Add Meaningful Comments

Document complex sections:

```osf
// Financial data for Q1 2026
// Source: SAP export from 2026-01-15
@sheet {
  name: "Q1 Financials";
  columns: ["Category", "Actual", "Budget", "Variance"];
  rows: [
    ["Revenue", 1500000, 1400000, 100000],
    // Note: Expenses exclude one-time costs
    ["Expenses", 1100000, 1200000, -100000]
  ];
}
```

---

## Data Best Practices

### 1. Consistent Data Types in Columns

Keep column data types consistent:

**Good:**
```osf
@sheet {
  columns: ["Name", "Age", "Salary"];
  rows: [
    ["Alice", 30, 75000],
    ["Bob", 25, 65000],
    ["Carol", 35, 85000]
  ];
}
```

**Avoid:**
```osf
@sheet {
  columns: ["Name", "Age", "Salary"];
  rows: [
    ["Alice", 30, 75000],
    ["Bob", "twenty-five", "$65K"],  // Inconsistent types
    ["Carol", 35, 85000]
  ];
}
```

---

### 2. Use Formulas for Calculations

Let Excel handle calculations:

```osf
@sheet {
  columns: ["Item", "Qty", "Price", "Total"];
  rows: [
    ["Widget", 10, 5.00, "=B2*C2"],
    ["Gadget", 5, 12.00, "=B3*C3"],
    ["Total", "", "", "=SUM(D2:D3)"]
  ];
}
```

---

### 3. Meaningful Chart Labels

Always include descriptive labels:

```osf
@chart {
  type: "bar";
  title: "Monthly Revenue by Product Line";  // Clear title
  data: {
    labels: ["Product A", "Product B", "Product C"];  // Descriptive labels
    datasets: [
      {
        label: "Q1 2026";  // Dataset label
        values: [50000, 35000, 28000];
      }
    ];
  };
  options: {
    yAxisLabel: "Revenue (USD)";  // Axis label
  };
}
```

---

## Presentation Best Practices

### 1. Follow Slide Layout Conventions

**Title slide:** Use `layout: "title"`
```osf
@slide {
  layout: "title";
  title: "Q1 2026 Review";
  subtitle: "Sales & Marketing Performance";
}
```

**Content slides:** Keep bullets concise
```osf
@slide {
  layout: "content";
  title: "Key Takeaways";
  content: '''
    - Revenue up 15% YoY
    - Customer satisfaction at 94%
    - Three new product launches
  ''';
}
```

---

### 2. Use Speaker Notes

Add context for presenters:

```osf
@slide {
  layout: "content";
  title: "Financial Results";
  content: "...";
  notes: '''
    Key talking points:
    - Emphasize the revenue growth despite market challenges
    - Mention the cost reduction initiative
    - Be prepared for questions about Q2 outlook
  ''';
}
```

---

### 3. Limit Content Per Slide

Follow the 6x6 rule: Maximum 6 bullets, 6 words each.

**Good:**
```osf
@slide {
  content: '''
    - Revenue increased 15%
    - Costs reduced 8%
    - Market share grew 3%
  ''';
}
```

**Too much:**
```osf
@slide {
  content: '''
    - Our revenue increased by approximately 15% compared to the same quarter
    - Operating costs were reduced through efficiency initiatives by 8%
    - Market share in the North American region grew by 3 percentage points
    - Customer satisfaction scores improved from 91% to 94%
    - We launched three new products in the enterprise segment
    - The sales team exceeded their targets by 12%
    - Partner revenue contribution increased to 25%
  ''';
}
```

---

## Performance Tips

### 1. Optimize Images

Use appropriate image sizes:
- Presentation images: 1920x1080 max
- Document images: 1200px width max
- Use compressed formats (JPEG for photos, PNG for graphics)

---

### 2. Limit Chart Data Points

Keep charts readable:
- Bar/Line charts: 10-15 data points max
- Pie charts: 5-7 slices max
- Use aggregation for large datasets

---

### 3. Split Large Documents

If a document has more than 50 blocks, consider splitting:

```osf
// Instead of one huge document
// Split into logical sections

// report-q1-2026.osf
@include { path: "./sections/executive-summary.osf"; }
@include { path: "./sections/sales-analysis.osf"; }
@include { path: "./sections/financial-data.osf"; }
```

---

## Version Control Tips

### 1. Format Before Committing

Run the formatter for consistent diffs:
```bash
/osf:format document.osf --write
```

### 2. Meaningful Commit Messages

```
docs: update Q1 sales figures in quarterly-report.osf
feat: add new diagram showing architecture in design.osf
fix: correct formula in budget spreadsheet
```

### 3. Review with Diff

Before committing, review changes:
```bash
/osf:diff old-version.osf new-version.osf
```

---

## Common Patterns

### Report Template

```osf
@meta {
  title: "Monthly Report - [Month] [Year]";
  author: "Team Name";
  date: "YYYY-MM-DD";
}

@doc {
  # Executive Summary

  Brief overview of key points.
}

@doc {
  # Detailed Analysis

  In-depth content.
}

@chart {
  // Key metrics visualization
}

@table {
  // Summary data
}

@doc {
  # Recommendations

  Next steps and action items.
}
```

### Presentation Template

```osf
@meta {
  title: "Presentation Title";
  author: "Presenter Name";
}

@slide { layout: "title"; title: "Main Title"; subtitle: "Subtitle"; }
@slide { layout: "content"; title: "Agenda"; content: "..."; }
@slide { layout: "content"; title: "Key Point 1"; content: "..."; }
@slide { layout: "two-column"; title: "Comparison"; left: "..."; right: "..."; }
@slide { layout: "content"; title: "Summary"; content: "..."; }
@slide { layout: "title"; title: "Questions?"; subtitle: "Contact info"; }
```

### Data Document Template

```osf
@meta {
  title: "Data Export - [Description]";
  date: "YYYY-MM-DD";
}

@sheet {
  name: "Raw Data";
  columns: [...];
  rows: [...];
}

@sheet {
  name: "Summary";
  columns: [...];
  rows: [...];  // With formulas
}

@chart {
  // Visualization of key metrics
}
```
