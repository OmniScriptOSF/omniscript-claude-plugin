---
description: Validate OmniScript syntax and report errors
argument-hint: "<file.osf>"
disable-model-invocation: true
allowed-tools: Bash, Read
---

# /osf:lint - Validate OSF Syntax

Validate an OSF file's syntax and report any errors or warnings. The linter checks for syntax errors, schema violations, and best practice issues.

## Arguments

- `$ARGUMENTS` - Path to the OSF file to validate (required)

## Steps

1. **Validate the file exists**:
   - Check that `$ARGUMENTS` is provided
   - Verify the file exists

2. **Run the linter**:
   ```bash
   cd /root/code/OmniScriptOSF/omniscript-core && bun run cli/src/osf.ts lint "$ARGUMENTS"
   ```

3. **Report results**:
   - If valid: Report success with block count
   - If errors: List each error with line number and description

4. **Provide fix suggestions** for any errors:
   - Explain what's wrong
   - Show the correct syntax
   - Offer to fix automatically if simple

## Common Validation Errors

| Error | Cause | Fix |
|-------|-------|-----|
| Missing semicolon | Property value not terminated | Add `;` after value |
| Unclosed block | Missing `}` | Add closing brace |
| Unknown block type | Typo in block name | Use valid type: meta, doc, slide, sheet, chart, diagram, table, code |
| Missing @meta | No metadata block | Add `@meta { ... }` at start |
| Invalid property | Unsupported property name | Check block schema |

## Example Usage

```
/osf:lint document.osf
/osf:lint ./reports/quarterly.osf
```

## Output Format

Success:
```
✓ document.osf is valid (3 blocks)
```

Error:
```
✗ document.osf has errors:
  Line 5: Missing semicolon after 'title' property
  Line 12: Unknown block type '@invalid'
```

## CLI Location

Linter CLI: `/root/code/OmniScriptOSF/omniscript-core/cli/src/osf.ts`
