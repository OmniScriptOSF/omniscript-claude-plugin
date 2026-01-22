---
description: Format an OmniScript file for consistency
argument-hint: "<file.osf> [--write]"
disable-model-invocation: true
allowed-tools: Bash, Read, Write
---

# /osf:format - Format OSF File

Format an OSF file for consistent style and readability. Applies standard indentation, spacing, and block organization.

## Arguments

- `$ARGUMENTS` - Path to the OSF file to format (required)
- `--write` - Write changes back to file (optional, shows diff by default)

## Steps

1. **Validate the file exists**:
   - Check that `$ARGUMENTS` is provided
   - Parse file path and flags

2. **Run the formatter**:
   ```bash
   cd /root/code/OmniScriptOSF/omniscript-core && bun run cli/src/osf.ts format "$FILE"
   ```

3. **Show the changes**:
   - Display a diff of original vs formatted
   - Highlight what was changed

4. **Apply changes** if `--write` flag is present:
   - Write formatted content back to file
   - Confirm the update

## Formatting Rules

The formatter applies these rules:

1. **Indentation**: 2 spaces for nested content
2. **Block spacing**: Blank line between blocks
3. **Property alignment**: Consistent property formatting
4. **Semicolons**: Ensure all properties end with `;`
5. **Braces**: Opening `{` on same line as block type
6. **Content**: Trim trailing whitespace

## Example Usage

```
# Preview formatting changes
/osf:format document.osf

# Apply formatting changes
/osf:format document.osf --write
```

## Before/After Example

Before:
```osf
@meta{
title:"My Doc";author:"Jane";}
@doc{
  # Heading
Content here.
}
```

After:
```osf
@meta {
  title: "My Doc";
  author: "Jane";
}

@doc {
  # Heading

  Content here.
}
```

## CLI Location

Formatter CLI: `/root/code/OmniScriptOSF/omniscript-core/cli/src/osf.ts`
