---
description: Compare two OmniScript files and show differences
argument-hint: "<file1.osf> <file2.osf>"
disable-model-invocation: true
allowed-tools: Bash, Read
---

# /osf:diff - Compare OSF Files

Compare two OSF files and display their differences at both the text and structural (AST) level.

## Arguments

- `$ARGUMENTS` - Two file paths separated by space (required)
  - First file: original/baseline
  - Second file: modified/comparison

## Steps

1. **Parse the arguments**:
   - Extract both file paths from `$ARGUMENTS`
   - Validate both files exist

2. **Run the diff command**:
   ```bash
   cd /root/code/OmniScriptOSF/omniscript-core && bun run cli/src/osf.ts diff "$FILE1" "$FILE2"
   ```

3. **Display the differences**:
   - Show text-level diff (line changes)
   - Show structural diff (block additions/removals/modifications)
   - Highlight significant changes

4. **Summarize changes**:
   - Number of blocks added/removed/modified
   - Property changes
   - Content changes

## Example Usage

```
/osf:diff original.osf modified.osf
/osf:diff v1/report.osf v2/report.osf
```

## Output Format

```
Comparing: original.osf → modified.osf

Text Diff:
-  title: "Old Title";
+  title: "New Title";

Structural Changes:
• @meta: title property changed
• @doc (block 2): content modified
• @slide: 1 block added

Summary: 3 changes (1 property, 1 content, 1 block added)
```

## Comparison Types

| Type | Description |
|------|-------------|
| Text diff | Line-by-line changes (like git diff) |
| AST diff | Structural changes at block level |
| Property diff | Changed property values |
| Content diff | Changed block content |

## CLI Location

Diff CLI: `/root/code/OmniScriptOSF/omniscript-core/cli/src/osf.ts`
