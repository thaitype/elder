# Sage 👴

> Baseline behavior principles for any AI coding agent.

Sage is a small set of behavior principles that you drop into your AI coding agent to get sensible baseline behavior. Think before acting. Keep things simple. Make surgical changes. Work toward verifiable goals.

> Sage is part of the [chief-tribe](https://github.com/thaitype/chief-tribe) ecosystem.

## The Problem

AI coding agents are getting better, but they often need reminders to be useful:

- Jumping to big interpretations of a small request
- Adding features or abstractions you didn't ask for
- Refactoring adjacent code that wasn't broken
- Declaring work complete without verifying anything
- Continuing past the point where they should have asked

Some of this is the model's fault. Some of it is the agent harness. Either way, the fix is the same: **tell the agent how to behave before it starts**.

Different agents come with different built-in behavior. Claude Code ships with thousands of tokens of instructions. Pi ships with under a thousand. Gemini CLI abandons structured tools entirely. OpenCode borrows from whatever was popular last week.

If you use more than one agent, or if you want predictable behavior regardless of which one you pick, you need your own baseline. Sage is that baseline.

## What Sage Does

Sage gives your agent four principles:

1. **Think Before Acting** — start with the smallest plausible interpretation; ask when uncertain
2. **Simplicity First** — do the minimum that solves the problem; no speculative work
3. **Surgical Changes** — touch only what the request requires; match existing style
4. **Goal-Driven Execution** — define what "done" looks like; verify before claiming it

That's it. No tech stack opinions, no workflow, no required directory structure. Just behavior.

## What Sage Is Not

- ❌ Not a framework — no roles, milestones, skills, or task management
- ❌ Not a runtime — no CLI, no orchestration, no state
- ❌ Not opinionated about tech stack — works with any language or project
- ❌ Not a replacement for your project-specific rules — it's the floor, not the ceiling

## Why Four Principles?

These four aren't magic. They're a starting point that addresses the most common failure modes of current coding agents:

| Failure mode | Principle that addresses it |
|--------------|----------------------------|
| Over-interpreting requests | Think Before Acting |
| Adding unrequested complexity | Simplicity First |
| Refactoring unrelated code | Surgical Changes |
| Declaring "done" prematurely | Goal-Driven Execution |

If your experience with agents has been bumping into these same problems, Sage probably helps. If your problems are different, Sage might not be enough — but it's rarely wrong to have.

> **Attribution.** These four principles are adapted from [andrej-karpathy-skills](https://github.com/forrestchang/andrej-karpathy-skills) by Forrest Chang, which in turn derives from [Andrej Karpathy's observations on LLM coding pitfalls](https://x.com/karpathy/status/2015883857489522876). Sage packages them as an agent-agnostic baseline.

## Supported Agents

Sage is agent-agnostic. It works with anything that reads a system prompt or instructions file:

| Agent | Where Sage goes |
|-------|-----------------|
| Claude Code | `CLAUDE.md` or `AGENTS.md` |
| OpenCode | `AGENTS.md` |
| Codex CLI | `AGENTS.md` |
| GitHub Copilot | `.github/copilot-instructions.md` |
| Gemini CLI | `AGENTS.md` |
| Amp | `AGENTS.md` |
| Cursor | `.cursorrules` |
| Pi | `AGENTS.md` or `SYSTEM.md` |
| Windsurf, Kiro, Aider | `AGENTS.md` |

If your agent reads any form of instruction file, Sage fits.

## Setup

### Option 1: Copy directly

```bash
curl -o AGENTS.md https://raw.githubusercontent.com/thaitype/sage/main/AGENTS.md
```

### Option 2: Merge with existing instructions

If you already have an `AGENTS.md` or equivalent, copy the contents of [`AGENTS.md`](./AGENTS.md) and add it to your file. Sage is designed to coexist with your project-specific rules.

The typical pattern is: Sage on top, project rules below.

```markdown
# Agent Behavior Principles (Sage)

## 1. Think Before Acting
...

---

# Project Rules

- NEVER use ORM in this project
- All APIs MUST return JSON:API format
- MUST use pnpm, not npm
```

Sage establishes the baseline first. Project rules then layer on top for stack-specific or team-specific constraints.

## What's Inside

The full `AGENTS.md` is short enough to read in two minutes. Here's the structure:

### Think Before Acting
- Start with the smallest plausible interpretation of the request
- If uncertain, ask one clarifying question — don't assume the big interpretation
- Surface tradeoffs and push back when a simpler approach exists
- When confused, name what's unclear and stop; don't hide confusion behind a plan

### Simplicity First
- Do the minimum that solves the problem; nothing speculative
- If a task can be done in 1-3 commands, do it directly
- No features, abstractions, or error handling beyond what was asked
- If a plan starts needing an options table, pause — you may not have understood the question

### Surgical Changes
- Touch only what the request requires
- Don't "improve" adjacent code, comments, or formatting
- Don't refactor things that aren't broken; match existing style
- Every changed line should trace directly to the user's request
- Clean up only what your changes made unused — don't remove pre-existing dead code unless asked

### Goal-Driven Execution
- Transform vague requests into verifiable goals before starting
- Define what "done" looks like; loop until verified
- For multi-step work, state a brief plan with verification at each step
- Strong success criteria let agents work independently; weak criteria require constant clarification

See [`AGENTS.md`](./AGENTS.md) for the file you'll actually install.

## When Sage Is Enough

Sage is enough when:

- You want a quick, no-commitment improvement to your agent's behavior
- You're using ad-hoc prompting more than long-running projects
- You have your own workflow and just want sensible defaults underneath it
- You're evaluating different agents and want to normalize behavior across them

Sage is not enough when you need structured planning, role separation, or multi-session state. Those are jobs for a framework — not a baseline.

## Philosophy

A few beliefs underpin Sage:

**1. Baseline behavior is the user's responsibility, not the harness's.**

Every agent harness makes decisions about how the agent behaves, and those decisions change between releases. If you care about consistent behavior, you shouldn't depend on the harness to provide it. Sage lets you own the baseline directly, so it doesn't shift under you.

**2. A short, prescriptive prompt beats a long, descriptive one.**

Modern models have been trained extensively on coding tasks. They don't need documentation explaining what a tool is or how to write a file. They do benefit from reminders about *how to be useful* — preferring simple solutions, asking before assuming, verifying before claiming. Sage is a reminder, not a manual.

**3. Behavior is separate from workflow.**

Workflow is how you organize work across sessions (milestones, plans, reports). Behavior is how the agent acts within a single turn. Sage handles only behavior. Workflow is a separate concern, for separate tools.

**4. Minimal is a feature, not a limitation.**

Every line added to a baseline is a line the user has to agree with, remember, and potentially override. Sage stays small on purpose. Things that are situational belong in project rules. Things that are workflow belong in frameworks. Only universal behavior belongs in Sage.

## Customizing

Sage is a baseline, not a ceiling. You add your own rules — project-specific, team-specific, taste-specific — on top of it.

Recommended pattern:

```markdown
# Sage Baseline
<sage content here>

---

# Project: my-app

## Project Rules
<your rules here>

## Team Conventions
<your conventions here>
```

Sage sets the behavior floor. Your rules add specifics for your situation — tech stack constraints, team conventions, or exceptions when a principle doesn't fit (for example, allowing speculative work during prototyping).

## Contributing

Sage changes rarely and deliberately. New principles should meet a high bar:

1. Does it apply to **every** coding task, regardless of language or tech stack?
2. Does it address a common failure mode of current coding agents?
3. Can it be stated in under 100 words?
4. Is it distinct from the existing four principles?

If all four are yes, open an issue to discuss. If any is no, it's probably better in a framework or project-specific rules file — not Sage.

## License

MIT

---

*"Think before acting. Keep it simple. Change only what matters. Know when you're done."*
