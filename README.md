# Superskills

A few skills I wrote for Claude Code and Codex to make long, autonomous build
sessions go better. They're prompt files, not software — copy them into your
skills directory and invoke them by name.

## The skills

### `/genesis` — build something start to finish

You say "go" and it researches an idea, picks one, builds it with parallel
agents, runs an adversarial review pass, scores the result, and hands you a list
of things to test. The idea is to flip who does what: it builds and owns the
decisions, you test and push back.

### `/production-autopilot` — a long hardening pass

Meant to run for a couple of hours rather than a couple of minutes:

- Research — related papers, existing tools, dependency and competitor checks
- Engineering — build, types, lint, tests, security, code review
- Experience — can someone non-technical actually use it? Full user journeys
- Adversary — a skeptic pass that argues the thing isn't good enough
- Loop — repeats until every phase comes back clean in the same cycle

### `/rubric` — a scoring checklist

Ten dimensions, scored with evidence rather than impressions. Anything below 7
means not ready.

| Dimension | What it asks |
|-----------|--------------|
| WORKS | Does it function, including the edge cases? |
| OBVIOUS | Can someone use it in 30 seconds? |
| FAST | Does it feel instant? |
| SOLID | Would it survive a hostile security audit? |
| TESTED | Would you know if something broke? |
| ALIVE | Does it have any personality? |
| MONEY | Could it make money, and who pays? |
| ELEGANT | Would a good engineer respect the code? |
| READY | One-command deploy? |
| ORIGINAL | Does this already exist? Why is this version worth having? |

### `cheatcodes.md` — Claude Code settings notes

Environment variables, effort levels, thinking triggers, permission modes, and
keyboard shortcuts, collected in one place. These are settings and usage notes
gathered from the docs and from using the tool a lot — not benchmark results.

## Installation

Claude Code:

```bash
cp genesis.md production-autopilot.md rubric.md ~/.claude/skills/
```

Codex CLI (no `.md` extension):

```bash
cp genesis production-autopilot rubric ~/.codex/skills/
```

Settings I run with, in `~/.claude/settings.json`:

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

## How they're written

Conventions used throughout, based on what's held up for me across a lot of
sessions — your results may differ:

- XML tags (`<instructions>`, `<critical>`) to mark section boundaries
- `IMPORTANT:` / `CRITICAL:` prefixes on rules that shouldn't be skipped
- Thinking triggers (`think hard`) on the phases that need more reasoning
- Explicit output formats in agent prompts instead of open-ended asks
- Evidence required for every rubric score
- An adversarial review pass, so "good enough" gets challenged by something
- Context management directives, since quality degrades in long sessions

## License

MIT — [@evilander](https://github.com/evilander)
