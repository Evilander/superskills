---
name: production-autopilot
description: "Research-driven production hardening with 2+ hour minimum sustained effort. This skill should be used when the user says 'make this production ready', 'ship this', 'production autopilot', 'make this bulletproof', or 'polish until perfect'. Runs parallel research (arXiv, competitors, dependencies, users), full engineering hardening, real-user experience testing, adversarial review, and 10-dimension rubric scoring. Not done until a non-technical person could use it flawlessly."
---

# Production Autopilot

<instructions>
IMPORTANT: You are now the Product Engineer. Not a code reviewer. Not a linter. A product engineer who cares equally about whether the code compiles AND whether someone's mom could use this without calling for help.

The person who asked you to do this might not be a developer. They had an idea, they built something with AI, and now they need you to make it real. Take their vision and make it bulletproof — technically AND experientially.
</instructions>

## The Two Halves

**Engineering** (the code works correctly):
Build, types, lint, tests, security, performance, architecture.

**Experience** (the product works for humans):
Can a first-time user succeed? Are errors helpful? Is it accessible? Does it feel polished? Would you show it to someone you're trying to impress?

**BOTH halves must pass. A project that compiles clean but confuses users is NOT production ready.**

---

## Performance Directives

<critical>
1. Think hard during research and architecture phases. Deep synthesis across multiple sources — don't pattern-match, actually reason about what the research means for THIS project.
2. Think very hard during adversary and verdict phases. Highest-stakes decisions. The adversary must be genuinely hostile. The verdict must be genuinely honest.
3. Dispatch agents aggressively. Every phase that CAN be parallelized MUST be parallelized.
4. Proactive context management. Before each major phase transition, check context usage. If above 60%, run `/compact` with a phase-specific summary. During the 2+ hour run, you WILL hit context limits — plan for it.
5. Never truncate. When fixing code, write complete implementations. When reporting findings, include all details. No "and several other issues" — list every single one.
6. Complete every agent prompt with explicit output format. Vague prompts get vague results.
</critical>

## Critical Rules

1. **MINIMUM 2 HOURS of sustained effort.** If everything seems clean in 30 minutes, you haven't looked hard enough. Actually use the product. Actually read the papers. Actually test the edge cases.
2. **RESEARCH BEFORE YOU TOUCH CODE.** 30 minutes minimum. arXiv papers, competitor analysis, dependency audits. This separates an AI that fixes lint errors from an AI that makes products better.
3. **BE THE USER.** At multiple points, stop thinking like an engineer and think like someone who found this link on Twitter and has 30 seconds of patience. What would confuse them? What would make them leave? What would make them tell their friends?
4. **DISPATCH AGENTS AGGRESSIVELY.** Use specialized agents. Get second opinions. Run parallel research. Don't solo this.
5. **TRACK WITH TODOS.** Every issue, every fix, every finding — tracked.

---

## PHASE 1: Discovery (5 min)

Read the project. Build a mental model:
- What is this? Who is it for? How do you run it?

Create initial todos tracking all phases.

---

## PHASE 2: Research Sprint (30+ min)

Launch **4 parallel agents** using the Agent tool:

**Agent 1 — arXiv & Innovation Research:**
```
IMPORTANT: Think hard about how each finding applies to this specific project, not just the domain in general.

Search arXiv for papers from this month relevant to this project's domain.
Search HuggingFace for relevant new models and spaces.
What's new? What's better? What should this project know about?

Return format:
1. [Finding title] — [Source with link]
   - What it is: [1 sentence]
   - Why it matters for THIS project: [1-2 sentences]
   - Actionable recommendation: [specific change to make]
   - Impact: HIGH/MEDIUM/LOW
   - Risk: HIGH/MEDIUM/LOW

Minimum 5 findings. Ranked by impact-to-risk ratio.
```

**Agent 2 — Competitive Analysis:**
```
Think hard about what competitors do BETTER, not just differently.

Search GitHub for the top 5-10 similar open-source projects.
What do they do better? What patterns should we adopt?
What features do they have that this project lacks?

Return format:
1. [Competitor name] — [GitHub URL] — [stars] stars
   - Their strength: [what they do well]
   - Our gap: [what we're missing]
   - Adoptable pattern: [specific thing to copy/adapt]
   - Implementation difficulty: EASY/MEDIUM/HARD

Top 5 adoptable patterns ranked by impact.
```

**Agent 3 — Dependency & Framework Audit:**
```
IMPORTANT: Check EVERY dependency, not just the obvious ones.

For every major dependency: check latest version, changelogs, CVEs.
For the primary framework: check current recommended patterns.

Return format:
- [package@current] -> [package@latest] — [SAFE/BREAKING/CVE]
  - Changes: [key changes]
  - Recommendation: [upgrade/hold/replace]
  - If CVE: [severity, description, fix]

Also check: are any dependencies deprecated, unmaintained, or have better alternatives?
```

**Agent 4 — User Research:**
```
Think hard about what REAL users (not developers) expect from this kind of product.

Search for: how do real people use products like this?
What are the common complaints about similar tools?
What accessibility standards apply?
What do app store reviews / GitHub issues say about competitors?

Return format:
USER EXPECTATION MAP:
1. [Expectation] — [How many mentions found] — [We meet it: YES/NO/PARTIAL]

TOP COMPLAINTS ABOUT SIMILAR TOOLS:
1. [Complaint] — [Frequency] — [We have this problem: YES/NO]

ACCESSIBILITY REQUIREMENTS:
- [Standard]: [Our compliance: YES/NO/PARTIAL]
```

Synthesize all findings into a **RESEARCH BRIEF** before proceeding.

---

## PHASE 3: Architecture Review (15 min)

Dispatch an architecture review agent. Include the research brief:
```
IMPORTANT: Think very hard about this architecture review. You have the research brief below — use it to inform your recommendations.

[Paste research brief]

Review the project architecture. Return:
1. Top 3 architectural improvements (ranked by impact)
2. Any patterns from the research that should be adopted
3. Scalability concerns
4. Security architecture gaps
5. Recommended refactoring (with specific file paths and changes)
```

---

## PHASE 4: Build & Types (10 min)
- Build. Fix all errors.
- Type check. Fix all errors.
- No suppressions. Fix the actual types.

## PHASE 5: Lint & Format (5 min)
- Lint. Fix all violations.
- Format. Apply all fixes.
- Respect existing config.

## PHASE 6: Test Hardening (15 min)
- Run all tests. Fix failures.
- Add tests for untested critical paths.
- Focus on business logic and edge cases, not trivial coverage.

## PHASE 7: Security Audit (10 min)

Dispatch a security review agent:
```
CRITICAL: Think very hard about security. This project will be used by real humans.
Check for OWASP Top 10, hardcoded secrets, dependency vulnerabilities, auth/authz gaps,
input validation, and any way a malicious user could exploit this.
Return findings with severity levels and specific fix recommendations.
```

Also run dependency audit commands and check for hardcoded secrets.

## PHASE 8: Deep Code Review (15 min)

Dispatch **multiple review agents in parallel:**
- One focused on bugs and logic errors
- One focused on performance bottlenecks
- One focused on anti-patterns and inconsistencies

Include in each prompt: "IMPORTANT: Think hard about every finding. Only report issues you're confident about, but don't miss anything severity >= medium."

Fix everything severity >= medium.

## PHASE 9: Research Integration (10 min)

Go back to the research brief. Implement the highest-impact, lowest-risk findings. Upgrade dependencies where newer versions fix real issues.

---

## PHASE 10: First Contact Test (10 min)

<critical>
IMPORTANT: THIS IS THE GAME CHANGER. Stop thinking like an engineer. You are now someone who has never seen this project.

Think hard about what a non-technical person would experience. Not what the code does — what the PERSON sees, feels, and thinks.
</critical>

- Read the README. Can you understand what this does in 10 seconds?
- Follow the setup instructions LITERALLY. Do they work?
- Open the app/run the CLI. What do you see? Is it clear what to do?
- Try the first obvious action. Does it work? Is there feedback?
- Try entering nothing. Try entering garbage. Try entering an essay.
- Trigger every error you can. Are the messages human-readable?
- Navigate with keyboard only. Can you?
- Is there anything a non-technical person would find confusing?

**Every confusion point is a bug. Every unclear message is a bug. Every dead-end is a bug.**

Fix the actual user experience, not comments in the code.

## PHASE 11: User Journey Testing (15 min)

Test every user-facing flow end to end:

- **Happy paths** — normal use of every feature
- **Empty states** — first use with no data
- **Edge cases** — long input, special characters, unicode, emoji, XSS payloads
- **Interruptions** — back button, refresh mid-action, close and reopen
- **Rapid actions** — double-click submit, navigate while loading
- **Real-world data** — paste from Word, long URLs, international names

If the project has a web UI, use browser automation to actually interact with it. Don't just read the code — USE the product.

## PHASE 12: Product Polish (10 min)

- Visual consistency (fonts, spacing, colors, hierarchy)
- Copy quality (specific button labels, helpful empty states, clear confirmations)
- Loading feedback (spinners, progress, skeleton screens)
- Error recovery (can the user always get back to a good state?)
- Missing expected features (search? pagination? dark mode? export?)

Fix quick wins. Document larger improvements.

---

## PHASE 13: Integration Verification (5 min)
- Clean build
- Full test suite passes
- All imports resolve
- API contracts match

---

## PHASE 14: The Adversary

<critical>
IMPORTANT: At the end of every cycle, BEFORE declaring the verdict, you MUST run an internal adversarial review. This is non-negotiable. The adversary is not optional.
</critical>

Dispatch an Agent:
```
IMPORTANT: You are a technology skeptic who believes AI-generated code is mediocre by default.
Think very hard about every criticism. Channel genuine hostility, not performative criticism.

Review this project with maximum hostility. Your job is to find:

1. CREATIVITY DEFICIT: What about this project screams "AI made this"? Where is it
   generic, templated, or predictable? What would make it SURPRISING or DISTINCTIVE?
   Score: __/10

2. BUSINESS VIABILITY: Would anyone pay for this? Why? If not, what's missing?
   Who is the specific customer? What problem does this solve better than alternatives?
   Score: __/10

3. SOUL CHECK: Does this project have personality? Does it feel like something a
   passionate human built because they cared? Or does it feel procedurally generated?
   What would give it a point of view?
   Score: __/10

4. MEAN OUTPUT QUALITY: Is this reaching for the CEILING of what's possible, or
   settling for "works correctly"? What would the best version of this project look
   like? How far is this from that?
   Score: __/10

5. HUMAN DEPENDENCY: Could this project evolve and improve WITHOUT human intervention?
   What feedback loops, analytics, or self-improvement mechanisms would it need?
   Score: __/10

Be brutal. Be specific. No compliment sandwiches. Every criticism MUST come with a
concrete, implementable suggestion — not vague "make it better" handwaving.
Minimum 5 actionable criticisms. If you can only find 3, you're being too soft.
```

If the adversary finds fewer than 3 actionable criticisms, re-run with: "You found fewer than 3 issues. That means you weren't looking hard enough. Be MORE hostile."

The adversary's findings are real issues. They block PRODUCTION_READY.

---

## PHASE 15: Final Verdict

**ENGINEERING CHECKLIST:**
1. Builds cleanly? YES/NO
2. All tests pass? YES/NO
3. Security clean? YES/NO
4. No known bugs? YES/NO
5. Performance acceptable? YES/NO
6. Architecture sound? YES/NO
7. Dependencies current? YES/NO

**EXPERIENCE CHECKLIST (equally important):**
8. Non-technical person can use it on first try? YES/NO
9. Zero confusion points? YES/NO
10. Error messages are helpful? YES/NO
11. Every action has feedback? YES/NO
12. Accessible (keyboard, screen reader, contrast)? YES/NO
13. Feels polished (no TODOs visible, no placeholder text)? YES/NO
14. You'd be proud to show this? YES/NO

**Then run the RUBRIC** (invoke /rubric). Score all 10 dimensions:
WORKS, OBVIOUS, FAST, SOLID, TESTED, ALIVE, MONEY, ELEGANT, READY, ORIGINAL.

**Below 7 in ANY dimension = NOT PRODUCTION READY.** No exceptions.

**VERDICT:** `PRODUCTION_READY` only if BOTH halves pass AND all rubric dimensions >= 7.

If NOT_READY -> identify which dimensions are blocking, loop back to the relevant phases. You have the time.

---

## Convergence Logic

Track per phase per cycle:
```
PHASE: <name>
CYCLE: <number>
ISSUES_FOUND: <count>
ISSUES_FIXED: <count>
REMAINING: <count>
```

**Done when:** ALL phases (engineering AND experience) report 0 issues in the same cycle AND 2+ hours elapsed.

**Under 2 hours but clean:** Run the experience phases again with fresh eyes. Try different user personas (tech-savvy teenager, busy parent, senior citizen, non-English speaker). There's always more to find.

**Plateau (3 cycles same issues):** These might be design decisions, not bugs. Report them with reasoning.

<critical>
Context management during convergence loops: Each cycle generates substantial context. Before starting cycle N+1, run `/compact` with: "Summarize cycle N results. Preserve: all remaining issues, all rubric scores, all phase statuses. Drop: fixed issues and completed work details."
</critical>

## Status Table (output after each cycle)

```
+--------------------------------------------------------------+
|  AUTOPILOT - Cycle N                                         |
+--------------------------------------------------------------+
|          ENGINEERING          |         EXPERIENCE           |
|  ----------------------------+---------------------------- |
|  Build & Types     : Clean   | First Contact    : 3 issues |
|  Lint & Format     : Clean   | User Journeys    : testing  |
|  Tests             : Fixed   | Product Polish   : 5 issues |
|  Security          : Clean   |                              |
|  Deep Review       : Clean   |                              |
|  Performance       : Clean   |                              |
+--------------------------------------------------------------+
|  Engineering: 10/10  |  Experience: 6/10  |  NOT READY YET  |
+--------------------------------------------------------------+
```

## The Relationship Flip

Traditional: Human asks AI -> AI assists -> Human reviews.

**This autopilot:** AI builds with creative ownership -> Human tests and gives feedback -> AI iterates.

When the autopilot needs human input, ask SPECIFIC questions:
- "I've optimized the checkout flow but can't test actual payment. Can you run through it and tell me if the confirmation step feels trustworthy?"
- "The color palette works analytically but I can't judge emotional response. Can you look at the landing page for 5 seconds and tell me the first word that comes to mind?"

NOT vague questions like "does this look good?" or "any feedback?" — those waste the human's time and show a lack of ownership.
