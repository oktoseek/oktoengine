# OktoEngine Examples

Complete working examples demonstrating OktoEngine capabilities.

---

## Table of Contents

1. [Basic Training](#basic-training)
2. [LoRA Fine-tuning](#lora-fine-tuning)
3. [Chatbot Training](#chatbot-training)
4. [Multi-format Export](#multi-format-export)

---

## Basic Training

**Location:** [`basic-training/`](./basic-training/)

Minimal working example for training a simple model.

**Files:**
- `scripts/train.okt` - Training configuration
- `dataset/train.jsonl` - Sample training data
- `dataset/val.jsonl` - Sample validation data

**Usage:**
```bash
cd basic-training
okto validate
okto train
```

---

## LoRA Fine-tuning

**Location:** [`lora-training/`](./lora-training/)

Example of efficient LoRA fine-tuning for large models.

**Files:**
- `scripts/train.okt` - LoRA configuration
- `dataset/train.jsonl` - Training data

**Usage:**
```bash
cd lora-training
okto validate
okto train
```

---

## Chatbot Training

**Location:** [`chatbot/`](./chatbot/)

Complete example for training a conversational AI model.

**Files:**
- `scripts/train.okt` - Chatbot configuration
- `dataset/train.jsonl` - Conversation data
- `dataset/val.jsonl` - Validation conversations

**Usage:**
```bash
cd chatbot
okto validate
okto train
okto eval
```

---

## Multi-format Export

**Location:** [`multi-export/`](./multi-export/)

Example showing how to export models to multiple formats.

**Files:**
- `scripts/train.okt` - Configuration with multiple export formats

**Usage:**
```bash
cd multi-export
okto train
okto export --format okm,onnx,gguf
```

---

## Running Examples

1. **Navigate to example directory:**
   ```bash
   cd examples/basic-training
   ```

2. **Validate configuration:**
   ```bash
   okto validate
   ```

3. **Train the model:**
   ```bash
   okto train
   ```

4. **Check results:**
   ```bash
   ls runs/
   ls export/
   ```

---

## Customizing Examples

All examples can be customized:

1. **Edit `scripts/train.okt`** - Modify training parameters
2. **Replace `dataset/*.jsonl`** - Use your own data
3. **Adjust `MODEL.base`** - Use different base models
4. **Modify `EXPORT.format`** - Change export formats

---

## Example Output

**Training output:**
```
🐙 OktoEngine v0.1
📄 Reading: "scripts/train.okt"

📊 Environment Check:
  ✔ Runtime: Python 3.14.0
  ✔ GPU: NVIDIA GeForce RTX 4070
  ✔ RAM: 63GB (40GB available)

🚀 Starting training pipeline...

Epoch 1/5: 100%|████████████| 500/500 [02:15<00:00, 3.70it/s]
  Loss: 2.345 → 1.892

✅ Training completed successfully!
📁 Output: runs/MyModel/
```

---

**Need help?** Check the [Getting Started Guide](../docs/GETTING_STARTED.md) or [FAQ](../docs/FAQ.md).

