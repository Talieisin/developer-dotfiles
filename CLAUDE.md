# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

Chezmoi-managed dotfiles templates for Talieisin developer onboarding. This is a template repository that developers use to bootstrap their development environment.

## Key Commands

```bash
# Test templates locally (renders templates without applying)
chezmoi execute-template < dot_zshrc.tmpl

# Preview what would be installed
chezmoi init --apply --dry-run .

# Apply locally for testing
chezmoi apply --source=.

# Validate template syntax (all .tmpl files should render without error)
chezmoi execute-template --init < .chezmoi.toml.tmpl
```

## Architecture

### File Naming Convention (Chezmoi)

- `dot_` prefix → installed as `.` (e.g., `dot_zshrc.tmpl` → `~/.zshrc`)
- `.tmpl` suffix → processed as Go template with chezmoi data
- `private_` prefix → installed with 0600 permissions
- Directory structure mirrors target: `dot_config/mise/` → `~/.config/mise/`

### Template Variables

Defined in `.chezmoi.toml.tmpl`, available in all `.tmpl` files:
- `.name`, `.email`, `.personal_email` - user identity
- `.editor` - preferred editor (nano/nvim/vim/code)
- `.work_gpg_key`, `.personal_gpg_key` - optional GPG signing keys
- `.chezmoi.os`, `.chezmoi.arch` - platform detection (darwin/linux, arm64/amd64)

### Git Identity Pattern

Uses conditional includes based on directory paths:
- `~/Projects/Talieisin/`, `~/work/` → work identity (`.gitconfig-work`)
- `~/Projects/personal/`, `~/personal/` → personal identity (`.gitconfig-personal`)

No default `[user]` section - forces explicit configuration per directory to prevent identity mistakes.

## Editing Guidelines

- Templates use Go text/template syntax with chezmoi functions
- Platform-specific blocks use `{{- if eq .chezmoi.os "darwin" }}...{{- end }}`
- Always test template rendering before committing
- Keep organisational defaults in clearly marked sections; personal customisation sections below
