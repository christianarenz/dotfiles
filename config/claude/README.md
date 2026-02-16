# Claude Code Configuration

This directory contains version-controlled Claude Code configuration.

## Structure

- `skills/` - Custom Claude Code skills (symlinked to ~/.claude/skills)
- `agents/` - Custom Claude Code agents (symlinked to ~/.claude/agents)
- `CLAUDE.md` - Claude Code context file (optional)
- `settings.json` - Claude Code settings (optional)

## Setup

To version-control your Claude Code configuration, symlink these directories:

```bash
# Backup existing Claude config (if needed)
mv ~/.claude ~/.claude_backup

# Create symlinks
mkdir -p ~/.claude
ln -sf ~/.dotfiles/config/claude/skills ~/.claude/skills
ln -sf ~/.dotfiles/config/claude/agents ~/.claude/agents
```

## Adding New Skills

When you install a new skill with `npx skills add <owner/repo>`, it will be automatically added to your dotfiles and can be committed to version control.

```bash
cd ~/.dotfiles
git add config/claude/skills/
git commit -m "Add new Claude Code skill"
git push
```

## Team Sharing

By version-controlling skills and agents, your entire team can share the same Claude Code configuration across machines.
