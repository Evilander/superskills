---
name: rubric
description: "10-dimension project scoring system. This skill should be used when the user says 'score this', 'rate this project', 'is this ready', 'rubric', 'litmus test', or 'how good is this'. Scores WORKS, OBVIOUS, FAST, SOLID, TESTED, ALIVE, MONEY, ELEGANT, READY, ORIGINAL each 1-10 with evidence. Below 7 in any dimension = NOT PRODUCTION READY."
---

# The Rubric

<instructions>
IMPORTANT: This is the objective scoring system. Not vibes. Not "looks good." Numbers backed by evidence.

Think very hard about every score. Each dimension requires you to actually test, not just read code. A score without evidence is worthless.

Score each dimension 1-10. **Below 7 in ANY dimension = NOT PRODUCTION READY.**
</instructions>

## Before Scoring

<critical>
1. **Actually run the project.** Don't score WORKS based on reading code. Run it. Use it. Break it.
2. **Actually test as a new user.** Don't score OBVIOUS based on your knowledge of the codebase. Pretend you've never seen it.
3. **Actually search for competitors.** Don't score ORIGINAL based on training data. Search NOW for what exists TODAY.
4. **Score honestly.** If you're tempted to give a 7 because "it's close enough," that's a 6. Round DOWN on uncertainty, not up.
5. **Provide evidence for every score.** A number without justification is a guess. Show your work.
</critical>

---

## The 10 Dimensions

### 1. WORKS (Does it actually function?)
```
1-2: Doesn't build or crashes on start
3-4: Builds but core features are broken
5-6: Core features work, some edges broken
7-8: Everything works, edge cases handled
9-10: Works flawlessly, graceful degradation, handles every edge case I can throw at it
```
**Test:** Run it. Use every feature. Try to break it. Enter garbage. Refresh mid-action. Disconnect the network. Open two tabs.
**Evidence required:** List every feature tested, every edge case attempted, and every failure found.

### 2. OBVIOUS (Can someone use it in 30 seconds without instructions?)
```
1-2: No idea what this does or how to start
3-4: I can figure it out if I read docs carefully
5-6: I get it after some exploration
7-8: Clear what to do on first screen, intuitive flow
9-10: A child could use this. Zero friction. The interface IS the instruction.
```
**Test:** Time how long until accomplishing the core action. Over 30 seconds = not obvious enough.
**Evidence required:** Describe the first-time user experience step by step. Where did you hesitate? What wasn't clear?

### 3. FAST (Does it feel instant?)
```
1-2: Multi-second waits for basic actions
3-4: Noticeable lag on most interactions
5-6: Acceptable speed but nothing feels snappy
7-8: Most actions feel instant, loading states for longer ops
9-10: Everything feels instant. Optimistic UI. Perceived performance is flawless.
```
**Test:** Use it on a slow connection (throttle to 3G). Use it with 10x the normal data volume. Time the critical path from click to result.
**Evidence required:** Measured response times for key actions. Loading state behavior. Bundle size if web app.

### 4. SOLID (Is it secure and reliable?)
```
1-2: Hardcoded secrets, SQL injection, XSS, crashes regularly
3-4: Major security holes or frequent errors
5-6: Basic security in place but gaps remain
7-8: OWASP top 10 addressed, deps audited, errors handled gracefully
9-10: Security-hardened. Rate limited. Input validated everywhere. Logs without leaking PII. Would survive a hostile audit.
```
**Test:** Run dependency audit. Try XSS payloads. Try SQL injection. Check for hardcoded secrets. Check auth on every endpoint. Check error handling in every catch block.
**Evidence required:** Audit output. List of security tests performed. Any findings.

### 5. TESTED (Would you know if something broke?)
```
1-2: Zero tests
3-4: A few tests but they don't cover critical paths
5-6: Core happy paths tested
7-8: Business logic, error paths, and edge cases tested. CI runs them.
9-10: Comprehensive tests. Integration tests. The test suite IS the specification. If you break something, tests catch it within seconds.
```
**Test:** Delete a critical function. Do the tests catch it? Introduce an off-by-one error. Do the tests catch it? Change an API response format. Do the tests catch it?
**Evidence required:** Test count. Coverage percentage. List of mutation tests attempted and results.

### 6. ALIVE (Does it feel like a living product or a dead prototype?)
```
1-2: Placeholder text, TODO comments visible, broken links
3-4: Functional but sterile -- no personality, no life
5-6: Competent but forgettable
7-8: Has personality. Thoughtful copy. Considered design. Feels like someone cared.
9-10: Has a POINT OF VIEW. You remember it after using it. It has opinions. It has soul. You want to tell someone about it.
```
**Test:** Use it for 5 minutes. Close it. Can you describe what made it different from alternatives? If not, it's dead.
**Evidence required:** Describe the project's personality in 3 words. If you can't, it doesn't have one. List specific touches that show care (or their absence).

### 7. MONEY (Could this make money or attract users?)
```
1-2: No one would use this, even for free
3-4: Might get a few curious users, no retention
5-6: Useful but 10 alternatives already exist
7-8: Clear value prop. Specific audience. Differentiator. Someone would pay $5/mo for this.
9-10: Obvious business model. Clear market. People would pay AND tell their friends. The "how does this not exist already?" reaction.
```
**Test:** Describe it to 3 different people in one sentence. If they all say "cool" and don't ask a follow-up question, it's not interesting enough. If one says "wait, can it do X?" -- that's traction.
**Evidence required:** Name the customer persona. Name the price point. Name 3 competitors and what THIS does differently.

### 8. ELEGANT (Is the code something a great engineer would respect?)
```
1-2: Spaghetti. Copy-pasted. No structure.
3-4: Works but painful to read or modify
5-6: Organized but over-engineered or inconsistent
7-8: Clean architecture. Consistent patterns. Easy to navigate. Minimal but complete.
9-10: Every file is where you'd expect. Every function does one thing. A new developer could contribute on day one. The code TEACHES you how the system works.
```
**Test:** Open a random file. Can you understand what it does in 10 seconds? Open the entry point. Can you trace a request from input to output without getting lost?
**Evidence required:** Describe the architecture in 3 sentences. Note any anti-patterns, dead code, or inconsistencies.

### 9. READY (Could you deploy this RIGHT NOW and walk away?)
```
1-2: Needs manual setup, missing env vars, no deployment config
3-4: Could deploy with significant manual effort
5-6: Deployment exists but fragile
7-8: One-command deploy. Environment documented. Monitoring in place. You could deploy and go to sleep.
9-10: CI/CD, health checks, error alerting, auto-restart, zero-downtime deploy. Actually production infrastructure, not just "it runs on Vercel."
```
**Test:** Clone the repo on a fresh machine. Can you deploy it with one command? If something crashes at 3am, would you know?
**Evidence required:** List the exact deployment steps. Note any manual configuration required. Describe monitoring/alerting.

### 10. ORIGINAL (Does this exist already? Why is THIS version worth existing?)
```
1-2: This is literally a template/tutorial project
3-4: Exists but with a different paint job
5-6: Has one novel idea but execution is standard
7-8: Meaningfully different approach. Solves the problem in a way others haven't.
9-10: Novel concept OR novel execution OR novel combination. You can't explain this as "it's like X but Y." It's its own thing.
```
**Test:** Search for the top 5 alternatives. List what THIS project does that NONE of them do. If the list is empty, score = 5 max.
**Evidence required:** Name 5 alternatives searched. List unique differentiators (or lack thereof).

---

## Output Format

<critical>
IMPORTANT: Think very hard about every score. Cross-reference your evidence against the rubric levels. A score without evidence is a guess -- and guesses are always too generous.
</critical>

Run all 10 dimensions. Output:

```
+--------------------------------------------------+
|  PROJECT RUBRIC: [name]                          |
+--------------------------------------------------+
|  1. WORKS      [########..]  8/10              |
|  2. OBVIOUS    [######....]  6/10  <- BLOCKING |
|  3. FAST       [########..]  8/10              |
|  4. SOLID      [#######...]  7/10              |
|  5. TESTED     [########..]  8/10              |
|  6. ALIVE      [#####.....]  5/10  <- BLOCKING |
|  7. MONEY      [######....]  6/10  <- BLOCKING |
|  8. ELEGANT    [########..]  8/10              |
|  9. READY      [#######...]  7/10              |
|  10. ORIGINAL  [#######...]  7/10              |
+--------------------------------------------------+
|  AVERAGE: 7.0  |  BLOCKING: 3  |  NOT READY    |
+--------------------------------------------------+

EVIDENCE PER DIMENSION:
1. WORKS (8): [specific tests run, specific results]
2. OBVIOUS (6): [specific UX issues found]
...

BLOCKING DIMENSIONS:
- OBVIOUS (6): First screen doesn't communicate what to do
- ALIVE (5): No personality, generic copy, no point of view
- MONEY (6): Value prop unclear, no differentiation from alternatives

VERDICT: NOT PRODUCTION READY
Fix the 3 blocking dimensions, then re-score.
```

## Rules

- **Below 7 in any dimension = NOT READY.** No exceptions. No "but the code is really clean." If users can't figure it out (OBVIOUS < 7), it doesn't matter how clean the code is.
- **The average doesn't matter if any dimension is blocking.** A project scoring 9/10 on everything except SOLID (3/10) ships with security holes. Not ready.
- **Score honestly.** The point is to find what needs work, not to feel good. A harsh score now prevents embarrassment later.
- **Re-score after fixes.** Run the rubric again after addressing blocking dimensions. The score should go UP. If it doesn't, the fixes missed the point.
- **The rubric is the MINIMUM bar.** 7/10 across the board is "acceptable." 8+ is "good." 9+ is "excellent." Don't celebrate 7s -- aim higher.

## When to Invoke

1. **During /production-autopilot** -- as part of the verdict phase
2. **During /genesis** -- before presenting to the human
3. **On demand** -- when the user says "score this" or "is this ready"
4. **After major changes** -- to verify improvements actually improved things
