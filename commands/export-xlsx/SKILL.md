---
description: Export OmniScript document to Excel (XLSX)
argument-hint: "<file.osf> [--output filename.xlsx]"
disable-model-invocation: true
allowed-tools: Bash, Read
---

# /osf:export-xlsx - Export to Excel

Export an OSF document to Microsoft Excel (XLSX) format. Ideal for spreadsheets with `@sheet` blocks.

## Arguments

- `$ARGUMENTS` - File path and options:
  - `<file.osf>` - Path to OSF file (required)
  - `--output <file.xlsx>` - Output filename (optional, defaults to input name)

## Steps

1. **Parse arguments**:
   - Extract file path and output options
   - Validate the OSF file exists

2. **Run the export command**:
   ```bash
   cd /root/code/OmniScriptOSF/omniscript-core && bun run cli/src/osf.ts render "$FILE" --format xlsx --output "$OUTPUT"
   ```

3. **Report results**:
   - Confirm successful export
   - Show sheet count and row counts
   - Show output file path and size

## Example Usage

```
/osf:export-xlsx data.osf
/osf:export-xlsx budget.osf --output q4-budget.xlsx
```

## Sheet Structure

Each `@sheet` block becomes an Excel worksheet:

```osf
@sheet {
  name: "Sales Data";
  columns: ["Month", "Revenue", "Expenses", "Profit"];
  rows: [
    ["January", 10000, 7000, 3000],
    ["February", 12000, 8000, 4000],
    ["March", 11000, 7500, 3500]
  ];
}
```

## Block Type Mapping

| Block | XLSX Rendering |
|-------|----------------|
| `@meta` | Document properties (workbook metadata) |
| `@sheet` | Worksheet with data |
| `@table` | Additional data tables |
| `@chart` | Embedded Excel chart (when data available) |

## Excel Features

- Column headers are automatically bolded
- Number formatting is auto-detected
- Formulas are preserved if specified
- Column widths auto-fit content
- Multiple sheets supported

## Formula Support

OSF supports Excel formulas in cell values:

```osf
@sheet {
  name: "Calculations";
  columns: ["A", "B", "Sum"];
  rows: [
    [10, 20, "=A2+B2"],
    [15, 25, "=A3+B3"]
  ];
}
```

## CLI Location

Export CLI: `/root/code/OmniScriptOSF/omniscript-core/cli/src/osf.ts`
Converter: `/root/code/OmniScriptOSF/omniscript-converters/`
