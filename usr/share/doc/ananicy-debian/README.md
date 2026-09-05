# Ananicy-CPP Debian Package

[![GitHub Release](https://img.shields.io/github/v/release/nilocnt/ananicy-debian?style=for-the-badge)](https://github.com/nilocnt/ananicy-debian/releases)
[![Package](https://img.shields.io/badge/package-.deb-orange?style=for-the-badge&logo=debian)](https://github.com/nilocnt/ananicy-debian/releases/latest)
[![Architecture](https://img.shields.io/badge/architecture-amd64-green?style=for-the-badge)](https://github.com/nilocnt/ananicy-debian/releases/latest)
[![License](https://img.shields.io/badge/license-GPL--3.0-blue?style=for-the-badge)](LICENSE)

An unofficial Debian package of [Ananicy-CPP](https://gitlab.com/ananicy-cpp/ananicy-cpp), bundled with the community-maintained rules from [CachyOS ananicy-rules](https://github.com/CachyOS/ananicy-rules).

The package provides a ready-to-use systemd service for Debian, Ubuntu, AnduinOS, and compatible distributions.

## Overview

Ananicy-CPP is a daemon that automatically adjusts process priorities according to configurable rules. It can manage `nice`, `ionice`, scheduler attributes, OOM score adjustments, and cgroups to improve responsiveness for interactive workloads.

This repository is a downstream packaging project. It combines the Ananicy-CPP executable, the packaged rule set, configuration files, and systemd integration into an installable `amd64` Debian package.

## Features

- Automatic process-priority management.
- Rules for games, desktop applications, audio services, and background workloads.
- Community-maintained rules sourced from CachyOS.
- Native systemd integration with automatic startup.
- Resource and service hardening directives.
- Configuration under `/etc/ananicy.d/`.
- Support for custom local rules.

## Requirements

- Debian or a Debian-based distribution.
- `systemd`.
- `amd64` architecture.
- Root or `sudo` access.

The package declares its runtime dependencies in `DEBIAN/control`, including `systemd`, `libc6`, `libstdc++6`, and `libsystemd0`.

## Installation

Download the latest package from the [GitHub Releases page](https://github.com/nilocnt/ananicy-debian/releases/latest), then install it with:

```bash
sudo apt install ./ananicy-debian_VERSION_amd64.deb
```

The package enables and starts `ananicy-cpp.service` automatically when systemd is available.

## Verification and usage

Check the service status:

```bash
systemctl status ananicy-cpp.service
```

View live service logs:

```bash
sudo journalctl -u ananicy-cpp.service -f
```

Inspect the rules loaded by the daemon:

```bash
ananicy-cpp dump rules
```

## Configuration

The main configuration file is:

```text
/etc/ananicy.d/ananicy.conf
```

Packaged rule files are installed under:

```text
/etc/ananicy.d/
```

After changing configuration or rules, restart the service:

```bash
sudo systemctl restart ananicy-cpp.service
```

### Custom rules

Add local rules to `/etc/ananicy.d/` using the syntax supported by Ananicy-CPP. Keep local changes separate from packaged files so they can be managed independently during package upgrades.

Example:

```json
{ "name": "your-application", "type": "Game" }
```

Avoid absolute executable paths. Ananicy-CPP matches process names.

The upstream rules project provides additional examples and contribution guidance in its [rules README](https://github.com/CachyOS/ananicy-rules).

## Service management

```bash
sudo systemctl start ananicy-cpp.service
sudo systemctl stop ananicy-cpp.service
sudo systemctl restart ananicy-cpp.service
sudo systemctl enable ananicy-cpp.service
sudo systemctl disable ananicy-cpp.service
```

The installed unit is:

```text
/usr/lib/systemd/system/ananicy-cpp.service
```

The service runs:

```text
/usr/bin/ananicy-cpp start
```

## Building the package

This repository contains a prepared Debian package tree. Build it with:

```bash
dpkg-deb --build --root-owner-group . ../ananicy-debian_VERSION_amd64.deb
```

Inspect the generated package with:

```bash
dpkg-deb --info ../ananicy-debian_VERSION_amd64.deb
dpkg-deb --contents ../ananicy-debian_VERSION_amd64.deb
```

Generated packages and build artifacts are excluded by `.gitignore`.

## Package layout

```text
DEBIAN/
├── conffiles
├── control
├── postinst
├── postrm
└── prerm
etc/
├── ananicy.d/
└── security/limits.d/
usr/
├── bin/
│   └── ananicy-cpp
├── lib/
│   └── systemd/system/
│       └── ananicy-cpp.service
└── share/
    └── doc/
        ├── ananicy-cpp-rules/
        │   └── upstream rule documentation
        └── ananicy-debian/
            ├── README.md
            ├── changelog.Debian
            └── copyright
```

## Contributing

Bug reports, packaging improvements, and rule suggestions are welcome through [GitHub Issues](https://github.com/nilocnt/ananicy-debian/issues) and pull requests.

For new process rules, first check the upstream [CachyOS ananicy-rules repository](https://github.com/CachyOS/ananicy-rules) and follow its contribution guidelines.

## Credits

- [Ananicy-CPP](https://gitlab.com/ananicy-cpp/ananicy-cpp) — daemon implementation.
- [CachyOS ananicy-rules](https://github.com/CachyOS/ananicy-rules) — community-maintained rules.
- Debian packaging and systemd integration — maintained by [nilocnt](https://github.com/nilocnt).

## License

This packaging project is distributed under the [GNU General Public License v3.0](LICENSE). Upstream Ananicy-CPP and rule files remain subject to their respective licenses and attribution requirements.

## Links

- [Project repository](https://github.com/nilocnt/ananicy-debian)
- [Latest releases](https://github.com/nilocnt/ananicy-debian/releases/latest)
- [Ananicy-CPP upstream project](https://gitlab.com/ananicy-cpp/ananicy-cpp)
- [CachyOS rules](https://github.com/CachyOS/ananicy-rules)
