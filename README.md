# NT Password Editor - Refreshed Edition

[![License: GPL v2](https://img.shields.io/badge/License-GPL%20v2-blue.svg)](https://www.gnu.org/licenses/old-licenses/gpl-2.0.en.html)
[![License: LGPL v2.1](https://img.shields.io/badge/License-LGPL%20v2.1-blue.svg)](https://www.gnu.org/licenses/lgpl-2.1)

A modernized version of the classic Offline NT Password Editor, originally created by Petter Nordahl-Hagen (1997-2014). This refreshed edition brings the tool into 2025 with enhanced security, modern build systems, and support for Windows 10/11.

## Overview

The NT Password Editor is a suite of tools that enables viewing and modifying user passwords, group memberships, and registry data in Windows NT/XP/Vista/7/8/10/11 SAM (Security Account Manager) database files. The tools work offline, meaning you don't need to know the original passwords to reset them.

### Key Features

- **Password Reset**: Reset user passwords without knowing the original
- **User Management**: View and modify user accounts and group memberships
- **Registry Editing**: Full read/write support for Windows registry hives
- **Import/Export**: Support for .reg file import and export
- **Cross-Platform**: Runs on Linux and other Unix-like systems
- **Scriptable**: Command-line tools for automation

## What's New in 2025+

This refreshed version addresses the limitations of the original codebase:

### Security Improvements
- ✅ **Buffer Overflow Fixes**: Eliminated known buffer overflow vulnerabilities
- ✅ **Memory Safety**: Enhanced memory management and bounds checking
- ✅ **Input Validation**: Strengthened input validation across all tools

### Modern Build System
- ✅ **Autotools Integration**: Standard `autoconf`/`automake` build system
- ✅ **Package Management**: Better integration with modern package managers
- ✅ **Cross-Platform Builds**: Improved compilation across different platforms

### Enhanced Compatibility
- ✅ **Windows 10/11 Support**: Updated SAM and registry format support
- ✅ **Dynamic Linking**: Removed static OpenSSL dependencies
- ✅ **Modern Crypto**: Updated cryptographic implementations

### Developer Experience
- ✅ **GitHub Workflow**: Modern CI/CD, issue tracking, and collaboration
- ✅ **Documentation**: Comprehensive documentation and examples
- ✅ **Testing**: Automated testing suite for reliability

## Tools Included

| Tool | Purpose | License |
|------|---------|---------|
| `chntpw` | Interactive password reset and registry editor | GPL v2 |
| `reged` | Registry editor with import/export capabilities | GPL v2 |
| `sampasswd` | Command-line password reset tool | GPL v2 |
| `samusrgrp` | Command-line user/group management tool | GPL v2 |
| `ntreg` | Registry manipulation library | LGPL v2.1 |
| `libsam` | SAM database manipulation library | LGPL v2.1 |

## Installation

### From Source

```bash
git clone https://github.com/jfstenuit/chntpw.git
cd chntpw
./autogen.sh
./configure
make
sudo make install
```

### Dependencies

- OpenSSL development libraries
- Standard C development tools
- Autotools (autoconf, automake, libtool)

### Package Managers

```bash
# Ubuntu/Debian
sudo apt-get install chntpw

# Fedora/RHEL
sudo dnf install chntpw

# Arch Linux
pacman -S chntpw
```

## Quick Start

### Reset a Windows Password

1. Boot from a Linux live CD/USB
2. Mount the Windows partition
3. Locate the SAM file (usually at `Windows/System32/config/SAM`)
4. Run the password reset tool:

```bash
sudo chntpw /mnt/windows/Windows/System32/config/SAM
```

### Script-Based Password Reset

```bash
# List all users
sampasswd -l /path/to/SAM

# Reset password for specific user
sampasswd -u Administrator -p newpassword /path/to/SAM
```

### Registry Editing

```bash
# Interactive registry editor
reged -e /path/to/registry/hive

# Import .reg file
reged -I registry_export.reg /path/to/hive

# Export to .reg file
reged -x /path/to/hive registry_export.reg
```

## Usage Examples

### Interactive Mode

```bash
# Start interactive session
sudo chntpw -i /mnt/windows/Windows/System32/config/SAM

# Follow the menu prompts to:
# 1. List users
# 2. Reset passwords
# 3. Promote users to administrators
# 4. Edit registry values
```

### Automation Scripts

```bash
#!/bin/bash
# Batch password reset script

SAMFILE="/mnt/windows/Windows/System32/config/SAM"

# Reset administrator password
sampasswd -u Administrator -p "" "$SAMFILE"

# Add user to administrators group
samusrgrp -a -u john -g Administrators "$SAMFILE"
```

## Supported Windows Versions

| Version | SAM Support | Registry Support | Notes |
|---------|-------------|------------------|-------|
| Windows NT 3.51 | ✅ | ✅ | Full support |
| Windows NT 4.0 | ✅ | ✅ | Full support |
| Windows 2000 | ✅ | ✅ | Full support |
| Windows XP | ✅ | ✅ | Full support |
| Windows Vista | ✅ | ✅ | Password blanking recommended |
| Windows 7 | ✅ | ✅ | Full support |
| Windows 8/8.1 | ✅ | ✅ | Full support |
| Windows 10 | ✅ | ✅ | **New in 2025** |
| Windows 11 | ✅ | ✅ | **New in 2025** |

## Security Considerations

### ⚠️ Important Warnings

- **Backup First**: Always backup registry files before making changes
- **Syskey Limitations**: Tools may not work with syskey-protected systems
- **Domain Accounts**: Limited support for domain-joined machines
- **BitLocker**: Decrypt drives before using these tools

### Best Practices

1. Use password blanking (empty password) rather than setting new passwords
2. Test changes in a virtual machine first
3. Keep rescue media handy
4. Document any changes made

## Contributing

We welcome contributions! Please see our [Contributing Guide](CONTRIBUTING.md) for details.

### Development Setup

```bash
git clone https://github.com/jfstenuit/chntpw.git
cd chntpw
./autogen.sh
./configure --enable-debug
make
```

### Running Tests

```bash
make check
```

## License

This project maintains the original dual-license structure:

- **Registry/SAM Libraries** (`ntreg`, `libsam`): [LGPL v2.1](LICENSE.LGPL)
- **User Tools** (`chntpw`, `reged`, `sampasswd`, `samusrgrp`): [GPL v2](LICENSE.GPL)

## History & Evolution

### Original Development (1997-2014)
Created by Petter Nordahl-Hagen, the original NT Password Editor was a groundbreaking tool that enabled offline Windows password recovery when few alternatives existed.

### Refreshed Edition (2025+)
This modernized version addresses security vulnerabilities, adds Windows 10/11 support, and brings the codebase up to contemporary standards while maintaining compatibility with the original tool's functionality.

For detailed version history, see [HISTORY.md](HISTORY.md).

## Documentation

- [Manual](docs/MANUAL.md) - Detailed usage instructions
- [Technical Details](docs/TECHNICAL.md) - Registry and SAM structure information
- [Build Instructions](docs/BUILDING.md) - Compilation and installation
- [FAQ](docs/FAQ.md) - Frequently asked questions
- [Migration Guide](docs/MIGRATION.md) - Upgrading from original version

## Support

- 🐛 [Issue Tracker](https://github.com/jfstenuit/chntpw/issues)
- 📖 [Documentation](https://github.com/jfstenuit/chntpw/wiki)
- 💬 [Discussions](https://github.com/jfstenuit/chntpw/discussions)

## Acknowledgments

- **Petter Nordahl-Hagen** - Original creator and maintainer (1997-2014)
- **Contributors** - All who helped improve and maintain this project
- **Community** - Users who provided feedback, bug reports, and testing

---

**Note**: This tool is intended for legitimate system administration and recovery purposes. Users are responsible for complying with applicable laws and organizational policies.