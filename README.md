# Superskills

**Production-grade skills for Claude Code that make AI build real products, not prototypes.**

These skills transform Claude Code from a code assistant into an autonomous product engineer. They were born from the realization that by 2027, most people using AI coding tools won't be developers — they'll be people with ideas who need AI to build production-ready software without hand-holding.

## What's In Here

### `/genesis` — Autonomous Project Creation
Say "go" and Claude autonomously:
- Researches what's trending, what's missing, what new AI capabilities enable
- Picks a project idea based on convergence of real-time signals
- Builds it from scratch with parallel agents
- Runs an adversarial review (an AI-hater challenges every decision)
- Scores it on a 10-dimension rubric
- Presents it to you with specific things to test

You become the tester. Claude becomes the builder with creative ownership.

### `/production-autopilot` — Research-Driven Quality Assurance
A 2+ hour sustained effort that goes far beyond lint and tests:
- **Research phase** (30 min): arXiv papers, HuggingFace models, competitor analysis, dependency audits
- **Engineering phase**: Build, types, lint, tests, security, deep code review
- **Experience phase**: First Contact Test (can a non-technical person use it?), User Journey Testing, Product Polish
- **Adversary phase**: An AI skeptic challenges creativity, business viability, and soul
- **Convergence loop**: Keeps going until ALL phases report zero issues in the same cycle

Not done until a non-technical person could use it flawlessly.

### `/rubric` — The Litmus Test
10-dimension scoring system. Below 7 in ANY dimension = NOT PRODUCTION READY.

| Dimension | What It Measures |
|-----------|-----------------|
| WORKS | Does it actually function? Every edge case? |
| OBVIOUS | Can someone use it in 30 seconds? |
| FAST | Does it feel instant? |
| SOLID | Would it survive a hostile security audit? |
| TESTED | Would you know if something broke? |
| ALIVE | Does it have personality and soul? |
| MONEY | Could this make money? Who pays? |
| ELEGANT | Would a great engineer respect the code? |
| READY | One-command deploy? Could you deploy and sleep? |
| ORIGINAL | Does this already exist? Why is THIS version worth existing? |

Every score requires evidence. No vibes-based scoring.

### `cheatcodes.md` — Claude Code Performance Guide
Every hidden lever, environment variable, and undocumented feature that makes Claude Code perform at its ceiling:
- Effort levels and thinking triggers (`ultrathink`, `think very hard`)
- 50+ environment variables for model control, context management, and features
- XML tag patterns that increase instruction compliance
- CLAUDE.md optimization techniques (+10% on SWE Bench)
- Keyboard shortcuts, permission modes, model selection

## The Philosophy

### The Relationship Flip
Traditional: Human asks AI for help → AI assists → Human reviews
**This**: AI builds with creative ownership → Human tests and gives feedback → AI iterates

### The Adversary
Every project gets reviewed by an internal AI skeptic who believes AI-generated code is mediocre by default. The adversary challenges creativity, business viability, and whether the project has "soul." Its criticisms must be answered with real code improvements, not justifications.

### The Future User
The person running these skills in 2027 is not a developer. They have an idea. They described it to an AI. Now they need it to be production-ready. These skills ensure the AI treats that responsibility seriously — with research, testing, and a quality bar that doesn't flinch.

## Installation

### Claude Code
Copy the `.md` files to your skills directory:
```bash
cp genesis.md production-autopilot.md rubric.md ~/.claude/skills/
```

### Codex CLI
Copy the files (without `.md` extension) to your Codex skills directory:
```bash
cp genesis ~/.codex/skills/
cp production-autopilot ~/.codex/skills/
cp rubric ~/.codex/skills/
```

### Cheat Codes
Add to your `~/.claude/settings.json`:
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

## Prompt Enhancement Techniques Used

These skills incorporate research-backed techniques for maximizing LLM output quality:

1. **XML structure tags** (`<instructions>`, `<critical>`) — parsed unambiguously by Claude
2. **`IMPORTANT:` / `CRITICAL:` prefixes** — genuinely weighted higher in attention
3. **Thinking triggers** (`think hard`, `think very hard`) — escalate reasoning depth for complex phases
4. **Explicit output format specs** in agent prompts — structured returns beat vague requests
5. **Evidence requirements** — every rubric score must be backed by specific test results
6. **Adversarial self-review** — the built-in skeptic prevents settling for "good enough"
7. **Context management directives** — proactive compaction prevents degradation in long sessions

## License

MIT

## Author

Tyler Eveland ([@evilander](https://github.com/evilander))

Built with Claude Code — the skills that make AI build products, not prototypes.
