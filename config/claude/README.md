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
ln -sf ~/.dotfiles/config/claude/settings.json ~/.claude/settings.json
```

## Browser Automation Setup

This configuration includes Chrome DevTools MCP for browser automation.

### Installation

```bash
# 1. Install Chrome DevTools MCP Server
claude mcp add chrome-devtools --scope user npx chrome-devtools-mcp@latest

# 2. Install browser agent skill (optional)
npx skills add -g agent-browser
```

### Usage

Start Chrome with remote debugging:

```bash
# Recommended: Separate profile for security
/Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome \
  --remote-debugging-port=9222 \
  --user-data-dir=/tmp/chrome-debugging

# Or use your main profile (Claude has access to all logins!)
/Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome \
  --remote-debugging-port=9222
```

### Capabilities

Once configured, Claude can:
- Navigate and interact with websites
- Fill forms and click buttons
- Execute authenticated actions (using your real cookies/sessions)
- Inspect DOM and run JavaScript
- Collect performance metrics

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
