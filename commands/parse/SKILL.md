---
description: Parse an OmniScript file and display its AST
argument-hint: "<file.osf>"
disable-model-invocation: true
allowed-tools: Bash, Read
---

# /osf:parse - Parse and Display AST

Parse an OSF file and display its Abstract Syntax Tree (AST) in a readable format. Useful for understanding document structure and debugging.

## Arguments

- `$ARGUMENTS` - Path to the OSF file to parse (required)

## Steps

1. **Validate the file exists**:
   - Check that `$ARGUMENTS` is provided
   - Verify the file exists and has `.osf` extension

2. **Run the parser**:
   ```bash
   cd /root/code/OmniScriptOSF/omniscript-core && bun run cli/src/osf.ts parse "$ARGUMENTS" --format json
   ```

3. **Display the AST**:
   - Show the parsed structure in a readable format
   - Highlight block types, properties, and content
   - Report any parsing warnings

4. **Explain the structure** if requested:
   - Describe each block type found
   - Note any unusual or complex structures

## Example Usage

```
/osf:parse document.osf
/osf:parse ./reports/quarterly.osf
```

## Output Format

The parser outputs JSON with this structure:

```json
{
  "blocks": [
    {
      "type": "meta",
      "properties": { "title": "...", "author": "..." }
    },
    {
      "type": "doc",
      "content": "..."
    }
  ],
  "includes": []
}
```

## CLI Location

Parser CLI: `/root/code/OmniScriptOSF/omniscript-core/cli/src/osf.ts`
