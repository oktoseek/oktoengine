# Changelog

All notable changes to OktoEngine will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [0.1.0] - 2025-01-XX

### Added

#### Core Features
- **Initial release** of OktoEngine CLI
- Complete OktoScript parser with full grammar support
- Training pipeline execution
- Model evaluation and export
- System diagnostics and environment checking

#### CLI Commands
- `okto init` - Initialize new OktoScript projects
- `okto validate` - Validate OktoScript files
- `okto train` - Train models from OktoScript
- `okto eval` - Evaluate trained models
- `okto export` - Export models to multiple formats
- `okto list` - List projects, models, and datasets
- `okto doctor` - System diagnostics
- `okto doctor --install` - Automatic dependency installation
- `okto upgrade` - Automatic engine updates
- `okto about` - Show engine information

#### Features
- **Debug mode** - Comprehensive debug logging via `--debug` flag
- **Automatic dependency management** - Installs missing dependencies
- **HuggingFace integration** - Automatic model downloading
- **Multi-format export** - Support for OKM, ONNX, GGUF, SafeTensors
- **Real-time metrics** - Training progress and metrics in terminal
- **Error handling** - Detailed error messages with troubleshooting tips
- **Cross-platform support** - Windows, Linux, macOS

#### Training Capabilities
- Full fine-tuning support
- LoRA fine-tuning support
- Automatic checkpoint management
- Mixed precision training (FP16/BF16)
- Automatic device selection (CPU/GPU)
- Gradient accumulation
- Memory optimization

#### System Features
- GPU detection and utilization
- CUDA support detection
- RAM and CPU monitoring
- Runtime environment checking
- Dependency verification
- Automatic updates via GitHub Releases

#### Documentation
- Complete CLI reference
- Getting started guide
- Debug mode guide
- FAQ with common questions
- Example projects and configurations

### Technical Details

- Built with Rust for performance and reliability
- Professional CLI interface with intuitive commands
- Robust error handling and validation
- Comprehensive logging system
- Cross-platform binary releases

---

## [Unreleased]

### Planned Features
- Integration with OktoSeek IDE
- Visual training dashboard
- Advanced monitoring and telemetry
- Multi-GPU training support
- Distributed training support
- Model serving capabilities
- API server mode
- Web dashboard interface

---

## Version History

- **0.1.0** (2025-01-XX) - Initial release

---

**For detailed information about each version, see the [GitHub Releases](https://github.com/oktoseek/oktoengine/releases) page.**

---

Copyright © 2025 OktoSeek AI. All rights reserved.

