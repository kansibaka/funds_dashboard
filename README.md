# Funds Dashboard

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A production-grade development environment and infrastructure setup for dashboard applications, with comprehensive documentation for WSL2, Docker, and GitHub integration on Windows 11.

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Quick Start](#quick-start)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Project Structure](#project-structure)
- [Development](#development)
- [Documentation](#documentation)
- [Changelog](#changelog)
- [License](#license)

## Overview

This project provides a **complete, reproducible development environment** for building and maintaining dashboard applications. It includes step-by-step setup guides, best practices for containerized development, and infrastructure documentation.

The setup ensures:
- ✅ Production-like Linux environment via WSL2
- ✅ Containerized development with Docker
- ✅ Secure GitHub authentication with SSH
- ✅ Professional developer experience with VS Code
- ✅ Machine-independent reproducibility

## Tech Stack

| Technology | Purpose |
|------------|---------|
| Ubuntu (WSL2) | Linux development environment on Windows |
| Docker | Containerized application development |
| Visual Studio Code | IDE with Remote WSL extension |
| GitHub | Remote repository hosting |
| SSH | Secure authentication |

## Why This Project?

Setting up a consistent development environment on Windows 11 for dashboard applications can be complex. This project provides:

- **Reproducibility** - Same environment across all machines
- **Best Practices** - Industry-standard tooling and workflows
- **Documentation** - Step-by-step guides for every component
- **Time Savings** - Avoid common pitfalls and configuration headaches

## Tech Stack

- **WSL2 + Ubuntu Setup** - Complete Windows 11 development environment
- **Docker Integration** - Containerized applications with WSL backend
- **GitHub SSH Auth** - Secure SSH-based repository access
- **VS Code Configuration** - Remote WSL development setup
- **Environment Documentation** - Detailed setup and migration guides
- **Architecture Guidance** - Best practices for project organization

## Quick Start

### For Existing Contributors

1. Ensure you have WSL2, Docker Desktop, and VS Code installed
2. Clone the repository:
   ```bash
   git clone git@github.com:yourusername/funds_dashboard.git
   cd funds_dashboard
   ```
3. Follow the [Development](#development) section below

### For New Setup

See [Installation](#installation) for complete step-by-step instructions.

## Prerequisites

### Windows 11
- [ ] WSL2 with Ubuntu installed
- [ ] Docker Desktop (with WSL backend enabled)
- [ ] Visual Studio Code
- [ ] SSH key configured with GitHub

**Not sure how to set these up?** See the detailed [Development Environment Setup Guide](./docs/dev-environment-setup.md).

## Installation

### 1. **Environment Setup**
Follow the comprehensive guide in [`docs/dev-environment-setup.md`](./docs/dev-environment-setup.md). This covers:
- WSL2 installation and configuration
- Docker Desktop setup with WSL integration
- SSH key generation and GitHub authentication
- VS Code Remote - WSL configuration

### 2. **Clone Repository**
```bash
git clone git@github.com:yourusername/funds_dashboard.git
cd funds_dashboard
```

### 3. **Verify Setup**
```bash
# Inside the WSL terminal:
pwd                    # Should show: /home/yourusername/projects/funds_dashboard
git remote -v          # Should show SSH URLs (git@github.com:...)
docker ps              # Should list containers (or show empty list, but no error)
```

## Project Structure

```
funds_dashboard/
├── README.md                         # This file
├── .gitignore                        # Git ignore rules
├── docs/
│   ├── dev-environment-setup.md      # Complete environment setup guide
│   └── CHANGELOG.md                  # Version history
└── .git/                            # Git repository
```

## Development

### Opening the Project

```bash
# From WSL Ubuntu terminal in ~/projects:
cd funds_dashboard
code .
```

Verify VS Code shows **"WSL: Ubuntu"** in the bottom-left corner.

### Running Docker

```bash
# Verify Docker is accessible
docker ps

# Example: List all containers
docker container ls -a
```

### Making Changes

1. Create a feature branch: `git checkout -b feature/your-feature`
2. Make your changes
3. Commit with clear messages: `git commit -m "Add feature description"`
4. Push to GitHub: `git push origin feature/your-feature`

## Documentation

Key documentation files:

| Document | Purpose |
|----------|---------|
| [`docs/dev-environment-setup.md`](./docs/dev-environment-setup.md) | Step-by-step WSL2 + Docker + GitHub setup for Windows 11 |
| [`docs/CHANGELOG.md`](./docs/CHANGELOG.md) | Project version history and notable changes |

## Contributing

Contributions are welcome! Here's how you can help:

1. **Fork** the repository
2. **Create** a feature branch: `git checkout -b feature/your-feature`
3. **Commit** your changes: `git commit -m "Add feature description"`
4. **Push** to the branch: `git push origin feature/your-feature`
5. **Open** a Pull Request

Please ensure your changes follow the existing documentation style and include updates to relevant guides if applicable.

## Troubleshooting

### Docker not starting
- Ensure Docker Desktop is installed with WSL backend enabled
- Try: `wsl --shutdown` then restart Docker Desktop
- Check Docker Desktop > Settings > Resources > WSL Integration

### SSH key not working
- Verify your key is added to the SSH agent: `ssh-add -l`
- Check GitHub has your public key at: github.com/settings/keys
- Ensure correct permissions: `chmod 600 ~/.ssh/id_ed25519`

### WSL2 not enabled
- Run `winver` to confirm Windows 11 (build 22000+)
- Enable WSL: `wsl --install`
- Enable Virtual Machine Platform in Windows Features

**Still stuck?** Check the [dev environment setup guide](./docs/dev-environment-setup.md) for detailed troubleshooting.

## Roadmap

- [ ] Add Docker Compose configuration for multi-service setup
- [ ] Include CI/CD pipeline examples (GitHub Actions)
- [ ] Add sample dashboard application code
- [ ] Include development scripts for common tasks
- [ ] Add automated environment validation

## Changelog

See [`docs/CHANGELOG.md`](./docs/CHANGELOG.md) for release notes and version history.

**Current Version:** 0.1.1

## License

This project is licensed under the [MIT License](https://opensource.org/licenses/MIT) - see the LICENSE file for details.

---

**Questions?** Refer to the [dev environment setup guide](./docs/dev-environment-setup.md) or check the troubleshooting section there.
