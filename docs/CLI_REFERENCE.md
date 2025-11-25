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
| `convert` | Convert model formats | `okto convert --input <path> --from <fmt> --to <fmt> --output <path>` |
| `infer` | Direct inference (single input/output) | `okto infer --model <path> --text "<input>"` |
| `chat` | Interactive chat mode | `okto chat --model <path>` |
| `compare` | Compare two models | `okto compare <model1> <model2>` |
| `logs` | View historical logs | `okto logs <model_or_run_id>` |
| `tune` | Auto-tune training | `okto tune [--file <path>]` |
| `list` | List resources | `okto list <projects|models|datasets|exports>` |
| `doctor` | System diagnostics | `okto doctor [--install]` |
| `about` | Show information | `okto about` |
| `upgrade` | Upgrade engine | `okto upgrade` |
| `exit` | Exit interactive mode | `okto exit` |

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

### `okto convert`

Convert a trained model between different formats.

**Usage:**
```bash
okto convert --input <model_path> --from <format> --to <format> --output <output_path>
```

**Options:**
- `--input <PATH>` - Path to input model file
- `--from <FORMAT>` - Source format (pt, bin, onnx, tflite, gguf, okm, safetensors)
- `--to <FORMAT>` - Target format (onnx, tflite, gguf, okm, safetensors)
- `--output <PATH>` - Path to output file

**Supported Formats:**

| Format | From | To | Usage |
|--------|------|-----|-------|
| `pt`, `bin` | ✅ | ❌ | PyTorch format |
| `onnx` | ✅ | ✅ | Web / Interoperability |
| `tflite` | ✅ | ✅ | Mobile (Android / iOS) |
| `gguf` | ✅ | ✅ | Local LLMs (llama.cpp) |
| `okm` | ✅ | ✅ | Okto Model Format |
| `safetensors` | ✅ | ✅ | Safe and fast |

**Examples:**

```bash
# PyTorch → GGUF (local inference)
okto convert --input model.pt --from pt --to gguf --output model.gguf

# PyTorch → TFLite (mobile)
okto convert --input model.pt --from pt --to tflite --output model.tflite

# PyTorch → ONNX (web)
okto convert --input model.pt --from pt --to onnx --output model.onnx

# ONNX → OktoModel (OktoSeek optimized)
okto convert --input model.onnx --from onnx --to okm --output model.okm
```

**Output:**
```
🐙 OktoEngine v0.1
🔄 Converting model...

📦 Input: model.pt (PyTorch format)
📦 Output: model.gguf (GGUF format)

⏳ Converting...
  ✓ Loading model: model.pt
  ✓ Quantizing to GGUF...
  ✓ Writing output: model.gguf

✅ Conversion completed!
📁 Output: model.gguf (245 MB)
```

---

### `okto infer`

Run direct inference on a trained model (single input/output).

**Usage:**
```bash
okto infer --model <model_path> --text "<input>"
```

**Options:**
- `--model <PATH>` - Path to trained model
- `--text <STRING>` - Input text for inference

**What it respects:**
- `BEHAVIOR` block settings (personality, verbosity, language)
- `GUARD` block rules (safety, content filtering)
- `INFERENCE` block parameters (temperature, max_length, etc.)
- `CONTROL` block logic (if defined)

**Example:**
```bash
okto infer --model models/pizzabot.okm --text "Good evening, I want a pizza"
```

**Output:**
```
🐙 OktoEngine v0.1
🤖 Loading model: models/pizzabot.okm

📋 Model Configuration:
  ✓ BEHAVIOR: friendly, medium verbosity, English
  ✓ GUARD: toxicity, bias, hallucination protection enabled
  ✓ INFERENCE: temperature=0.7, max_length=120

💭 Input: "Good evening, I want a pizza"

🤖 Processing...
  ✓ Guard check passed
  ✓ Inference parameters applied
  ✓ CONTROL rules evaluated

📤 Output: "Good evening! I'd be happy to help you order a pizza. What size and toppings would you like?"

✅ Inference completed in 0.23s
```

**Advanced Example with Multiple Inputs:**
```bash
# Single inference
okto infer --model models/chatbot.okm --text "What are your business hours?"

# Batch inference (via file)
echo "What are your business hours?" > input.txt
echo "Do you deliver?" >> input.txt
okto infer --model models/chatbot.okm --file input.txt
```

**Error Handling:**
```
⚠️  Guard violation detected: toxicity
🛡️  Content blocked by GUARD rules
📤 Output: "Sorry, this request is not allowed."
```

---

### `okto chat`

Start an interactive chat session with a trained model.

**Usage:**
```bash
okto chat --model <model_path>
```

**Options:**
- `--model <PATH>` - Path to trained model

**Features:**
- Uses `prompt_style` from BEHAVIOR block
- Respects BEHAVIOR settings (personality, verbosity, language)
- Enforces GUARD rules in real-time
- Can use MEMORY in the future (session context)
- Type `/exit` or `exit` to quit

**Example:**
```bash
okto chat --model models/pizzabot.okm
```

**Interactive Session:**
```
🐙 OktoEngine v0.1
🤖 Loading model: models/pizzabot.okm

📋 Model Configuration:
  ✓ BEHAVIOR: friendly, medium verbosity, English
  ✓ GUARD: enabled
  ✓ INFERENCE: chat mode
  ✓ Exit command: /exit

🟢 Okto Chat started (type '/exit' to quit)

─────────────────────────────────────────

You: hi
Bot: Hello! How can I help you today?

You: what flavors do you have?
Bot: We have a great selection of pizza flavors! Here are some popular options:

  • Margherita - Classic tomato, mozzarella, and basil
  • Pepperoni - Spicy pepperoni with mozzarella
  • Four Cheese - Mozzarella, gorgonzola, parmesan, and provolone
  • Hawaiian - Ham and pineapple
  • Vegetarian - Fresh vegetables and herbs

  What sounds good to you?

You: do you deliver?
Bot: Yes, we offer delivery! Our delivery service is available in your area. 

  Delivery time is typically 30-45 minutes, and we have a minimum order of $15 for delivery. 

  Would you like to place an order?

You: /exit
🔴 Session ended

📊 Session Summary:
  Messages: 6 (3 user, 3 bot)
  Duration: 2m 15s
  Guard checks: 3 (all passed)
```

**Advanced Features:**
```
You: tell me a joke
Bot: I'd love to share a joke! Here's a light one:

  Why did the pizza maker go to art school?
  Because they wanted to learn how to make a masterpiece!

  🍕 Hope that made you smile! Is there anything else I can help you with?

You: [tries to input toxic content]
🛡️  Guard: Content violation detected
Bot: I cannot assist with that request. How else can I help you?

You: /exit
🔴 Session ended
```

**Session Context (Future):**
```
You: my name is John
Bot: Nice to meet you, John! How can I help you today?

You: what's my name?
Bot: Your name is John! Is there anything else you'd like to know?
```

---

### `okto compare`

Compare two trained models using the same test inputs.

**Usage:**
```bash
okto compare <model1> <model2>
```

**Options:**
- `<model1>` - Path to first model
- `<model2>` - Path to second model

**What it compares:**
- Latency (inference speed)
- Accuracy (if test dataset provided)
- Loss values
- Response quality
- Resource usage

**Example:**
```bash
okto compare models/pizza_v1.okm models/pizza_v2.okm
```

**Output:**
```
🐙 OktoEngine v0.1
📊 Comparing models...

📦 Model 1: models/pizza_v1.okm
📦 Model 2: models/pizza_v2.okm

⏳ Running comparison tests...
  ✓ Loading models...
  ✓ Running inference on 100 test samples...
  ✓ Measuring metrics...

📈 Comparison Results:

┌─────────────────────┬──────────────┬──────────────┬─────────────┐
│ Metric              │ Model 1 (V1) │ Model 2 (V2) │ Difference  │
├─────────────────────┼──────────────┼──────────────┼─────────────┤
│ Latency (avg)       │ 245ms        │ 189ms        │ V2 -23% ⚡  │
│ Accuracy            │ 0.892        │ 0.856        │ V1 +4% 📈  │
│ Loss                │ 1.234        │ 1.156        │ V2 -6% 📉  │
│ GPU Memory          │ 2.1GB        │ 2.3GB        │ V2 +9%     │
│ Response Quality    │ 8.5/10       │ 8.2/10       │ V1 +0.3    │
└─────────────────────┴──────────────┴──────────────┴─────────────┘

💡 Recommendation: V2
   • 23% faster inference
   • Lower loss
   • Slightly lower accuracy (acceptable trade-off)

✅ Comparison completed!
```

**With Test Dataset:**
```bash
okto compare models/v1.okm models/v2.okm --dataset dataset/test.jsonl
```

---

### `okto logs`

View historical training logs and metrics saved by CONTROL and MONITOR blocks.

**Usage:**
```bash
okto logs <model_or_run_id>
```

**Options:**
- `<model_or_run_id>` - Model name or run ID

**What it shows:**
- Loss per epoch
- Validation loss
- Accuracy metrics
- CPU/GPU/RAM usage
- Decisions made by CONTROL block
- System metrics from MONITOR block

**Example:**
```bash
okto logs pizzabot_v1
```

**Output:**
```
🐙 OktoEngine v0.1
📊 Viewing logs for: pizzabot_v1

📁 Log file: runs/pizzabot_v1/logs/training.log

═══════════════════════════════════════════════════════════
📈 Training Metrics
═══════════════════════════════════════════════════════════

Epoch 1:
  Loss: 2.345 → 1.892
  Val Loss: 2.123 → 1.756
  Accuracy: 0.654 → 0.723
  GPU Usage: 78% (9.2GB / 12GB)
  RAM Usage: 12.3GB

Epoch 2:
  Loss: 1.892 → 1.654
  Val Loss: 1.756 → 1.523
  Accuracy: 0.723 → 0.789
  GPU Usage: 82% (9.8GB / 12GB)
  RAM Usage: 12.5GB

Epoch 3:
  Loss: 1.654 → 1.456
  Val Loss: 1.523 → 1.312
  Accuracy: 0.789 → 0.834
  GPU Usage: 85% (10.1GB / 12GB)
  RAM Usage: 12.7GB
  ⚠️  CONTROL: High loss detected, reducing learning rate
  ✓ CONTROL: Learning rate set to 0.00005

Epoch 4:
  Loss: 1.456 → 1.234
  Val Loss: 1.312 → 1.156
  Accuracy: 0.834 → 0.867
  GPU Usage: 88% (10.5GB / 12GB)
  RAM Usage: 12.9GB
  ✓ CONTROL: Best model saved (accuracy > 0.85)

Epoch 5:
  Loss: 1.234 → 1.123
  Val Loss: 1.156 → 1.089
  Accuracy: 0.867 → 0.892
  GPU Usage: 90% (10.8GB / 12GB)
  RAM Usage: 13.1GB
  ✓ CONTROL: Training completed successfully

═══════════════════════════════════════════════════════════
🎯 CONTROL Decisions
═══════════════════════════════════════════════════════════

Step 500:
  ✓ LOG: loss = 1.892

Step 1000:
  ✓ SAVE: checkpoint saved

Epoch 3, Step 1500:
  ⚠️  IF loss > 2.0: SET LR = 0.00005
  ✓ LOG: "High loss detected"

Epoch 4, Step 2000:
  ✓ IF accuracy > 0.85: SAVE "best_model"

═══════════════════════════════════════════════════════════
📊 System Metrics
═══════════════════════════════════════════════════════════

Average GPU Usage: 82.6%
Peak GPU Usage: 92%
Average RAM Usage: 12.7GB
Peak RAM Usage: 13.5GB
Average Temperature: 72°C
Peak Temperature: 78°C

Throughput: 3.7 samples/sec
Average Latency: 270ms/step
```

**Filter by Metric:**
```bash
okto logs pizzabot_v1 --metric loss
okto logs pizzabot_v1 --metric accuracy
okto logs pizzabot_v1 --metric gpu_usage
```

---

### `okto tune`

Auto-tune training parameters using the CONTROL block for intelligent optimization.

**Usage:**
```bash
okto tune [--file <path>]
```

**Options:**
- `--file <PATH>` - Path to OktoScript file (default: `scripts/train.okt`)

**What it does:**
- Uses CONTROL block logic to auto-adjust training
- Can adjust learning rate dynamically
- Can change batch size based on memory
- Can activate early stopping
- Can balance classes automatically
- This is unique in the market

**Example:**
```bash
okto tune
okto tune --file scripts/train.okt
```

**Output:**
```
🐙 OktoEngine v0.1
🎛️  Auto-tuning training...

📄 Reading: scripts/train.okt
✓ CONTROL block detected
✓ MONITOR block detected

🚀 Starting tuned training...

Epoch 1:
  Loss: 2.345
  ✓ CONTROL: Monitoring metrics...

Epoch 2:
  Loss: 1.892
  ✓ CONTROL: Loss improving, continuing...

Epoch 3:
  Loss: 1.654
  ⚠️  CONTROL: Loss plateau detected
  ✓ CONTROL: Reducing learning rate from 0.0001 to 0.00005
  ✓ CONTROL: Adjusting batch size from 32 to 16

Epoch 4:
  Loss: 1.456
  ✓ CONTROL: Learning rate adjustment successful
  ✓ CONTROL: Loss improving again

Epoch 5:
  Loss: 1.234
  ✓ CONTROL: Best model saved (accuracy improved)

✅ Auto-tuning completed!
📊 Final metrics:
  Loss: 1.234 (improved from 2.345)
  Accuracy: 0.892 (improved from 0.654)
  Optimizations applied: 3
```

**What makes it unique:**
- Real-time parameter adjustment based on metrics
- Uses CONTROL block logic for decision-making
- No manual intervention needed
- Adapts to training conditions automatically

---

### `okto exit`

Exit interactive mode (chat, tune, or other interactive sessions).

**Usage:**
```bash
okto exit
```

**When to use:**
- Exiting chat mode (alternative to `/exit` command)
- Exiting interactive tuning session
- Exiting session context

**Example:**
```bash
# In chat mode
You: /exit
# or
okto exit

# In interactive tuning
okto tune --interactive
# ... tuning session ...
okto exit
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

# 7. Convert to different formats
okto convert --input export/model.okm --from okm --to onnx --output export/model.onnx

# 8. Test inference
okto infer --model export/model.okm --text "Hello, how can I help?"

# 9. Interactive chat
okto chat --model export/model.okm

# 10. View training logs
okto logs my-chatbot
```

### Inference Workflow

```bash
# Direct inference
okto infer --model models/chatbot.okm --text "What are your business hours?"

# Interactive chat session
okto chat --model models/chatbot.okm
# ... chat interaction ...
# Type '/exit' to quit

# Compare two model versions
okto compare models/v1.okm models/v2.okm
```

### Conversion Workflow

```bash
# Convert PyTorch to multiple formats
okto convert --input model.pt --from pt --to gguf --output model.gguf
okto convert --input model.pt --from pt --to onnx --output model.onnx
okto convert --input model.pt --from pt --to tflite --output model.tflite

# Convert for mobile deployment
okto convert --input model.pt --from pt --to tflite --output model.tflite

# Convert for web deployment
okto convert --input model.pt --from pt --to onnx --output model.onnx
```

### Monitoring and Analysis Workflow

```bash
# View training logs
okto logs my-model

# View specific metrics
okto logs my-model --metric loss
okto logs my-model --metric gpu_usage

# Auto-tune training
okto tune

# Compare model versions
okto compare models/v1.okm models/v2.okm
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

