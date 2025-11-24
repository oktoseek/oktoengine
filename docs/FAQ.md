# OktoEngine FAQ

Frequently Asked Questions about OktoEngine CLI.

---

## General Questions

### Q: What is OktoEngine?

**A:** OktoEngine is the official execution engine for OktoScript—a professional CLI tool that transforms declarative AI configurations into trained, production-ready models. It provides a complete command-line interface for training, evaluating, and exporting AI models.

### Q: Do I need to know Python to use OktoEngine?

**A:** No! OktoEngine provides a complete CLI interface. You only need to write OktoScript configuration files. The engine handles all the complex operations behind the scenes.

### Q: What models can I train with OktoEngine?

**A:** OktoEngine supports any model compatible with modern AI frameworks. From small models (millions of parameters) to large language models (billions of parameters). The engine automatically handles model loading, training, and optimization.

### Q: Is OktoEngine free?

**A:** OktoEngine binary releases are available for download. See the [LICENSE](../LICENSE) file for licensing terms.

---

## Installation & Setup

### Q: How do I install OktoEngine?

**A:** Download the latest release from [GitHub Releases](https://github.com/oktoseek/oktoengine/releases) for your platform:
- Windows: `okto-windows.exe`
- Linux: `okto-linux`
- macOS: `okto-macos`

Make it executable (Linux/Mac) and optionally add to PATH.

### Q: How do I update OktoEngine?

**A:** Simply run:
```bash
okto upgrade
```

This automatically downloads and installs the latest version.

### Q: What are the system requirements?

**A:** 
- **Minimum:** 8GB RAM, 10GB storage, compatible runtime
- **Recommended for training:** GPU with CUDA, 32GB+ RAM, 50GB+ SSD storage

Check your system:
```bash
okto doctor
```

---

## Training

### Q: Can I train models without a GPU?

**A:** Yes! OktoEngine automatically detects available hardware and uses CPU when GPU is not available. Training will be slower but fully functional. Set `device: "auto"` in your TRAIN block for automatic detection.

### Q: How long does training take?

**A:** Training time depends on:
- Model size (parameters)
- Dataset size
- Hardware (GPU/CPU)
- Number of epochs

**Rough estimates:**
- Small models (100M params): 5-15 minutes
- Medium models (1B params): 30-60 minutes
- Large models (7B params): Several hours

### Q: Can I resume training from a checkpoint?

**A:** Yes! OktoEngine automatically saves checkpoints during training. You can resume from any checkpoint by configuring your OktoScript file.

### Q: What if training fails?

**A:** 
1. Check system: `okto doctor`
2. Validate configuration: `okto validate --debug`
3. Check error messages for specific issues
4. Common fixes:
   - Reduce `batch_size` if out of memory
   - Verify dataset paths exist
   - Check model name is valid
   - Install missing dependencies: `okto doctor --install`

---

## Configuration

### Q: How do I validate my OktoScript file?

**A:** 
```bash
okto validate
```

Or with debug mode:
```bash
okto validate --debug
```

### Q: What if validation fails?

**A:** 
1. Enable debug mode: `okto validate --debug`
2. Check error messages
3. Verify syntax matches OktoScript grammar
4. Check file paths exist
5. Verify values are within allowed ranges

### Q: Can I use models from HuggingFace?

**A:** Yes! OktoEngine automatically downloads models from HuggingFace. Just specify the model identifier in your MODEL block:

```okt
MODEL {
  base: "gpt2"  # Downloads automatically
}
```

### Q: What export formats are supported?

**A:** OktoEngine supports multiple formats:
- `okm` - OktoSeek Model format (optimized)
- `onnx` - ONNX format (universal)
- `gguf` - GGUF format (local inference)
- `safetensors` - SafeTensors format (HuggingFace)

---

## Debug Mode

### Q: What is debug mode?

**A:** Debug mode provides detailed, real-time logging of OktoEngine's internal operations. It shows parsing details, execution flow, and error diagnostics.

### Q: How do I enable debug mode?

**A:** 
```bash
okto train --debug
okto validate --debug
```

Or via environment variable:
```bash
OKTO_DEBUG=1 okto train
```

### Q: When should I use debug mode?

**A:** Use debug mode when:
- Troubleshooting parsing errors
- Understanding execution flow
- Performance analysis
- Configuration debugging

---

## System & Dependencies

### Q: How do I check my system?

**A:** 
```bash
okto doctor
```

Shows GPU, CUDA, RAM, runtime, and dependencies.

### Q: How do I install missing dependencies?

**A:** 
```bash
okto doctor --install
```

Automatically installs missing dependencies.

### Q: What dependencies are required?

**A:** OktoEngine automatically manages dependencies. Required packages are installed automatically when needed. Check with:
```bash
okto doctor
```

---

## Errors & Troubleshooting

### Q: Training fails with "Model not found"

**A:** 
1. Check the model name in MODEL block is valid
2. Verify it's a valid HuggingFace model identifier
3. Check internet connection (for downloading)
4. Try a different model: `gpt2`, `distilgpt2`, etc.

### Q: Training fails with "Dataset not found"

**A:** 
1. Verify dataset paths in DATASET block
2. Check files exist at specified paths
3. Use absolute paths if relative paths fail
4. Verify file format (JSONL, CSV, etc.)

### Q: Training fails with "Out of memory"

**A:** 
1. Reduce `batch_size` in TRAIN block
2. Use LoRA fine-tuning instead of full fine-tuning
3. Reduce model size
4. Close other applications
5. Use CPU if GPU memory is insufficient

### Q: Validation fails with syntax error

**A:** 
1. Enable debug mode: `okto validate --debug`
2. Check OktoScript syntax matches grammar
3. Verify all required blocks are present
4. Check for typos in block names
5. Verify quotes around string values

---

## Performance

### Q: How can I speed up training?

**A:** 
1. Use GPU: Set `accelerator: "gpu"` in ENV block
2. Use mixed precision: Set `precision: "fp16"` in ENV block
3. Increase batch size (if memory allows)
4. Use LoRA fine-tuning for large models
5. Use SSD storage for datasets

### Q: How do I monitor training progress?

**A:** Training progress is shown in real-time in the terminal:
- Progress bars
- Loss values
- Learning rate
- GPU memory usage
- Epoch progress

### Q: Can I train multiple models simultaneously?

**A:** Yes, but ensure you have sufficient resources (GPU memory, RAM). Run training in separate terminals or use different GPU devices.

---

## Integration

### Q: Will OktoEngine be integrated into OktoSeek IDE?

**A:** Yes! OktoEngine will be integrated into OktoSeek IDE for visual training workflows, including:
- Visual pipeline builder
- Real-time dashboard
- One-click training
- Project management

### Q: Can I use OktoEngine in scripts?

**A:** Yes! OktoEngine is designed for CLI usage and can be integrated into scripts, CI/CD pipelines, and automation workflows.

---

## Licensing

### Q: Is OktoEngine open source?

**A:** No. OktoEngine is proprietary software. Binary releases are available for download, but the source code is proprietary. See [LICENSE](../LICENSE) for details.

### Q: Can I redistribute OktoEngine?

**A:** See the [LICENSE](../LICENSE) file for redistribution terms.

---

## Support

### Q: Where can I get help?

**A:** 
- **Documentation:** Check [docs/](./) folder
- **GitHub Issues:** https://github.com/oktoseek/oktoengine/issues
- **Email:** service@oktoseek.com
- **Website:** https://www.oktoseek.com

### Q: How do I report a bug?

**A:** 
1. Open an issue on [GitHub](https://github.com/oktoseek/oktoengine/issues)
2. Include:
   - OktoEngine version: `okto --version`
   - System information: `okto doctor`
   - Error messages
   - Steps to reproduce
   - Debug output (if applicable)

---

## Advanced

### Q: Can I customize training behavior?

**A:** Yes, through OktoScript configuration:
- Training parameters (epochs, batch size, learning rate)
- Optimizer settings
- Scheduler configuration
- Checkpoint settings
- Export formats

### Q: Can I use custom datasets?

**A:** Yes! OktoEngine supports multiple dataset formats:
- JSONL (recommended)
- CSV
- TXT
- Parquet

Just specify the path in your DATASET block.

### Q: How do I export to multiple formats?

**A:** 
```okt
EXPORT {
  format: ["okm", "onnx", "gguf"]
  path: "export/"
}
```

---

**Need more help?** Check the [Getting Started Guide](./GETTING_STARTED.md) or [CLI Reference](./CLI_REFERENCE.md).

