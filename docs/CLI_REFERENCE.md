# OktoEngine CLI Reference

Complete reference for all OktoEngine CLI commands and options.

---

## Table of Contents

1. [Command Overview](#command-overview)
2. [Core Commands](#core-commands)
3. [Utility Commands](#utility-commands)
4. [Global Flags](#global-flags)
5. [Examples](#examples)

---

## Command Overview

```bash
okto [FLAGS] <COMMAND>
```

### Available Commands

| Command | Description | Usage |
|---------|-------------|-------|
| `init` | Initialize new project | `okto init <name>` |
| `validate` | Validate OktoScript file | `okto validate [--file <path>]` |
| `train` | Train a model | `okto train [--file <path>]` |
| `eval` | Evaluate a model | `okto eval [--file <path>]` |
| `export` | Export a model | `okto export [--format <fmt>] [--file <path>]` |
| `list` | List resources | `okto list <projects|models|datasets>` |
| `doctor` | System diagnostics | `okto doctor [--install]` |
| `about` | Show information | `okto about` |
| `upgrade` | Upgrade engine | `okto upgrade` |

---

## Core Commands

### `okto init`

Initialize a new OktoScript project with proper folder structure.

**Usage:**
```bash
okto init <project-name>
```

**Example:**
```bash
okto init my-ai-model
```

**Creates:**
```
my-ai-model/
├── scripts/
│   └── train.okt
├── dataset/
│   ├── train.jsonl
│   └── val.jsonl
└── export/
```

**Output:**
```
🚀 Initializing OktoScript project: my-ai-model
✅ Project 'my-ai-model' initialized successfully!

Next steps:
  cd my-ai-model
  okto validate
  okto train
```

---

### `okto validate`

Validate an OktoScript file for syntax errors and configuration issues.

**Usage:**
```bash
okto validate [--file <path>]
okto validate -f scripts/train.okt
```

**Default:** Validates `scripts/train.okt` in current directory

**Options:**
- `-f, --file <PATH>` - Path to OktoScript file

**Example:**
```bash
okto validate
okto validate --file scripts/train.okt
okto validate --debug  # Enable debug mode
```

**Output:**
```
🐙 OktoEngine v0.1
🔍 Validating OktoScript file: "scripts/train.okt"
📄 File: "scripts/train.okt"
📄 Size: 382 bytes
📄 Lines: 31

✔ File parsed successfully

📋 Validation Results:
✅ Validation passed! No errors or warnings.

📊 Summary:
  Project: my-model
  ENV: Configured
  Dataset: dataset/train.jsonl
  Model: gpt2
  Training: 5 epochs, batch size 32
  Export: ["okm"]
```

**Exit Codes:**
- `0` - Validation passed
- `1` - Validation failed

---

### `okto train`

Train a model from an OktoScript configuration file.

**Usage:**
```bash
okto train [--file <path>]
okto train -f scripts/train.okt
```

**Default:** Uses `scripts/train.okt` in current directory

**Options:**
- `-f, --file <PATH>` - Path to OktoScript file
- `--debug` - Enable debug mode

**Example:**
```bash
okto train
okto train --file scripts/train.okt
okto train --debug  # Show detailed logs
```

**Output:**
```
🐙 OktoEngine v0.1
📄 Reading: "scripts/train.okt"

📊 Environment Check:
  ✔ Runtime: Python 3.14.0
  ✔ GPU: NVIDIA GeForce RTX 4070
  ✔ RAM: 63GB (40GB available)
  ✔ Platform: windows

📦 Checking dependencies...
  ✔ All dependencies available

🚀 Starting training pipeline...

Epoch 1/5: 100%|████████████| 500/500 [02:15<00:00, 3.70it/s]
  Loss: 2.345 → 1.892
  Learning Rate: 5e-5
  GPU Memory: 8.2GB / 12GB

✅ Training completed successfully!
📁 Output: runs/my-model/
```

**What it does:**
1. Parses and validates OktoScript file
2. Checks system environment
3. Verifies dependencies
4. Loads dataset
5. Initializes model
6. Executes training loop
7. Saves checkpoints
8. Exports model (if configured)

---

### `okto eval`

Evaluate a trained model against test datasets.

**Usage:**
```bash
okto eval [--file <path>]
okto eval -f scripts/train.okt
```

**Options:**
- `-f, --file <PATH>` - Path to OktoScript file

**Example:**
```bash
okto eval
okto eval --file scripts/train.okt
```

**Output:**
```
🐙 OktoEngine v0.1
📊 Evaluating model...

📈 Evaluation Results:
  Accuracy: 0.892
  Loss: 1.234
  Perplexity: 2.456
  F1-Score: 0.876

✅ Evaluation completed!
```

---

### `okto export`

Export a trained model to various formats.

**Usage:**
```bash
okto export [--format <fmt>] [--file <path>]
okto export --format okm
okto export --format onnx --file scripts/train.okt
```

**Options:**
- `-f, --format <FORMAT>` - Export format (okm, onnx, gguf, safetensors)
- `--file <PATH>` - Path to OktoScript file

**Supported Formats:**
- `okm` - OktoSeek Model format (optimized)
- `onnx` - ONNX format (universal)
- `gguf` - GGUF format (local inference)
- `safetensors` - SafeTensors format (HuggingFace)

**Example:**
```bash
okto export --format okm
okto export --format onnx
okto export --format okm,onnx  # Multiple formats
```

**Output:**
```
🐙 OktoEngine v0.1
📦 Exporting model...

✅ Exported to: export/model.okm
✅ Exported to: export/model.onnx

📁 Export directory: export/
```

---

### `okto list`

List available projects, models, or datasets.

**Usage:**
```bash
okto list <projects|models|datasets>
```

**Examples:**
```bash
okto list projects
okto list models
okto list datasets
```

**Output:**
```
📋 Available Projects:
  • my-chatbot
  • vision-model
  • recommender-system

📋 Available Models:
  • runs/my-chatbot/checkpoint-500
  • runs/vision-model/checkpoint-1000

📋 Available Datasets:
  • dataset/train.jsonl
  • dataset/val.jsonl
  • dataset/test.jsonl
```

---

## Utility Commands

### `okto doctor`

System diagnostics and environment checking.

**Usage:**
```bash
okto doctor
okto doctor --install
```

**Options:**
- `--install` - Automatically install missing dependencies

**Example:**
```bash
okto doctor              # Check system
okto doctor --install    # Check and install dependencies
```

**Output:**
```
🐙 OktoEngine v0.1 - System Diagnostics

🖥️  Platform: Windows
💾 RAM: 63GB total, 40GB available
⚙️  CPU: 32 cores
🎮 GPU: Checking...
  ✔ GPU found: NVIDIA GeForce RTX 4070 Laptop GPU
🔧 CUDA: Checking...
  ✔ CUDA available: 576.02
🔧 Runtime: Checking...
  ✔ Runtime available: Python 3.14.0
📦 Dependencies: Checking...
  ✔ All required packages installed

✅ Diagnostics complete
```

**With `--install`:**
```
📦 Dependencies: Checking...
  ❌ Missing packages: torch, transformers

💡 To install missing packages, run:
   pip install torch transformers datasets safetensors

🔧 Auto-installing missing packages...
  ✔ Successfully installed all packages!
```

---

### `okto upgrade`

Upgrade OktoEngine to the latest version.

**Usage:**
```bash
okto upgrade
```

**Example:**
```bash
okto upgrade
```

**Output:**
```
🐙 OktoEngine Upgrader
Current version: 0.1.0
🔍 Checking for updates...

📦 Downloading OktoEngine v0.2.0...
████████████████████ 100% [00:15<00:00]

✅ Updated successfully to v0.2.0
```

**What it does:**
1. Checks GitHub Releases for latest version
2. Compares with current version
3. Downloads appropriate binary for your OS
4. Replaces current binary
5. Makes it executable (Linux/Mac)

**Requirements:**
- Internet connection
- Write permissions to OktoEngine directory

---

### `okto about`

Show information about OktoEngine and OktoScript.

**Usage:**
```bash
okto about
```

**Output:**
```
🐙 OktoScript & OktoEngine

📚 Language: OktoScript
📝 Description: Domain-specific programming language for building, training, evaluating and exporting AI models
👤 Author: OktoSeek AI
📦 Version: 1.1
🌐 Website: https://www.oktoseek.com
💻 GitHub: https://github.com/oktoseek/oktoscript

🔧 OktoEngine:
   Official execution engine for OktoScript
   Repository: https://github.com/oktoseek/oktoengine
   Version: 0.1.0

📖 Learn more:
   - Grammar: https://github.com/oktoseek/oktoscript/blob/main/docs/grammar.md
   - Getting Started: https://github.com/oktoseek/oktoscript/blob/main/docs/GETTING_STARTED.md
   - FAQ: https://github.com/oktoseek/oktoscript/blob/main/docs/FAQ.md
```

---

## Global Flags

### `--debug`

Enable debug mode for detailed logging.

**Usage:**
```bash
okto <command> --debug
OKTO_DEBUG=1 okto <command>
```

**Example:**
```bash
okto validate --debug
okto train --debug
OKTO_DEBUG=1 okto train
```

**What it shows:**
- Detailed parsing logs
- Execution flow
- Error diagnostics
- Performance metrics

**Use cases:**
- Troubleshooting parsing errors
- Understanding execution flow
- Performance analysis
- Configuration debugging

---

### `--help`

Show help information for a command.

**Usage:**
```bash
okto --help
okto <command> --help
```

**Example:**
```bash
okto --help
okto train --help
```

---

### `--version`

Show OktoEngine version.

**Usage:**
```bash
okto --version
```

**Output:**
```
okto 0.1.0
```

---

## Examples

### Complete Workflow

```bash
# 1. Initialize project
okto init my-chatbot
cd my-chatbot

# 2. Validate configuration
okto validate

# 3. Check system
okto doctor

# 4. Train model
okto train

# 5. Evaluate model
okto eval

# 6. Export model
okto export --format okm
```

### Debug Workflow

```bash
# Validate with debug
okto validate --debug

# Train with debug
okto train --debug

# Or use environment variable
OKTO_DEBUG=1 okto train
```

### Update and Check

```bash
# Update engine
okto upgrade

# Check system
okto doctor

# Show information
okto about
```

---

## Exit Codes

| Code | Meaning |
|------|---------|
| `0` | Success |
| `1` | Error (general) |
| `2` | Validation error |
| `3` | Training error |
| `4` | System error |

---

## Environment Variables

| Variable | Description |
|----------|-------------|
| `OKTO_DEBUG` | Enable debug mode (any value) |
| `OKTO_LOG_LEVEL` | Set log level (debug, info, warn, error) |

---

## Tips & Best Practices

1. **Always validate before training:**
   ```bash
   okto validate && okto train
   ```

2. **Use debug mode for troubleshooting:**
   ```bash
   okto train --debug
   ```

3. **Check system before training:**
   ```bash
   okto doctor
   ```

4. **Keep engine updated:**
   ```bash
   okto upgrade
   ```

5. **Use absolute paths for clarity:**
   ```bash
   okto train --file /path/to/scripts/train.okt
   ```

---

**Need more help?** Check the [FAQ](./FAQ.md) or [Getting Started Guide](./GETTING_STARTED.md).

