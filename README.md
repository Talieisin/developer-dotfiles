# Talieisin Developer Dotfiles

Chezmoi-managed dotfiles templates for Talieisin developer onboarding.

## Quick Start

### New Machine Setup (One Command)

```bash
# Install chezmoi and apply these dotfiles
sh -c "$(curl -fsLS get.chezmoi.io)" -- init --apply Talieisin/developer-dotfiles
```

### If Chezmoi is Already Installed

```bash
chezmoi init --apply Talieisin/developer-dotfiles
```

## What's Included

| File | Destination | Description |
|------|-------------|-------------|
| `dot_zshrc.tmpl` | `~/.zshrc` | Zsh config with mise, Homebrew, OrbStack |
| `dot_gitconfig.tmpl` | `~/.gitconfig` | Git config with conditional identity includes |
| `dot_gitconfig-work.tmpl` | `~/.gitconfig-work` | Work identity (Talieisin email) |
| `dot_gitconfig-personal.tmpl` | `~/.gitconfig-personal` | Personal identity |
| `dot_gitignore_global` | `~/.gitignore_global` | Global git ignores (personal artefacts only) |
| `dot_config/mise/config.toml.tmpl` | `~/.config/mise/config.toml` | Runtime version defaults |

## Configuration

During `chezmoi init`, you'll be prompted for:
- Your name
- Work email (defaults to username@talieisin.com)
- Personal email
- Editor preference (nano, nvim, vim, code)
- GPG keys (optional)

Edit your config anytime:
```bash
chezmoi edit-config
```

## Usage Patterns

### Option A: Use as Starting Point (Recommended)

1. Fork this repository to your personal GitHub
2. Initialise from your fork:
   ```bash
   chezmoi init --apply YOUR_USERNAME/developer-dotfiles
   ```
3. Customise to your preferences
4. Push changes to your fork

### Option B: Use Directly (Read-Only)

```bash
chezmoi init --apply Talieisin/developer-dotfiles
```

Note: Changes you make locally won't sync back to this repository.

### Option C: One-Shot Mode (Temporary Environments)

For containers or VMs where you don't need persistent chezmoi:
```bash
sh -c "$(curl -fsLS get.chezmoi.io)" -- init --one-shot Talieisin/developer-dotfiles
```

## Daily Workflow

```bash
# Edit a dotfile
chezmoi edit ~/.zshrc

# Preview changes
chezmoi diff

# Apply changes
chezmoi apply

# Commit to your fork
chezmoi cd
git add . && git commit -m "Update zshrc" && git push
```

## Organisational Defaults

### Shell Setup
- mise activation for runtime management
- Homebrew shellenv (Apple Silicon and Intel)
- OrbStack CLI integration
- zsh-syntax-highlighting and zsh-autosuggestions (if installed)

### Git Configuration
- Conditional includes for work/personal identity
- Credential helpers (macOS Keychain, GitHub CLI)
- Useful aliases (lg, st, cleanup, etc.)

### Runtime Versions (mise)
- Node.js LTS
- Python 3.13
- Go latest
- Rust latest

## Customisation Tips

### Adding Your Own Files

```bash
# Add an existing file to chezmoi management
chezmoi add ~/.bashrc

# Create a new template
chezmoi edit ~/.config/starship.toml
```

### Machine-Specific Configuration

Create `~/.zshrc.local` for machine-specific settings (automatically sourced).

## Security

- Store secrets in 1Password or macOS Keychain
- Use `private_` prefix for sensitive files
- Never commit API keys or tokens

## Contributing

This repository provides organisational defaults. For personal customisations, fork and maintain your own copy.

## Resources

- [Chezmoi Documentation](https://www.chezmoi.io/)
- [Talieisin Engineering Slack](#engineering)

---

**Maintained By**: Talieisin IT Team
