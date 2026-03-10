# Codex CLI Cheat Codes

Performance-enhancing settings, hidden features, and environment variables for OpenAI Codex CLI.

## Quick Setup

Add to `~/.codex/config.toml`:

```toml
model = "gpt-5.4"
model_reasoning_effort = "high"        # or "xhigh" for hardest problems
model_reasoning_summary = "detailed"
developer_instructions = "Your persistent coding preferences here."

[sandbox_workspace_write]
network_access = true

[features]
unified_exec = true
shell_snapshot = true
apps = true
multi_agent = true
runtime_metrics = true
memories = true
plugins = true
js_repl = true
image_generation = true
prevent_idle_sleep = true
```

## Top Levers (Ranked by Impact)

### 1. Reasoning Effort → Maximum Intelligence

```toml
model_reasoning_effort = "xhigh"    # none|minimal|low|medium|high|xhigh
```

Or per-session: `codex -c model_reasoning_effort='"xhigh"'`

GPT-5.4 supports all levels including `xhigh`. Default is `medium` — you're leaving intelligence on the table.

### 2. Developer Instructions → Persistent System Prompt

```toml
developer_instructions = "Always use ES modules. Never use CommonJS. Prefer simple solutions."
```

Injected into every session automatically. Like CLAUDE.md but for Codex.

### 3. Reasoning Summary → Better Output

```toml
model_reasoning_summary = "detailed"    # auto|concise|detailed|none
```

Controls how much of the model's reasoning chain is surfaced. `detailed` gives you the full picture.

### 4. Performance Profiles → Different Modes

```toml
profile = "deep"    # Default profile at startup

[profiles.deep]
model = "gpt-5.4"
model_reasoning_effort = "xhigh"
model_reasoning_summary = "detailed"
service_tier = "fast"
approval_policy = "never"

[profiles.quick]
model = "gpt-5.1-codex-mini"
model_reasoning_effort = "low"
service_tier = "flex"
approval_policy = "on-request"
```

Switch between profiles for different work types.

### 5. Full Auto Mode → Zero Friction

```toml
approval_policy = "never"
sandbox_mode = "danger-full-access"
```

Or CLI: `codex exec --full-auto`

### 6. Sandbox Network Access

```toml
[sandbox_workspace_write]
network_access = true
```

**Critical**: Without this, sandboxed commands can't hit the network. Needed for npm install, pip install, API calls, etc.

## All 43 Feature Flags

Enable with `codex features enable <flag>` or in `config.toml` under `[features]`.

### Stable (safe to enable)
| Flag | Default | Purpose |
|------|---------|---------|
| `enable_request_compression` | true | zstd compression on API requests |
| `fast_mode` | true | /fast toggle for service tier |
| `personality` | true | Style selection (pragmatic/friendly/none) |
| `shell_tool` | true | Shell command execution |
| `shell_snapshot` | false | **Cache shell environment between commands** |
| `sqlite` | true | SQLite state persistence |
| `undo` | false | Undo support for file changes |
| `unified_exec` | true | PTY-backed exec tool |

### Experimental (worth enabling)
| Flag | Default | Purpose |
|------|---------|---------|
| `js_repl` | false | **JavaScript REPL with dynamic imports** |
| `multi_agent` | false | **Agent spawning and orchestration** |
| `prevent_idle_sleep` | false | Block machine sleep during turns |
| `runtime_metrics` | false | Token/timing metrics display |
| `memories` | false | **Workspace-scoped persistent memory** |
| `plugins` | false | **Full plugin system** |
| `image_generation` | false | **Built-in image generation** |

### Under Development (use at own risk)
| Flag | Default | Purpose |
|------|---------|---------|
| `artifact` | false | Native artifact tools (build/render) |
| `child_agents_md` | false | Append AGENTS.md to sub-agent context |
| `codex_git_commit` | false | Agent-driven git commits |
| `realtime_conversation` | false | Voice/realtime sessions |
| `voice_transcription` | false | Voice-to-text input |
| `apply_patch_freeform` | false | Alternative patch application |

## Environment Variables

### Core
| Variable | Purpose |
|----------|---------|
| `CODEX_HOME` | Override config/state directory (default: `~/.codex`) |
| `OPENAI_API_KEY` | API authentication |
| `OPENAI_BASE_URL` | Override API endpoint |
| `CODEX_STARTING_DIFF` | Pre-load a diff at session start |

### Debug & Development
| Variable | Purpose |
|----------|---------|
| `CODEX_CI` | CI mode flag |
| `CODEX_SQLITE_HOME` | Override SQLite state DB location |
| `CODEX_TUI_RECORD_SESSION` | Record TUI session |
| `CODEX_TUI_SESSION_LOG_PATH` | Session recording path |
| `CODEX_JS_REPL_NODE_PATH` | Custom Node.js for JS REPL |

### Network & Sandbox
| Variable | Purpose |
|----------|---------|
| `CODEX_SANDBOX_NETWORK_DISABLED` | Disable sandbox networking |
| `CODEX_NETWORK_ALLOW_LOCAL_BINDING` | Allow local network binding |
| `HTTP_PROXY` / `HTTPS_PROXY` | Proxy configuration |

## Hidden Subcommands

| Command | Purpose |
|---------|---------|
| `codex app-server` | WebSocket/stdio server for IDE extensions |
| `codex app-server generate-json-schema --out DIR` | Dump full protocol schema (311 definitions) |
| `codex cloud exec --env ENV_ID --attempts N` | Best-of-N cloud execution |
| `codex debug clear-memories` | Reset all saved memory state |
| `codex mcp-server` | Run Codex itself as an MCP server |
| `codex fork` | Fork/branch a previous session |
| `codex sandbox windows` | Run under Windows restricted token |
| `codex features list` | Show all feature flags with status |

## Available Models

| Model | Best For |
|-------|----------|
| `gpt-5.4` | Most powerful, complex reasoning |
| `gpt-5.3-codex` | Strong coding with lower cost |
| `gpt-5.2-codex` | Balanced performance |
| `gpt-5.1-codex-max` | Long context/complex tasks |
| `gpt-5.1-codex-mini` | Fast, cheap, simple tasks |

## Multi-Agent Configuration

```toml
[agents]
max_threads = 6              # Concurrent sub-agents
max_depth = 1                # Nesting depth
job_max_runtime_seconds = 1800   # 30 min timeout per worker

[agents.reviewer]
description = "Performs code review of changes"
config_file = "path/to/reviewer_config.toml"
```

## Shell Environment Security

```toml
[shell_environment_policy]
inherit = "all"                    # all|core|none
ignore_default_excludes = false    # Keep KEY/SECRET/TOKEN filtering
exclude = ["AWS_*", "AZURE_*"]     # Extra exclusions
```

## Config.toml Full Reference

```toml
# Model
model = "gpt-5.4"
model_reasoning_effort = "xhigh"
model_reasoning_summary = "detailed"
model_verbosity = "high"
model_context_window = 1000000
model_auto_compact_token_limit = 800000
model_instructions_file = "path/to/instructions.md"
review_model = "gpt-5.3-codex"

# Automation
approval_policy = "never"
sandbox_mode = "danger-full-access"
developer_instructions = "Your preferences here"

# Notifications
notify = ["python3", "path/to/notify.py"]

# TUI
[tui]
theme = "dracula"
animations = true
alternate_screen = "never"
show_tooltips = false

[history]
persistence = "save-all"
max_bytes = 104857600

# Debug
hide_agent_reasoning = false
show_raw_agent_reasoning = true
```
