# Dotfiles

Personal dotfiles managed with [chezmoi](https://www.chezmoi.io/) - a secure dotfile manager that handles configuration files across multiple machines.

## What's included

This repository contains configuration files and setup scripts for macOS development environment, including:

- Shell configuration (zsh, bash)
- Git configuration
- Editor configurations
- Application settings
- Installation scripts for development tools

## Quick Start

### Install chezmoi and apply dotfiles

On a new machine, install chezmoi and apply these dotfiles with a single command:

```bash
sh -c "$(curl -fsLS get.chezmoi.io)" -- init --apply hgsgtk
```

### Update dotfiles

To update your dotfiles on any machine:

```bash
chezmoi update
```

## Manual Installation

If you prefer to install chezmoi manually:

```bash
# Install chezmoi (choose your preferred method)
# macOS with Homebrew:
brew install chezmoi

# Or download binary:
curl -sfL https://git.io/chezmoi | sh

# Initialize and apply dotfiles
chezmoi init hgsgtk
chezmoi apply
```

## Daily Usage

- `chezmoi status` - Check status of your dotfiles
- `chezmoi diff` - See what changes would be made
- `chezmoi apply` - Apply changes to your dotfiles
- `chezmoi edit <file>` - Edit a dotfile
- `chezmoi add <file>` - Add a new file to be managed

## Git Configuration Customization

This dotfiles repository includes a flexible Git configuration system that automatically adapts to different machines while allowing manual customization.

### Automatic Configuration

The Git configuration uses chezmoi templating to automatically adapt to each machine:

- **Username**: Automatically detected from the system
- **Email**: Uses default from `.chezmoidata.yaml` or can be overridden
- **excludesfile**: Automatically uses `/Users/{username}/.gitignore_global`

### Machine-Specific Customization

To customize Git settings for a specific machine, edit `.chezmoidata.yaml`:

```yaml
git:
  name: "Your Name"
  email: "your.email@company.com"
  editor: "code"  # or "vim", "nano", etc.
  excludesfile: "/Users/yourusername/.gitignore_global"
  ghqRoot: "~/src"  # or "~/repos", "~/code", etc.
  hubProtocol: "https"  # or "ssh"
```

### Popular ghq Root Directories

The `ghq` tool manages repository cloning. Popular root directory choices:

- `~/ghq` - Default
- `~/src` - Clean and simple
- `~/repos` - General repositories
- `~/go/src` - Go development (current default)
- `~/code` - Alternative clean option
- `~/projects` - Descriptive organization

### Git Aliases Included

Useful Git aliases are pre-configured:

- `st` = status
- `co` = checkout (legacy)
- `sw` = switch (modern)
- `br` = branch
- `ci` = commit
- `see` = browse (opens repository in browser)
- `lg` = pretty log graph
- `uncommit` = undo last commit
- `amend` = amend without editing
- `cleanup` = delete merged branches

### Examples

**Personal Machine:**
```yaml
git:
  name: "hgsgtk"
  email: "hgsgtk@gmail.com"
  ghqRoot: "~/go/src"
```

**Work Machine:**
```yaml
git:
  name: "Your Name"
  email: "your.email@company.com"
  ghqRoot: "~/work/repos"
  excludesfile: "/Users/workuser/.gitignore_work"
```

**Custom Setup:**
```yaml
git:
  excludesfile: "/Users/dev/.config/git/ignore"
  ghqRoot: "~/development"
```

## About chezmoi

chezmoi is a dotfile manager that provides:

- **Templates** - Handle differences between machines
- **Password manager support** - Store secrets securely
- **File encryption** - Using gpg or age
- **Script execution** - Handle complex setup tasks
- **Cross-platform** - Works on Linux, macOS, and Windows

For more information, visit [chezmoi.io](https://www.chezmoi.io/).

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
