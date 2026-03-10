# Claude Code Cheat Codes

Performance-enhancing settings, environment variables, and hidden features for Claude Code.

## Quick Setup

Add to `~/.claude/settings.json`:

```json
{
  "effortLevel": "max",
  "env": {
    "ENABLE_TOOL_SEARCH": "auto:0",
    "DISABLE_NON_ESSENTIAL_MODEL_CALLS": "1",
    "CLAUDE_CODE_MAX_OUTPUT_TOKENS": "64000",
    "CLAUDE_AUTOCOMPACT_PCT_OVERRIDE": "80"
  }
}
```

## Top Levers (Ranked by Impact)

### 1. Effort Level → Maximum Intelligence

| Method | Command |
|--------|---------|
| Settings | `"effortLevel": "max"` |
| CLI flag | `claude --effort max` |
| In-session | `/effort max` |
| Env var | `CLAUDE_CODE_EFFORT_LEVEL=max` |

`max` is Opus 4.6 only. Gives highest reasoning with no token constraints.

### 2. Thinking Triggers → Deeper Reasoning

These keywords in your prompt trigger escalating thinking budgets:

| Keyword | Effect |
|---------|--------|
| `think` | Enable extended thinking |
| `think hard` | Higher thinking budget |
| `think harder` / `think very hard` | Near-max |
| **`ultrathink`** | Maximum thinking budget (~32K tokens) |

Works in CLAUDE.md, skill files, and direct prompts.

### 3. Output Length → Complete Responses

```
CLAUDE_CODE_MAX_OUTPUT_TOKENS=64000
```

Default is 32K. Doubles max output for comprehensive code generation.

### 4. Tool Search → Save 30-100K Tokens

```
ENABLE_TOOL_SEARCH=auto:0
```

Lazily loads MCP tool schemas instead of front-loading everything at session start. Critical if you have many MCP servers or plugins.

### 5. Compaction Control → Better Context

```
CLAUDE_AUTOCOMPACT_PCT_OVERRIDE=80
```

Lower = earlier compaction (more headroom). Higher = more context before first compaction. 80 is a good balance.

Manual: `/compact [custom summary instructions]`

### 6. XML Tags in Instructions → Higher Compliance

Claude parses these unambiguously:
```markdown
<instructions>
IMPORTANT: Key directive here
</instructions>

<critical>
CRITICAL: Must-follow rule here
</critical>
```

`IMPORTANT:` and `CRITICAL:` prefixes are genuinely weighted higher in attention.

### 7. Permission Modes → Zero Friction

| Mode | How |
|------|-----|
| Accept edits | `Shift+Tab` to cycle |
| Full bypass | `claude --dangerously-skip-permissions` |
| Settings | `"permissions": { "defaultMode": "bypassPermissions" }` |

### 8. Model Selection

| Alias | Behavior |
|-------|----------|
| `opus` | Most powerful (Opus 4.6) |
| `sonnet` | Fast workhorse (Sonnet 4.6) |
| `haiku` | Cheapest, simple tasks |
| `sonnet[1m]` | Sonnet with 1M context |

Change mid-session: `/model` or `Alt+P`

## Essential Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| **Shift+Tab** | Cycle permission modes |
| **Alt+P** | Switch model |
| **Alt+T** | Toggle thinking |
| **Ctrl+B** | Background task |
| **Ctrl+F** (2x) | Kill all background agents |
| **Ctrl+O** | Toggle verbose |
| **Ctrl+G** | Open prompt in editor |
| **Ctrl+T** | Toggle task list |
| **Esc+Esc** | Rewind/summarize |

## All Environment Variables

### Model & Reasoning
| Variable | Purpose |
|----------|---------|
| `ANTHROPIC_MODEL` | Override default model |
| `CLAUDE_CODE_EFFORT_LEVEL` | `low`/`medium`/`high`/`max` |
| `CLAUDE_CODE_MAX_OUTPUT_TOKENS` | Max output tokens (default 32K) |
| `MAX_THINKING_TOKENS` | Extended thinking budget (default 31999) |
| `CLAUDE_CODE_DISABLE_ADAPTIVE_THINKING` | Use fixed thinking budget |
| `CLAUDE_CODE_SUBAGENT_MODEL` | Force model for sub-agents |

### Context & Compaction
| Variable | Purpose |
|----------|---------|
| `CLAUDE_AUTOCOMPACT_PCT_OVERRIDE` | When compaction fires (1-100%) |
| `DISABLE_COMPACT` | Disable all compaction |
| `DISABLE_AUTO_COMPACT` | Disable auto-compaction only |
| `CLAUDE_CODE_FILE_READ_MAX_OUTPUT_TOKENS` | Max tokens for file reads |

### Feature Toggles
| Variable | Purpose |
|----------|---------|
| `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS` | Multi-agent orchestration |
| `ENABLE_LSP_TOOL` | Language Server Protocol |
| `ENABLE_SESSION_BACKGROUNDING` | Ctrl+B backgrounding |
| `CLAUDE_CODE_SIMPLE` | Minimal mode (no MCP, hooks, CLAUDE.md) |
| `DISABLE_NON_ESSENTIAL_MODEL_CALLS` | Reduce background token usage |
| `ENABLE_TOOL_SEARCH` | Lazy MCP tool loading |

### Shell & Bash
| Variable | Purpose |
|----------|---------|
| `BASH_MAX_OUTPUT_LENGTH` | Max bash output chars (default 30K) |
| `BASH_DEFAULT_TIMEOUT_MS` | Default bash timeout |
| `CLAUDE_CODE_SHELL` | Override shell detection |
| `CLAUDE_BASH_MAINTAIN_PROJECT_WORKING_DIR` | Reset cwd after each command |

### API & Auth
| Variable | Purpose |
|----------|---------|
| `ANTHROPIC_API_KEY` | Direct API key |
| `ANTHROPIC_BASE_URL` | Custom API endpoint |
| `ANTHROPIC_BETAS` | Beta feature headers |
| `CLAUDE_CODE_EXTRA_BODY` | Additional JSON for API bodies |
| `API_TIMEOUT_MS` | Request timeout |

## CLAUDE.md Best Practices

1. **Keep it short.** Instruction-following quality decreases with length
2. **Use XML tags** (`<instructions>`, `<critical>`) for unambiguous parsing
3. **Use `IMPORTANT:` prefix** for must-follow directives — genuinely weighted higher
4. **Put critical rules at the very beginning and very end** — Claude biases toward periphery
5. **Don't duplicate what linters do** — use hooks for deterministic enforcement
6. **Convert repeated instructions into hooks** — hooks run every time, CLAUDE.md is advisory

## Advanced: System Prompt Patching

```bash
npx tweakcc
```

Extracts and lets you edit Claude Code's ~40 internal system prompt sections. Nuclear option for total control.

## Sources

- [390+ Env Vars Gist](https://gist.github.com/unkn0wncode/f87295d055dd0f0e8082358a0b5cc467)
- [165 Env Vars in v2.1.69](https://www.turboai.dev/blog/claude-code-env-vars-v2-1-69)
- [Claude Code Internals](https://github.com/eran-broder/claude-code-internals)
- [System Prompt Tracker](https://github.com/Piebald-AI/claude-code-system-prompts)
- [CLAUDE.md Optimization (+10% SWE Bench)](https://arize.com/blog/claude-md-best-practices-learned-from-optimizing-claude-code-with-prompt-learning/)
- [Hidden Multi-Agent System](https://paddo.dev/blog/claude-code-hidden-swarm/)
- [Hidden MCP Flag](https://paddo.dev/blog/claude-code-hidden-mcp-flag/)
