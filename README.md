<p align="center">
  <img src="./assets/okto_logo.png" alt="OktoEngine Banner" width="50%" />
</p>

<h1 align="center">OktoEngine</h1>

<p align="center">
  <strong>Professional CLI Engine for Training AI Models with OktoScript</strong>
</p>

<p align="center">
  Built by <strong>OktoSeek AI</strong> for the <strong>OktoSeek ecosystem</strong>
</p>

<p align="center">
  <a href="https://www.oktoseek.com/">OktoSeek Homepage</a> •
  <a href="https://github.com/oktoseek/oktoscript">OktoScript Language</a> •
  <a href="https://x.com/oktoseek">Twitter</a> •
  <a href="https://www.youtube.com/@Oktoseek">YouTube</a>
</p>

---

## Table of Contents

1. [What is OktoEngine?](#-what-is-oktoengine)
2. [Quick Start](#-quick-start)
3. [Key Features](#-key-features)
4. [Installation](#-installation)
5. [CLI Commands](#️-cli-commands)
6. [Training Capabilities](#-training-capabilities)
7. [Debug Mode](#-debug-mode)
8. [Examples](#-examples)
9. [System Requirements](#-system-requirements)
10. [Documentation](#-documentation)
11. [FAQ](#-frequently-asked-questions-faq)
12. [License](#-license)
13. [Contact](#-contact)

---

## 🚀 Quick Start

**Get started with OktoEngine in 3 steps:**

1. **Download the latest release** from [GitHub Releases](https://github.com/oktoseek/oktoengine/releases)
2. **Initialize a project:** `okto init my-project`
3. **Train your model:** `okto train`

```bash
# Initialize a new project
okto init my-ai-model

# Navigate to project
cd my-ai-model

# Validate your OktoScript configuration
okto validate

# Train your model
okto train
```

📚 **Full documentation:** [`docs/GETTING_STARTED.md`](./docs/GETTING_STARTED.md)  
🔍 **CLI Reference:** [`docs/CLI_REFERENCE.md`](./docs/CLI_REFERENCE.md)

---

## 🚀 What is OktoEngine?

**OktoEngine** is the official execution engine for **OktoScript**—a powerful CLI tool that transforms declarative AI configurations into trained, production-ready models.

### Built for Scale

OktoEngine is engineered to handle:
- ✅ **Models of any size** - From millions to billions of parameters
- ✅ **Complex training pipelines** - Full fine-tuning, LoRA adapters, and more
- ✅ **Production workloads** - Optimized for real-world AI development
- ✅ **Enterprise-grade reliability** - Robust error handling and validation

### Why OktoEngine?

**Traditional Approach:**
```python
# Hundreds of lines of Python code
# Complex configuration management
# Error-prone manual setup
# Difficult to reproduce
```

**With OktoEngine:**
```okt
PROJECT "MyModel"
MODEL { base: "gpt2" }
DATASET { train: "dataset/train.jsonl" }
TRAIN { epochs: 5, batch_size: 32 }
EXPORT { format: ["okm"] }
```

**One command:** `okto train` → **Trained model ready for deployment**

---

## ✨ Key Features

### 🎯 **Complete CLI Interface**

Professional command-line interface with intuitive commands:

```bash
okto init          # Initialize new projects
okto validate      # Validate OktoScript files
okto train         # Train models
okto eval          # Evaluate models
okto export        # Export to multiple formats
okto doctor        # System diagnostics
okto upgrade       # Auto-update engine
okto about         # Engine information
```

### 🔧 **Advanced Training Capabilities**

- **Full Fine-tuning** - Train entire models from scratch
- **LoRA Fine-tuning** - Efficient adapter-based training
- **Multi-dataset Training** - Combine datasets with weighted sampling
- **Automatic Checkpointing** - Never lose progress
- **Real-time Metrics** - Monitor training in the terminal

### 📊 **Detailed Metrics & Monitoring**

Real-time training metrics displayed directly in your terminal:

```
🚀 Starting training pipeline...

Epoch 1/5: 100%|████████████| 500/500 [02:15<00:00, 3.70it/s]
  Loss: 2.345 → 1.892
  Learning Rate: 5e-5
  GPU Memory: 8.2GB / 12GB

Epoch 2/5: 100%|████████████| 500/500 [02:14<00:00, 3.72it/s]
  Loss: 1.892 → 1.654
  ...
```

### 🐛 **Debug Mode**

Comprehensive debug mode for troubleshooting:

```bash
okto train --debug
okto validate --debug
```

Shows detailed parsing logs, execution flow, and error diagnostics.

### 🔄 **Automatic Updates**

Built-in upgrade system:

```bash
okto upgrade
```

Automatically downloads and installs the latest version from GitHub Releases.

### 🏥 **System Diagnostics**

Comprehensive environment checking:

```bash
okto doctor
```

Checks GPU, CUDA, RAM, dependencies, and provides recommendations.

### 📦 **Dependency Management**

Automatic dependency installation:

```bash
okto doctor --install
```

Installs missing dependencies automatically.

---

## 📥 Installation

### Download Pre-built Binaries

Download the latest release for your platform:

- **Windows:** `okto-windows.exe`
- **Linux:** `okto-linux`
- **macOS:** `okto-macos`

Available at: [GitHub Releases](https://github.com/oktoseek/oktoengine/releases)

### Upgrade Existing Installation

```bash
okto upgrade
```

Automatically updates to the latest version.

---

## 🖥️ CLI Commands

### Core Commands

**Initialize Project:**
```bash
okto init my-project
```
Creates a new OktoScript project with proper folder structure.

**Validate Configuration:**
```bash
okto validate
okto validate --file scripts/train.okt
```
Validates OktoScript syntax and configuration.

**Train Model:**
```bash
okto train
okto train --file scripts/train.okt
okto train --debug  # Enable debug mode
```
Executes the complete training pipeline.

**Evaluate Model:**
```bash
okto eval --file scripts/train.okt
```
Evaluates a trained model against test datasets.

**Export Model:**
```bash
okto export --format okm --file scripts/train.okt
okto export --format onnx
```
Exports trained models to various formats.

### Utility Commands

**System Diagnostics:**
```bash
okto doctor              # Check system
okto doctor --install    # Auto-install dependencies
```

**Upgrade Engine:**
```bash
okto upgrade
```
Automatically updates to the latest version.

**About:**
```bash
okto about
```
Shows information about OktoEngine and OktoScript.

**List Resources:**
```bash
okto list projects
okto list models
okto list datasets
```

### Global Flags

```bash
--debug    # Enable debug mode (detailed logs)
--help     # Show help
--version  # Show version
```

📖 **Complete CLI Reference:** [`docs/CLI_REFERENCE.md`](./docs/CLI_REFERENCE.md)

---

## 🎓 Training Capabilities

### Supported Model Sizes

OktoEngine can train models of any size:

- **Small Models** (1M - 100M parameters) - Fast training, minimal resources
- **Medium Models** (100M - 1B parameters) - Balanced performance
- **Large Models** (1B - 7B parameters) - Requires GPU, optimized training
- **Very Large Models** (7B+ parameters) - Enterprise-grade, multi-GPU support

### Training Methods

**Full Fine-tuning:**
```okt
TRAIN {
  epochs: 5
  batch_size: 32
  device: "auto"
}
```

**LoRA Fine-tuning:**
```okt
FT_LORA {
  lora_rank: 8
  lora_alpha: 32
  epochs: 3
}
```

### Automatic Optimizations

- **Mixed Precision Training** - FP16/BF16 support
- **Gradient Accumulation** - Train large models on smaller GPUs
- **Automatic Device Selection** - CPU/GPU/CUDA detection
- **Memory Optimization** - Efficient memory management
- **Checkpoint Management** - Automatic saving and resuming

---

## 🐛 Debug Mode

Debug mode provides detailed insights into the engine's operation:

### Enable Debug Mode

```bash
# Via command flag
okto train --debug
okto validate --debug

# Via environment variable
OKTO_DEBUG=1 okto train
```

### What Debug Mode Shows

**Parsing Details:**
```
DEBUG: Starting parse_oktoscript. Input preview: '# okto_version: "1.0" PROJECT...'
DEBUG: Parsed version: Some("1.0")
DEBUG: Parsed project: my-model
DEBUG: After PROJECT, remaining input: 'ENV { accelerator: "gpu"...'
```

**Execution Flow:**
```
DEBUG: Attempting to parse ENV block...
DEBUG: Parsed ENV field: accelerator = gpu
DEBUG: Parsed ENV field: precision = fp16
DEBUG: Successfully parsed ENV block with 5 fields
```

**Error Diagnostics:**
```
DEBUG: Failed to parse key in ENV block. Input: 'accelerator: "gpu"...'
DEBUG: Failed to parse ':' after key 'accelerator'. Input: '"gpu"...'
```

### Use Cases

- **Troubleshooting parsing errors** - See exactly where parsing fails
- **Understanding execution flow** - Track how your configuration is processed
- **Performance analysis** - Identify bottlenecks
- **Configuration debugging** - Verify your OktoScript is parsed correctly

📖 **Debug Guide:** [`docs/DEBUG_GUIDE.md`](./docs/DEBUG_GUIDE.md)

---

## 📚 Examples

### Basic Training Example

**scripts/train.okt:**
```okt
PROJECT "ChatBot"
ENV {
  accelerator: "gpu"
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

**Terminal Output:**
```bash
$ okto train

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

✅ Training completed successfully!
📁 Output: runs/ChatBot/
```

### Advanced Example with LoRA

See [`examples/lora-training.okt`](./examples/lora-training.okt) for a complete LoRA fine-tuning example.

### Complete Project Examples

- [`examples/basic-training/`](./examples/basic-training/) - Minimal working example
- [`examples/chatbot/`](./examples/chatbot/) - Conversational AI training
- [`examples/vision-model/`](./examples/vision-model/) - Computer vision pipeline

📖 **More Examples:** [`examples/README.md`](./examples/README.md)

---

## 💻 System Requirements

### Minimum Requirements

- **OS:** Windows 10+, Linux (Ubuntu 20.04+), macOS 11+
- **RAM:** 8GB (16GB recommended)
- **Storage:** 10GB free space
- **Runtime:** Compatible runtime environment

### Recommended for Training

- **GPU:** NVIDIA GPU with CUDA support (8GB+ VRAM)
- **RAM:** 32GB+ for large models
- **Storage:** SSD with 50GB+ free space
- **CPU:** Multi-core processor (8+ cores)

### Check Your System

```bash
okto doctor
```

Shows detailed system information and recommendations.

---

## 📚 Documentation

Complete documentation for OktoEngine:

- 📖 **[Getting Started Guide](./docs/GETTING_STARTED.md)** - Your first 5 minutes
- 🖥️ **[CLI Reference](./docs/CLI_REFERENCE.md)** - Complete command reference
- 🐛 **[Debug Guide](./docs/DEBUG_GUIDE.md)** - Debug mode usage
- 💡 **[Examples](./examples/)** - Working examples
- ❓ **[FAQ](./docs/FAQ.md)** - Frequently Asked Questions
- 📋 **[Changelog](./CHANGELOG.md)** - Version history

### Advanced Topics

- **Training Optimization** - Best practices for efficient training
- **Error Handling** - Troubleshooting common issues
- **Performance Tuning** - Maximize training speed
- **Integration** - Using OktoEngine in your workflow

---

## ❓ Frequently Asked Questions (FAQ)

**Q: What models can I train with OktoEngine?**  
A: OktoEngine supports any model compatible with modern AI frameworks. From small models (millions of parameters) to large language models (billions of parameters).

**Q: Do I need to know Python to use OktoEngine?**  
A: No! OktoEngine provides a complete CLI interface. You only need to write OktoScript configuration files.

**Q: Can I train models without a GPU?**  
A: Yes, OktoEngine automatically detects available hardware and uses CPU when GPU is not available. Training will be slower but fully functional.

**Q: How do I update OktoEngine?**  
A: Simply run `okto upgrade` to automatically download and install the latest version.

**Q: What formats can I export to?**  
A: OktoEngine supports multiple export formats: OKM (OktoSeek), ONNX, GGUF, SafeTensors, and more.

**Q: Can I resume training from a checkpoint?**  
A: Yes, OktoEngine automatically saves checkpoints and can resume training from any checkpoint.

📖 **[Complete FAQ →](./docs/FAQ.md)**

---

## 🔮 Future Integration

OktoEngine will be integrated into **OktoSeek IDE** for visual training workflows:

- 🎯 **Visual Pipeline Builder** - Drag-and-drop training configuration
- 📊 **Real-time Dashboard** - Live training metrics and visualization
- 🔄 **One-click Training** - Train models directly from the IDE
- 📁 **Project Management** - Organize and manage multiple training projects

---

## 🐙 Powered by OktoSeek AI

**OktoEngine** is developed and maintained by **OktoSeek AI**.

- **Official website:** https://www.oktoseek.com
- **OktoScript Language:** https://github.com/oktoseek/oktoscript
- **Twitter:** https://x.com/oktoseek
- **YouTube:** https://www.youtube.com/@Oktoseek
- **Repository:** https://github.com/oktoseek/oktoengine

---

## 📄 License

This software is proprietary and licensed under the End User License Agreement (EULA). See [LICENSE](./LICENSE) file for details.

**Important:** OktoEngine is not open source. Binary releases are available for download, but the source code is proprietary.

---

## 📧 Contact

For questions, support, or licensing inquiries:

- **Email:** service@oktoseek.com
- **GitHub Issues:** https://github.com/oktoseek/oktoengine/issues
- **Website:** https://www.oktoseek.com

---

<p align="center">
  Made with ❤️ by the <strong>OktoSeek AI</strong> team
</p>

