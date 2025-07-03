# whodidit – Suspicious File Inspector

`whodidit` is a lightweight Bash CLI tool to scan directories for recently modified files and flag potentially suspicious ones — such as executables, hidden files, or world-writable files.

---

## Why Use whodidit?

Modern Linux environments are filled with config files, shell scripts, executables, and user-created content that change frequently. It's easy to lose track of what’s modified, when, and by whom — especially in shared or developer environments.

`whodidit` helps you monitor file changes and spot red flags quickly:

- Identify files recently modified in any directory
- Detect executables that may have been silently created or altered
- Find world-writable files that could pose security risks
- Highlight hidden dotfiles that could override system behavior

Use it after installing new software, checking USB drives, inspecting your dotfiles, or scanning shared folders. It provides clear, readable output with no dependencies and no overhead.

---

## How It Detects Suspicious Activity

For every file modified within the specified time frame, `whodidit` checks several risk factors:

### 1. Executable Files

If a file has the executable (`x`) permission, it could be a shell script or binary that was just created or altered.

[[ -x "$file" ]]

These are flagged because they may:

• Contain malicious code

• Be used as backdoors

• Replace existing trusted commands

### 2. World-Writable Files
If a file is writable by all users (e.g., chmod 777), it's flagged as insecure.

[[ "$perm" =~ ..7$|.7.|7.. ]]

World-writable files are dangerous because:

•Any local user or process can alter them

•They can be used for privilege escalation

### 3. Hidden Dotfiles
Files starting with . are often used to configure shell behavior (e.g., .bashrc, .profile). If modified recently, they could be used to inject malicious aliases or commands.

[[ "$(basename "$file")" == .* ]]

Output Example

/home/user/.config/autostart.sh
  Owner: user | Modified: 2025-07-02 14:03:44
  Perm: 755 | Type: Bourne-Again shell script
  Suspicious: executable dotfile
  
This layered detection approach helps surface risky or unexpected changes in any folder you choose to inspect.

Features

• Scans for files modified in the last N days

• Shows file owner, permissions, last modified time, and type

• Flags:

  -Executables

  -Dotfiles (hidden)

  -World-writable files

Installation
```bash
git clone https://github.com/cyberknighttron/whodidit-cli.git
cd whodidit-cli
chmod +x whodidit
sudo mv whodidit /usr/local/bin
```
Usage -

whodidit [DIRECTORY] [DAYS]

DIRECTORY — folder to scan (default: current directory)

DAYS — how many days back to look (default: 1)

Examples-

whodidit                  # Scan current folder, last 1 day

whodidit ~/Downloads 3    # Scan Downloads for last 3 days

• Available Flags

Flag	Description -

--help	Show help message

--version	Display tool version
