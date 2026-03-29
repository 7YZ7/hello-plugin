# hello-plugin

A minimal Claude Code plugin containing all five component types. Built for learning plugin development.

## Components

| Component | File | Description |
|-----------|------|-------------|
| Agent | `agents/hello-agent.md` | Placeholder agent that greets the user |
| Skill | `skills/hello-skill/SKILL.md` | Placeholder greeting skill |
| Hook | `hooks/hooks.json` + `hooks/on-prompt.sh` | Logs every user input to `logs/input.log` and pushes to this repo |
| Rule | `rules/hello-rule.md` | General placeholder guidelines |
| Command | `commands/hello.md` | `/hello` slash command |

## Directory Structure

```
hello-plugin/
  .claude-plugin/
    plugin.json          # Plugin manifest
    marketplace.json     # Marketplace metadata
  agents/
    hello-agent.md
  skills/
    hello-skill/
      SKILL.md
    hello-ag-skill/
      skillag.md
  hooks/
    hooks.json           # Hook event config
    on-prompt.sh         # Hook script
  rules/
    hello-rule.md
  commands/
    hello.md
  logs/
    input.log            # Auto-generated; appended by hook on every user prompt
```

## Installation

```bash
claude plugin install /path/to/hello-plugin
```

## Hook Behavior

Every time you submit a prompt in Claude Code:
1. Outputs `this is hello-hacker` to the terminal
2. Appends a timestamped line to `logs/input.log`
3. Commits and pushes the log to `origin main`

Remote: `https://github.com/7YZ7/hello-plugin/tree/main/.claude-plugin`

## Usage

```
/hello    # Show plugin status and component list
```
