# OktoEngine Debug Guide

Complete guide to using debug mode for troubleshooting and understanding OktoEngine's operation.

---

## Table of Contents

1. [What is Debug Mode?](#what-is-debug-mode)
2. [Enabling Debug Mode](#enabling-debug-mode)
3. [What Debug Mode Shows](#what-debug-mode-shows)
4. [Use Cases](#use-cases)
5. [Interpreting Debug Output](#interpreting-debug-output)
6. [Common Debug Scenarios](#common-debug-scenarios)

---

## What is Debug Mode?

Debug mode provides detailed, real-time logging of OktoEngine's internal operations. It shows:

- **Parsing details** - How your OktoScript is being parsed
- **Execution flow** - Step-by-step execution of commands
- **Error diagnostics** - Detailed error information
- **Performance metrics** - Timing and resource usage

**When to use:**
- Troubleshooting parsing errors
- Understanding execution flow
- Performance analysis
- Configuration debugging
- Learning how OktoEngine works

---

## Enabling Debug Mode

### Method 1: Command Flag

```bash
okto validate --debug
okto train --debug
okto export --debug
```

### Method 2: Environment Variable

```bash
# Linux/Mac
OKTO_DEBUG=1 okto train

# Windows PowerShell
$env:OKTO_DEBUG=1; okto train

# Windows CMD
set OKTO_DEBUG=1 && okto train
```

### Method 3: Global Flag

The `--debug` flag works with all commands:

```bash
okto <command> --debug
```

---

## What Debug Mode Shows

### Parsing Phase

**Example output:**
```
DEBUG: Starting parse_oktoscript. Input preview: '# okto_version: "1.0" PROJECT "MyModel" ENV {'
DEBUG: Parsed version: Some("1.0")
DEBUG: Parsed project: MyModel
DEBUG: After PROJECT, remaining input: 'ENV { accelerator: "gpu" min_memory: "8GB"...'
DEBUG: Attempting to parse ENV block...
DEBUG: Parsed ENV field: accelerator = gpu
DEBUG: Parsed ENV field: min_memory = 8GB
DEBUG: Parsed ENV field: precision = fp16
DEBUG: Successfully parsed ENV block with 5 fields
DEBUG: After ENV, remaining input: 'DATASET { train: "dataset/train.jsonl"...'
```

**What it shows:**
- How the parser processes your OktoScript
- Which blocks are being parsed
- Field-by-field parsing
- Remaining input after each step

### Execution Phase

**Example output:**
```
DEBUG: Parsed DATASET block
DEBUG: Parsed MODEL block
DEBUG: After MODEL, remaining input: 'TRAIN { epochs: 5 batch_size: 32...'
DEBUG: Attempting to parse TRAIN block...
DEBUG: Parsed TRAIN block
DEBUG: After TRAIN, remaining input: 'EXPORT { format: ["okm"]...'
DEBUG: Attempting to parse EXPORT block...
DEBUG: Parsing EXPORT field: format
DEBUG: parse_string_list - attempting to parse array. Input: '["okm"] path: "export/" }'
DEBUG: parse_string_list - parsed 1 items: ["okm"]
DEBUG: Parsed format: ["okm"]
DEBUG: Parsed EXPORT block
DEBUG: Final remaining input: ''
```

**What it shows:**
- Block parsing order
- Field extraction
- Array/list parsing
- Final state

### Error Diagnostics

**Example output:**
```
DEBUG: Failed to parse key in ENV block. Input: 'accelerator: "gpu"...'
DEBUG: Failed to parse ':' after key 'accelerator'. Input: '"gpu"...'
```

**What it shows:**
- Exact point of failure
- Input context at failure
- Parsing step that failed
- Remaining input

---

## Use Cases

### 1. Troubleshooting Parsing Errors

**Problem:** Validation fails with unclear error

**Solution:**
```bash
okto validate --debug
```

**Example:**
```
DEBUG: Failed to parse ':' after key 'accelerator:'. Input: '"gpu"'
```

**Interpretation:** The parser found `accelerator:` but couldn't find the colon separator. This suggests a syntax issue in the ENV block.

**Fix:** Check your OktoScript syntax:
```okt
ENV {
  accelerator: "gpu"  # ✅ Correct
  # accelerator: "gpu"  # ❌ Wrong (colon in key)
}
```

### 2. Understanding Execution Flow

**Use case:** Want to see how OktoEngine processes your configuration

**Solution:**
```bash
okto train --debug
```

**Shows:**
- Order of block parsing
- How fields are extracted
- How arrays are parsed
- Final parsed structure

### 3. Performance Analysis

**Use case:** Training is slow, want to see where time is spent

**Solution:**
```bash
okto train --debug
```

**Look for:**
- Time spent in parsing
- Time spent loading datasets
- Time spent initializing models
- Training loop performance

### 4. Configuration Debugging

**Use case:** Configuration works but results are unexpected

**Solution:**
```bash
okto validate --debug
okto train --debug
```

**Check:**
- Are all fields parsed correctly?
- Are values what you expect?
- Are arrays parsed correctly?
- Are boolean values correct?

---

## Interpreting Debug Output

### Parsing Flow

**Normal flow:**
```
DEBUG: Starting parse_oktoscript...
DEBUG: Parsed version: Some("1.0")
DEBUG: Parsed project: MyModel
DEBUG: After PROJECT, remaining input: 'ENV {...'
DEBUG: Attempting to parse ENV block...
DEBUG: Successfully parsed ENV block
DEBUG: After ENV, remaining input: 'DATASET {...'
...
DEBUG: Final remaining input: ''
```

**What to look for:**
- ✅ Each block parsed successfully
- ✅ Remaining input decreases after each block
- ✅ Final remaining input is empty

**Error indicators:**
- ❌ "Failed to parse" messages
- ❌ Remaining input contains unexpected content
- ❌ Blocks not parsed in expected order

### Field Parsing

**Normal:**
```
DEBUG: Parsed ENV field: accelerator = gpu
DEBUG: Parsed ENV field: precision = fp16
```

**Error:**
```
DEBUG: Failed to parse value for key 'accelerator'. Input: 'gpu min_memory...'
```

**Interpretation:** The parser couldn't extract the value for `accelerator`. This might indicate:
- Missing quotes around string values
- Syntax error in value
- Unexpected character

### Array Parsing

**Normal:**
```
DEBUG: parse_string_list - attempting to parse array. Input: '["okm"] path: "export/"'
DEBUG: parse_string_list - parsed 1 items: ["okm"]
```

**Error:**
```
DEBUG: parse_string_list - failed to parse array. Input: '[okm] path: "export/"'
```

**Interpretation:** Array parsing failed. Common causes:
- Missing quotes around array items
- Invalid array syntax
- Unexpected characters

---

## Common Debug Scenarios

### Scenario 1: Validation Fails

**Problem:**
```bash
$ okto validate
❌ Parsing failed!
```

**Debug:**
```bash
$ okto validate --debug
DEBUG: Starting parse_oktoscript...
DEBUG: Failed to parse PROJECT block. Input: 'ENV { accelerator: "gpu"...'
```

**Solution:** Missing PROJECT block or syntax error before PROJECT.

### Scenario 2: Training Fails

**Problem:**
```bash
$ okto train
❌ Training failed!
```

**Debug:**
```bash
$ okto train --debug
DEBUG: Parsed ENV field: accelerator = gpu
DEBUG: Parsed ENV field: precision = fp16
DEBUG: After ENV, remaining input: 'DATASET { train: "dataset/train.jsonl"...'
DEBUG: Parsed DATASET block
DEBUG: After DATASET, remaining input: 'MODEL { base: "gpt2" } TRAIN...'
DEBUG: Parsed MODEL block
DEBUG: After MODEL, remaining input: 'TRAIN { epochs: 5...'
...
Training error: Dataset file not found
```

**Solution:** Dataset file path is incorrect. Check the path in DATASET block.

### Scenario 3: Export Fails

**Problem:**
```bash
$ okto export
❌ Export failed!
```

**Debug:**
```bash
$ okto export --debug
DEBUG: Parsing EXPORT field: format
DEBUG: parse_string_list - attempting to parse array. Input: '["okm"] path: "export/"'
DEBUG: parse_string_list - parsed 1 items: ["okm"]
DEBUG: Parsed format: ["okm"]
DEBUG: Parsed EXPORT block
Export error: Model not found at runs/MyModel/
```

**Solution:** Model hasn't been trained yet. Run `okto train` first.

---

## Tips for Effective Debugging

1. **Start with validation:**
   ```bash
   okto validate --debug
   ```
   Fix parsing errors before training.

2. **Use debug for training:**
   ```bash
   okto train --debug
   ```
   See full execution flow.

3. **Look for patterns:**
   - Multiple "Failed to parse" messages indicate syntax issues
   - "Remaining input" shows what wasn't parsed
   - Field parsing shows exact values extracted

4. **Compare working vs. broken:**
   - Run debug on a working configuration
   - Compare output with broken configuration
   - Identify differences

5. **Check final state:**
   - Look for "Final remaining input: ''"
   - Empty means successful parsing
   - Non-empty means unparsed content

---

## Debug Output Examples

### Successful Parsing

```
DEBUG: Starting parse_oktoscript. Input preview: '# okto_version: "1.0" PROJECT "MyModel"'
DEBUG: Parsed version: Some("1.0")
DEBUG: Parsed project: MyModel
DEBUG: After PROJECT, remaining input: 'ENV { accelerator: "gpu"...'
DEBUG: Attempting to parse ENV block...
DEBUG: Parsed ENV field: accelerator = gpu
DEBUG: Parsed ENV field: precision = fp16
DEBUG: Successfully parsed ENV block with 2 fields
DEBUG: After ENV, remaining input: 'DATASET { train: "dataset/train.jsonl"...'
DEBUG: Parsed DATASET block
DEBUG: Parsed MODEL block
DEBUG: Parsed TRAIN block
DEBUG: Parsed EXPORT block
DEBUG: Final remaining input: ''
```

### Parsing Error

```
DEBUG: Starting parse_oktoscript...
DEBUG: Parsed version: Some("1.0")
DEBUG: Parsed project: MyModel
DEBUG: After PROJECT, remaining input: 'ENV { accelerator: "gpu"...'
DEBUG: Attempting to parse ENV block...
DEBUG: Failed to parse key in ENV block. Input: 'accelerator: "gpu"...'
```

**Issue:** Key parsing failed. Check ENV block syntax.

---

## Best Practices

1. **Use debug mode proactively:**
   - Enable debug when first setting up
   - Verify configuration is parsed correctly
   - Understand execution flow

2. **Disable when not needed:**
   - Debug output can be verbose
   - Disable for production runs
   - Use only when troubleshooting

3. **Save debug output:**
   ```bash
   okto train --debug > debug.log 2>&1
   ```
   Review later or share for support

4. **Combine with validation:**
   ```bash
   okto validate --debug && okto train --debug
   ```
   Fix parsing issues before training

---

**Need more help?** Check the [FAQ](./FAQ.md) or open an issue on [GitHub](https://github.com/oktoseek/oktoengine/issues).

