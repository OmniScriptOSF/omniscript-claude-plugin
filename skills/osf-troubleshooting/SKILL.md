---
name: osf-troubleshooting
description: Troubleshoot OmniScript parsing errors, validation failures, and export problems. Use when users encounter OSF syntax errors, document validation issues, or export failures.
---

# OmniScript Troubleshooting Guide

Common errors and solutions for OmniScript documents.

## Parse Errors

### Missing Semicolon

**Error:** `Expected ';' after property value`

**Cause:** Property values must end with a semicolon.

**Wrong:**
```osf
@meta {
  title: "My Doc"
  author: "Jane"
}
```

**Correct:**
```osf
@meta {
  title: "My Doc";
  author: "Jane";
}
```

---

### Unclosed Block

**Error:** `Unexpected end of input, expected '}'`

**Cause:** Missing closing brace for a block.

**Wrong:**
```osf
@meta {
  title: "My Doc";

@doc {
  Content here.
}
```

**Correct:**
```osf
@meta {
  title: "My Doc";
}

@doc {
  Content here.
}
```

---

### Unclosed String

**Error:** `Unterminated string literal`

**Cause:** String not properly closed with matching quote.

**Wrong:**
```osf
@meta {
  title: "My Doc;
}
```

**Correct:**
```osf
@meta {
  title: "My Doc";
}
```

For multi-line strings, use triple quotes:
```osf
@doc {
  content: '''
    This is a
    multi-line string.
  ''';
}
```

---

### Invalid Block Type

**Error:** `Unknown block type '@invalid'`

**Cause:** Using a block type that doesn't exist.

**Valid block types:**
- `@meta` - Metadata
- `@doc` - Document content
- `@slide` - Presentation slides
- `@sheet` - Spreadsheet data
- `@chart` - Charts
- `@diagram` - Diagrams
- `@table` - Tables
- `@code` - Code blocks
- `@include` - File includes

---

### Invalid Property Name

**Error:** `Unknown property 'xyz' in block type 'meta'`

**Cause:** Using a property that's not valid for the block type.

**Solution:** Check the block reference for valid properties:
- `/osf:help` or ask "What properties does @meta support?"

---

## Validation Errors

### Missing @meta Block

**Error:** `Document must start with @meta block`

**Cause:** Every OSF document should have a `@meta` block.

**Solution:** Add a meta block at the beginning:
```osf
@meta {
  title: "My Document";
  author: "Author Name";
  date: "2026-01-22";
}
```

---

### Invalid Array Syntax

**Error:** `Expected array value`

**Cause:** Arrays must use square brackets with comma-separated values.

**Wrong:**
```osf
@sheet {
  columns: "A", "B", "C";
}
```

**Correct:**
```osf
@sheet {
  columns: ["A", "B", "C"];
}
```

---

### Invalid Object Syntax

**Error:** `Expected object with properties`

**Cause:** Objects must use curly braces with property: value pairs.

**Wrong:**
```osf
@chart {
  data: labels: ["A", "B"];
}
```

**Correct:**
```osf
@chart {
  data: {
    labels: ["A", "B"];
    datasets: [];
  };
}
```

---

### Type Mismatch

**Error:** `Property 'rows' expects array, got string`

**Cause:** Property value doesn't match expected type.

**Solution:** Check the property type in the block reference.

---

## Export Errors

### PDF Export Fails

**Error:** `Puppeteer not found` or `Browser launch failed`

**Cause:** PDF export requires Puppeteer to be installed.

**Solution:**
```bash
cd /root/code/OmniScriptOSF/omniscript-core
bun add puppeteer
```

If on a server without display:
```bash
# Install headless Chrome dependencies
apt-get install -y chromium-browser
```

---

### DOCX Export Fails

**Error:** `Cannot find module 'docx'`

**Solution:**
```bash
cd /root/code/OmniScriptOSF/omniscript-converters
bun add docx
```

---

### PPTX Export Fails

**Error:** `Cannot find module 'pptxgenjs'`

**Solution:**
```bash
cd /root/code/OmniScriptOSF/omniscript-converters
bun add pptxgenjs
```

---

### XLSX Export Fails

**Error:** `Cannot find module 'exceljs'`

**Solution:**
```bash
cd /root/code/OmniScriptOSF/omniscript-converters
bun add exceljs
```

---

### Unsupported Block in Export

**Error:** `Block type '@diagram' not supported for xlsx export`

**Cause:** Not all block types export to all formats.

**Block compatibility:**

| Block | PDF | DOCX | PPTX | XLSX | HTML |
|-------|-----|------|------|------|------|
| @meta | ✓ | ✓ | ✓ | ✓ | ✓ |
| @doc | ✓ | ✓ | ✓ | - | ✓ |
| @slide | ✓ | ✓ | ✓ | - | ✓ |
| @sheet | ✓ | ✓ | - | ✓ | ✓ |
| @chart | ✓ | ✓ | ✓ | ✓* | ✓ |
| @diagram | ✓ | ✓ | ✓ | - | ✓ |
| @table | ✓ | ✓ | ✓ | ✓ | ✓ |
| @code | ✓ | ✓ | - | - | ✓ |

*Charts in XLSX require associated data

---

## Include Errors

### File Not Found

**Error:** `Include file not found: ./chapters/intro.osf`

**Cause:** The included file doesn't exist at the specified path.

**Solutions:**
1. Check the file path is correct
2. Ensure the path is relative to the current file
3. Verify the file exists:
   ```bash
   ls -la ./chapters/
   ```

---

### Circular Include

**Error:** `Circular include detected: a.osf → b.osf → a.osf`

**Cause:** File A includes B, which includes A (directly or indirectly).

**Solution:** Restructure your includes to avoid cycles:
```
main.osf
├── include: chapter1.osf
├── include: chapter2.osf
└── include: chapter3.osf
```

---

## Debugging Tips

### 1. Parse First, Then Export

Always validate your OSF before exporting:
```bash
/osf:lint document.osf
```

### 2. Check AST Structure

View the parsed structure to understand issues:
```bash
/osf:parse document.osf
```

### 3. Start Simple

When debugging, reduce to minimal example:
```osf
@meta {
  title: "Test";
}

@doc {
  Hello world.
}
```

### 4. Check Quotes and Braces

Use editor matching to verify:
- All `{` have matching `}`
- All `"` have matching `"`
- All `'''` have matching `'''`

### 5. Validate Property Types

Common type mistakes:
- Arrays need `[]`: `columns: ["A", "B"];`
- Numbers don't need quotes: `value: 123;`
- Booleans: `true` or `false` (no quotes)

---

## Getting Help

If you can't resolve an issue:

1. Share the exact error message
2. Share the relevant OSF code
3. Mention what you're trying to accomplish
4. Ask: "Why won't my OSF file parse?" or "Help me fix this OSF error"
