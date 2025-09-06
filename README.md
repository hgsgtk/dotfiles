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

### Avoiding Git Diffs

To prevent `.chezmoidata.yaml` from causing git diffs between machines:

1. **Use `.chezmoiignore`** (recommended): The `.chezmoiignore` file excludes `.chezmoidata.yaml` from git tracking
2. **Use environment variables**: Set `GIT_USER_NAME` and `GIT_USER_EMAIL` environment variables
3. **Use the template**: Copy `chezmoidata.yaml.tmpl` to `.chezmoidata.yaml` and customize

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

### Using Environment Variables

Instead of editing `.chezmoidata.yaml`, you can set environment variables:

```bash
# Set in your shell profile (~/.zshrc, ~/.bashrc, etc.)
export GIT_USER_NAME="Your Name"
export GIT_USER_EMAIL="your.email@example.com"
```

This approach works automatically without needing to edit any files.

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
