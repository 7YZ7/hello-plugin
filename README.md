# hello-plugin

A minimal Claude Code plugin that bundles the usual component types for learning plugin development.

## Components

| Component | Location | Description |
|-----------|----------|-------------|
| Agent | `agents/hello-agent.md` | Placeholder agent that greets the user |
| Skill | `skills/hello-skill/SKILL.md` | Placeholder greeting skill |
| Skill (extra) | `skills/hello-ag-skill/skillag.md` | Additional sample skill folder |
| Hook | `hooks/hooks.json` + `hooks/on-prompt.sh` | `UserPromptSubmit`: log prompt, optional git commit/push |
| Rule | `rules/hello-rule.md` | General placeholder guidelines |
| Command | `commands/hello.md` | `/hello` slash command |

## Directory structure

```
hello-plugin/
  .claude-plugin/
    plugin.json          # Manifest (agents, commands, skills, rules)
    marketplace.json     # Marketplace metadata
  agents/
    hello-agent.md
  skills/
    hello-skill/
      SKILL.md
    hello-ag-skill/
      skillag.md
  hooks/
    hooks.json           # Hook events (auto-loaded; do not duplicate in plugin.json)
    on-prompt.sh         # UserPromptSubmit script
  rules/
    hello-rule.md
  commands/
    hello.md
  logs/                  # Created by the hook (gitignored or committed per your choice)
    <username>-input.log # One file per OS user (e.g. Xiyao_Meng-input.log)
```

## Installation

```bash
claude plugin install /path/to/hello-plugin
```

## Hooks and `plugin.json`

Claude Code **automatically** loads `hooks/hooks.json` at the plugin root. Do **not** add a `hooks` field in `plugin.json` that points at that same file, or you will get a **Duplicate hooks file** error. Use `plugin.json` → `hooks` only for **extra** hook JSON files (for example `./config/more-hooks.json`).

The hook command uses **`${CLAUDE_PLUGIN_ROOT}`** so the script path works after the plugin is installed from any location. The shell script resolves the plugin root from its own path (`BASH_SOURCE`) so logging and `git` run against the installed plugin directory, not the arbitrary process working directory.

## Hook behavior

On every user prompt (`UserPromptSubmit`):

1. Prints `[hello-plugin] this is hello-hacker` to **stderr** (visible in the Claude Code TUI).
2. Parses the hook JSON on stdin and appends a timestamped line to **`logs/<username>-input.log`** under the plugin root.
3. From that same root, runs `git add` on that log file, then **commit** and **`git push origin main`** if there are staged changes. Failures are ignored so the session is not blocked.

Requires **bash** (e.g. Git Bash on Windows) and **Python** (`python3` or `python`) for JSON parsing, with a **grep** fallback.

## Usage

```
/hello    # Show plugin status and component list
```

## Repository

Upstream example: [hello-plugin on GitHub](https://github.com/7YZ7/hello-plugin).
