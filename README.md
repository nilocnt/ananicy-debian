   <div align="center">
    
    # Ananicy-CPP Rules for Debian / Ubuntu
    
    [![GitHub Release](https://img.shields.io/github/v/release/nilocnt/ananicy-cpp-rules?style=for-the-
  badge&color=blue)](https://github.com/nilocnt/ananicy-cpp-rules/releases)
    [![Debian Package](https://img.shields.io/badge/package-.deb-orange?style=for-the-
  badge&logo=debian)](https://github.com/nilocnt/ananicy-cpp-rules/releases/latest)
    [![Architecture](https://img.shields.io/badge/arch-amd64-green?style=for-the-badge)](https://github.
  com/nilocnt/ananicy-cpp-rules/releases/latest)
    [![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg?style=for-the-badge)](LICENSE)
    
    **Ananicy-CPP** daemon with community-driven rules from **CachyOS**, packaged ready-to-use for Debian, Ubuntu,
  AnduinOS, and derivatives.
    
    [📥 Download Latest .deb](https://github.com/nilocnt/ananicy-cpp-rules/releases/latest) • [📖 Features](#-
  features) • [🚀 Installation](#-installation) • [⚙️ Configuration](#️-configuration) • [🙏 Credits](#-credits-and-
  acknowledgments)
    
    ---
    
    </div>
    
    ## 📌 Overview
    
    **Ananicy** (*ANother Auto NICe daemon*) is a system service that automatically manages process priorities
  (`nice`, `ionice`, `cgroups`, and CPU scheduler attributes) in the background.
    
    This repository bundles:
    1. The high-performance C++ implementation of the daemon: **[ananicy-cpp](https://gitlab.com/ananicy-
  cpp/ananicy-cpp)** (compiled statically with zero heavy runtime dependencies).
    2. The complete, updated ruleset from **[CachyOS ananicy-rules](https://github.com/CachyOS/ananicy-rules)**
  (over 15,800+ community rules).
    3. Pre-configured **Systemd** service integration and packaging for Debian-based systems.
    
    ---
    
    ## ✨ Features
    
    - 🎮 **Gaming Optimizations**: Automatically prioritizes native Linux and Wine/Proton games.
    - ⚡ **Low Latency**: Prioritizes audio servers (PipeWire, PulseAudio), compositor, and interactive
  applications.
    - 🧹 **Background Management**: Automatically throttles resource-heavy tasks, compilation, and file indexers so
  they don't stutter the desktop.
    - 📦 **Zero-Config Debian Package**: Install `.deb` and it immediately enables and runs as a native systemd
  service.
    - 🔒 **Lightweight & Safe**: Pre-compiled static binary with hardened systemd security directives.
    
    ---
    
    ## 🚀 Installation
    
    ### Option 1: Graphical Install (Easiest)
    1. Download the latest `.deb` package from [Releases](https://github.com/nilocnt/ananicy-cpp-
  rules/releases/latest).
    2. Double-click the downloaded `.deb` file and click **Install**.
    
    ### Option 2: Terminal Install
    
    ```bash
    # Download the latest release package
    wget https://github.com/nilocnt/ananicy-cpp-rules/releases/download/v1.2.48/ananicy-cpp-rules-1.2.48.deb
    
    # Install using apt (resolves any missing runtime dependencies automatically)
    sudo apt install ./ananicy-cpp-rules-1.2.48.deb
  ──────
  ## 🔍 Verification & Usage

  Check if the service is running and rules are loaded:

    systemctl status ananicy-cpp

  View active logs and process scans:

    journalctl -u ananicy-cpp -f

  Inspect loaded rules:

    ananicy-cpp dump rules
  ──────
  ## ⚙️ Configuration & Custom Rules

  • Main configuration: /etc/ananicy.d/ananicy.conf
  • Rule definitions: /etc/ananicy.d/00-default/

  ### Adding Custom Rules

  To add your own custom rules that persist across updates, create a file in /etc/ananicy.d/99-custom.rules:

    [
      {
        "name": "your-app",
        "type": "Game"
      }
    ]

  Restart the service to apply changes:

    sudo systemctl restart ananicy-cpp
  ──────
  ## 🤝 How to Contribute

  Contributions, rule suggestions, and improvements are welcome!

  1. For new game/application rules, check existing rules in /etc/ananicy.d/00-default/.
  2. Format rules following standard JSON syntax.
  3. Open a Pull Request or create an Issue.
  ──────
  ## 🙏 Credits and Acknowledgments

  This project is an unofficial downstream packaging distribution that brings together the excellent work of the
  open-source community:

  • Ananicy-Cpp https://gitlab.com/ananicy-cpp/ananicy-cpp — Created and maintained by the Ananicy-Cpp team.
  Licensed under GPL-3.0.
  • CachyOS ananicy-rules https://github.com/CachyOS/ananicy-rules — Created and maintained by the CachyOS Team
  https://cachyos.org and contributors.
  • Debian / Ubuntu Packaging — Maintained by nilocnt https://github.com/nilocnt.
  ──────
  ## 📄 License

  Distributed under the GNU General Public License v3.0 (GPL-3.0). See LICENSE for more information.

___
