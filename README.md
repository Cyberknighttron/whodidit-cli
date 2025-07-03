# whodidit – Suspicious File Inspector

`whodidit` is a lightweight Bash CLI tool to scan directories for recently modified files and flag potentially suspicious ones — like executables, hidden files, or world-writable files.

---

## Features

- ✅ Scan files modified in the last **N days**
- ✅ Show:
  - Owner
  - Last modified date
  - Permissions
  - File type
- ⚠️ Flags:
  - Executables
  - Dotfiles (hidden)
  - World-writable files

---

## Installation

```bash
git clone https://github.com/cyberknighttron/whodidit-cli.git
cd whodidit-cli
chmod +x whodidit
sudo mv whodidit /usr/local/bin
