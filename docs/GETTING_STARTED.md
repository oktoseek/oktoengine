# Getting Started with OktoEngine

**Your first 5 minutes with OktoEngine** - A quick guide to get you up and running.

---

## Prerequisites

- OktoEngine installed (download from [GitHub Releases](https://github.com/oktoseek/oktoengine/releases))
- Basic understanding of AI/ML concepts
- A dataset ready for training (optional for first run)

---

## Step 1: Install OktoEngine

### Download Pre-built Binary

1. Visit [GitHub Releases](https://github.com/oktoseek/oktoengine/releases)
2. Download the binary for your platform:
   - **Windows:** `okto-windows.exe`
   - **Linux:** `okto-linux`
   - **macOS:** `okto-macos`
3. Make it executable (Linux/Mac):
   ```bash
   chmod +x okto-linux
   ```
4. Add to PATH (optional but recommended)

### Verify Installation

```bash
okto --version
```

Should output: `okto 0.1.0`

---

## Step 2: Check Your System

Before starting, check if your system is ready:

```bash
okto doctor
```

This will show:
- ✅ Platform information
- ✅ RAM and CPU
- ✅ GPU detection
- ✅ CUDA availability
- ✅ Runtime environment
- ✅ Dependencies status

**If dependencies are missing:**
```bash
okto doctor --install
```

Automatically installs missing dependencies.

---

## Step 3: Create Your First Project

Initialize a new OktoScript project:

```bash
okto init my-first-model
cd my-first-model
```

This creates:
```
my-first-model/
├── scripts/
│   └── train.okt          # Your training configuration
├── dataset/
│   ├── train.jsonl        # Training data (sample)
│   └── val.jsonl          # Validation data (sample)
└── export/                # Where models will be exported
```

---

## Step 4: Prepare Your Dataset

Edit `dataset/train.jsonl` with your training data:

**dataset/train.jsonl:**
```json
{"input":"Hello","output":"Hi! How can I help you?"}
{"input":"What's the weather?","output":"I don't have access to weather data."}
{"input":"Thank you","output":"You're welcome!"}
```

**Minimum requirements:**
- At least 10 examples for basic training
- Consistent format (JSONL recommended)
- Valid JSON on each line

**Supported formats:**
- JSONL (recommended)
- CSV
- TXT
- Parquet

---

## Step 5: Configure Your Training

Edit `scripts/train.okt`:

```okt
PROJECT "MyFirstModel"
DESCRIPTION "My first AI model with OktoEngine"

ENV {
  accelerator: "gpu"
  min_memory: "8GB"
  precision: "fp16"
  install_missing: true
}

DATASET {
  train: "dataset/train.jsonl"
  validation: "dataset/val.jsonl"
}

MODEL {
  base: "gpt2"
}

TRAIN {
  epochs: 5
  batch_size: 32
  device: "auto"
}

EXPORT {
  format: ["okm"]
  path: "export/"
}
```

**Key settings:**
- `PROJECT` - Your model name
- `MODEL.base` - Base model (gpt2, distilgpt2, etc.)
- `TRAIN.epochs` - Number of training epochs
- `TRAIN.batch_size` - Batch size
- `TRAIN.device` - "auto" detects GPU/CPU automatically
- `EXPORT.format` - Output format

---

## Step 6: Validate Your Configuration

Before training, validate your configuration:

```bash
okto validate
```

**What it checks:**
- ✅ Syntax is correct
- ✅ All required fields are present
- ✅ Dataset files exist
- ✅ Model paths are valid
- ✅ Values are within allowed ranges

**Example output:**
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
  Project: MyFirstModel
  ENV: Configured
  Dataset: dataset/train.jsonl
  Model: gpt2
  Training: 5 epochs, batch size 32
  Export: ["okm"]
```

**If validation fails:**
- Check error messages
- Fix syntax errors
- Verify file paths
- Run `okto validate --debug` for detailed logs

---

## Step 7: Train Your Model

Start training:

```bash
okto train
```

**What happens:**
1. ✅ Configuration is parsed and validated
2. ✅ System environment is checked
3. ✅ Dependencies are verified
4. ✅ Dataset is loaded
5. ✅ Model is initialized (downloads from HuggingFace if needed)
6. ✅ Training loop starts
7. ✅ Progress is shown in real-time
8. ✅ Model is saved to `runs/MyFirstModel/`
9. ✅ Exported models saved to `export/`

**Example output:**
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

Epoch 2/5: 100%|████████████| 500/500 [02:14<00:00, 3.72it/s]
  Loss: 1.892 → 1.654

...

✅ Training completed successfully!
📁 Output: runs/MyFirstModel/
```

**Training time:**
- Small models (100M params): 5-15 minutes
- Medium models (1B params): 30-60 minutes
- Large models (7B params): Several hours

---

## Step 8: Check Your Results

After training completes:

**Check training output:**
```bash
ls runs/MyFirstModel/
```

**Files created:**
- `checkpoint-*/` - Training checkpoints
- `training_logs.json` - Detailed training logs
- `metrics.json` - Training metrics
- `tokenizer.json` - Tokenizer configuration

**Check exported models:**
```bash
ls export/
```

**Exported files:**
- `model.okm` - OktoSeek Model format

---

## Step 9: Evaluate Your Model (Optional)

Evaluate your trained model:

```bash
okto eval
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

## Common First Steps

### Using GPU

If you have a GPU, OktoEngine will automatically detect and use it. To ensure GPU usage:

```okt
ENV {
  accelerator: "gpu"
  precision: "fp16"
}

TRAIN {
  device: "auto"  # or "cuda" for explicit GPU
}
```

### Adding More Epochs

```okt
TRAIN {
  epochs: 10  # Increase from 5
  batch_size: 32
}
```

### Exporting to Multiple Formats

```okt
EXPORT {
  format: ["okm", "onnx", "gguf"]
  path: "export/"
}
```

### Using Debug Mode

For detailed logs during training:

```bash
okto train --debug
```

Shows:
- Parsing details
- Execution flow
- Error diagnostics
- Performance metrics

---

## Troubleshooting

### Training Fails

**Check system:**
```bash
okto doctor
```

**Check configuration:**
```bash
okto validate --debug
```

**Common issues:**
- **Out of memory:** Reduce `batch_size` in TRAIN block
- **Model not found:** Check `MODEL.base` is a valid HuggingFace model
- **Dataset not found:** Verify paths in DATASET block
- **Dependencies missing:** Run `okto doctor --install`

### Validation Fails

**Enable debug mode:**
```bash
okto validate --debug
```

**Common errors:**
- Syntax errors - Check OktoScript syntax
- Missing fields - Add required blocks
- Invalid paths - Verify file paths exist
- Invalid values - Check value ranges

### System Issues

**Check system:**
```bash
okto doctor
```

**Install dependencies:**
```bash
okto doctor --install
```

---

## Next Steps

- 📚 Read the [Complete CLI Reference](./CLI_REFERENCE.md)
- 🎯 Check out [Examples](../examples/) for advanced use cases
- 🐛 Learn about [Debug Mode](./DEBUG_GUIDE.md)
- 💡 Explore [FAQ](./FAQ.md) for common questions

---

## Quick Reference

| Task | Command |
|------|---------|
| Initialize project | `okto init <name>` |
| Validate | `okto validate` |
| Check system | `okto doctor` |
| Train | `okto train` |
| Evaluate | `okto eval` |
| Export | `okto export --format okm` |
| Debug mode | `okto train --debug` |
| Upgrade | `okto upgrade` |

---

**Need help?** Check the [FAQ](./FAQ.md) or open an issue on [GitHub](https://github.com/oktoseek/oktoengine/issues).

