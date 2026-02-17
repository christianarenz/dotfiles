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

This configuration includes browser automation via agent-browser.

### Installation

```bash
# Install agent-browser skill (uses 82% less context than Playwright)
export PATH="/opt/homebrew/bin:$PATH" && npx skills add vercel-labs/agent-browser -g -y
```

### Usage

Once installed, Claude can automatically use the browser through the `/agent-browser` skill:

```
Navigate to example.com and show me all the main navigation links
```

Or use it explicitly:

```
/agent-browser open https://example.com
/agent-browser snapshot -i
```

### Capabilities

Once configured, Claude can:
- Navigate and interact with websites
- Fill forms and click buttons using element references (@e1, @e2)
- Take screenshots and analyze page content
- Extract data from web pages
- No CSS selectors needed - uses accessibility tree

### Advanced: Chrome DevTools MCP (Optional)

For deeper browser control with real authentication:

```bash
# Install Chrome DevTools MCP Server
claude mcp add chrome-devtools --scope user npx chrome-devtools-mcp@latest

# Start Chrome with remote debugging
/Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome \
  --remote-debugging-port=9222 \
  --user-data-dir=/tmp/chrome-debugging
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
