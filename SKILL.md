---
name: mole
description: Install and use Mole (mo) - a powerful macOS system cleaning and optimization CLI tool. Use when the user needs to clean caches, uninstall apps completely, analyze disk usage, optimize system performance, purge build artifacts, or monitor system health on macOS. Handles installation via Homebrew or install script, and all Mole commands including clean, uninstall, optimize, analyze, status, purge, and installer cleanup. ALWAYS uses dry-run first for destructive operations, asks for user approval, then executes.
---

# Mole Skill

Mole (`mo`) is a comprehensive macOS system cleaning and optimization tool that combines features of CleanMyMac, AppCleaner, DaisyDisk, and iStat Menus into a single binary.

## Safety-First Workflow (REQUIRED)

For ALL destructive operations (clean, uninstall, purge, installer), you MUST follow this workflow:

1. **DRY-RUN FIRST:** Always run with `--dry-run` to preview what will happen
2. **SHOW PREVIEW:** Present the dry-run output to the user clearly
3. **ASK FOR APPROVAL:** Wait for explicit user confirmation before proceeding
4. **EXECUTE:** Only then run the actual command without `--dry-run`

**Never skip the dry-run step for destructive operations.**

## Installation

### Via Homebrew (Recommended)

```bash
brew install mole
```

### Via Install Script

```bash
# Latest stable release
curl -fsSL https://raw.githubusercontent.com/tw93/mole/main/install.sh | bash

# Latest main branch
curl -fsSL https://raw.githubusercontent.com/tw93/mole/main/install.sh | bash -s -- -s latest

# Specific version
curl -fsSL https://raw.githubusercontent.com/tw93/mole/main/install.sh | bash -s -- -s 1.17.0
```

## Quick Commands

```bash
mo                    # Interactive menu
mo clean              # Deep cleanup caches, logs, browser data
mo uninstall          # Smart app uninstaller (removes leftovers)
mo optimize           # Refresh caches & system services
mo analyze            # Visual disk explorer
mo status             # Live system health dashboard
mo purge              # Clean project build artifacts (node_modules, etc.)
mo installer          # Find and remove installer files
mo touchid            # Configure Touch ID for sudo
mo completion         # Set up shell tab completion
mo update             # Update Mole
mo remove             # Remove Mole from system
mo --help             # Show help
mo --version          # Show installed version
```

## Command Details

### Deep System Cleanup

**WORKFLOW:**
1. Run `mo clean --dry-run` to preview
2. Show output to user
3. Ask: "Proceed with cleanup? (yes/no)"
4. If yes: Run `mo clean`

```bash
# Step 1: Preview (ALWAYS do this first)
mo clean --dry-run

# Step 4: Execute (only after user approval)
mo clean
```

**What gets cleaned:**
- User app caches
- Browser caches (Chrome, Safari, Firefox)
- Developer tools (Xcode, Node.js, npm)
- System logs and temp files
- App-specific caches (Spotify, Dropbox, Slack)
- Trash

**Additional options:**
```bash
mo clean --whitelist        # Manage protected caches
mo clean --dry-run --debug  # Detailed preview with risk levels
```

### Smart App Uninstaller

**WORKFLOW:**
1. Run `mo uninstall` (interactive - shows what will be removed)
2. Present the list of apps and files to be removed
3. Ask: "Proceed with uninstallation? (yes/no)"
4. If yes: User confirms in the interactive UI

```bash
mo uninstall                # Interactive uninstaller
```

### System Optimization

**WORKFLOW:**
1. Run `mo optimize --dry-run` to preview
2. Show output to user
3. Ask: "Proceed with optimization? (yes/no)"
4. If yes: Run `mo optimize`

```bash
# Step 1: Preview
mo optimize --dry-run

# Step 4: Execute
mo optimize
```

**What gets optimized:**
- Rebuild system databases and clear caches
- Reset network services
- Refresh Finder and Dock
- Clean diagnostic and crash logs
- Remove swap files and restart dynamic pager
- Rebuild launch services and spotlight index

### Disk Space Analyzer

Safe/non-destructive - no dry-run needed.

```bash
mo analyze                  # Analyze home directory
mo analyze /Volumes         # Analyze external drives
mo analyze ~/Documents      # Analyze specific path
```

**Navigation:**
- `↑↓←→` or `h/j/k/l` - Navigate
- `o` - Open directory
- `f` - Show in Finder
- `⌫` - Delete item (will ask for confirmation)
- `l` - Show large files only
- `q` - Quit

### Live System Status

Safe/non-destructive - read-only dashboard.

```bash
mo status                   # Live system dashboard
```

**Shortcuts:**
- `k` - Toggle cat visibility
- `q` - Quit

### Project Artifact Purge

**WORKFLOW:**
1. Run `mo purge` to see the interactive list
2. Present what will be removed (projects, sizes)
3. Ask: "Proceed with purging selected artifacts? (yes/no)"
4. If yes: User confirms in the interactive UI

```bash
mo purge                    # Interactive purge
mo purge --paths            # Configure scan directories
```

**Configure custom paths:**
```bash
# Edit ~/.config/mole/purge_paths
echo "~/Documents/MyProjects" >> ~/.config/mole/purge_paths
echo "~/Work/ClientA" >> ~/.config/mole/purge_paths
```

**Note:** Recent projects (< 7 days) are marked and unselected by default.

### Installer Cleanup

**WORKFLOW:**
1. Run `mo installer` to see the interactive list
2. Present what will be removed (installers, sizes, locations)
3. Ask: "Proceed with removing selected installers? (yes/no)"
4. If yes: User confirms in the interactive UI

```bash
mo installer                # Interactive installer cleanup
```

## Safety Features

- **Dry-run mode:** Preview all changes before executing with `--dry-run`
- **Whitelist:** Protect specific paths from cleanup with `--whitelist`
- **Operation log:** All file operations logged to `~/.config/mole/operations.log`
- **Recent project protection:** Recent projects are unselected by default in purge
- **User confirmation:** Always ask before destructive operations

## Environment Variables

```bash
MO_NO_OPLOG=1               # Disable operation logging
MO_LAUNCHER_APP=<name>      # Override terminal app detection
```

## Quick Launchers (Raycast/Alfred)

Set up quick launchers for instant access:

```bash
curl -fsSL https://raw.githubusercontent.com/tw93/Mole/main/scripts/setup-quick-launchers.sh | bash
```

Then add `~/Library/Application Support/Raycast/script-commands` to Raycast's Script Commands directories.

## Terminal Compatibility

Recommended terminals:
- ✅ Alacritty
- ✅ Kitty
- ✅ WezTerm
- ✅ Ghostty
- ✅ Warp
- ⚠️ iTerm2 (known compatibility issues)

## Troubleshooting

**Operation logs:**
```bash
cat ~/.config/mole/operations.log
```

**Debug mode:**
```bash
mo <command> --debug
```

**Reinstall:**
```bash
mo remove && brew install mole
```
