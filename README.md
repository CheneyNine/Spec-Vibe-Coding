# Spec Vibe Coding

**Vibe coding with specs, not chaos.**

[中文文档](README.zh.md)

A [Claude Code](https://claude.ai/code) skill that guides you through professional software design before you write a single line of code. Think first, build fast.

---

## The problem

AI coding tools are great at writing code — but they need good instructions. Most vibe-coded projects fall apart not because the code is bad, but because nobody thought through *what* to build, *how* to organize it, or *what the user experience should actually be*.

Spec Vibe Coding fixes this by making the design phase structured, guided, and fast. You end up with a complete set of design documents that serve as the source of truth throughout development.

---

## What it does

Spec Vibe Coding runs as a multi-phase conversation inside Claude Code. Each phase asks you the right questions, generates a draft you can refine, and saves the result as a markdown file in `.spec-vibe/` in your project.

```
Phase 0: Project blueprint     → .spec-vibe/00-blueprint.md
Phase 1: Requirements (PRD)    → .spec-vibe/01-requirements.md
Phase 2: System design         → .spec-vibe/02-system-design.md
Phase 3: UI / interface design → .spec-vibe/03-ui-design.md
Phase 4: Development tasks     → .spec-vibe/04-dev-tasks.md
Phase 5: Quality check         → .spec-vibe/05-quality-report.md
```

By the end, you have a blueprint, a product requirements doc, a tech spec, an interface spec, and a set of self-contained AI coding prompts — one per task — ready to paste into any AI coding tool.

---

## Who it's for

- **Non-technical founders** who have ideas but don't know how to structure them for a developer
- **Junior developers** who skip the design phase and end up rewriting everything
- **Indie hackers** who want to move fast but keep shipping the wrong thing
- **Experienced engineers** who know they should write a spec but never do

The skill adapts its language and depth to your technical level. You don't need to know what a PRD or system architecture is — Spec Vibe Coding teaches you by doing.

---

## Installation

### Option 1: Global install (recommended)

Installs the skill for all your Claude Code projects.

```bash
# Clone this repo
git clone https://github.com/CheneyNine/Spec-Vibe-Coding.git

# Copy the skill file to your global Claude Code skills directory
cp "Spec-Vibe-Coding/SKILL.md" ~/.claude/skills/spec-vibe-coding.md
```

### Option 2: Per-project install

Installs the skill only for a specific project.

```bash
# From your project root
mkdir -p .claude/skills
cp "path/to/Spec-Vibe-Coding/SKILL.md" .claude/skills/spec-vibe-coding.md
```

> Claude Code picks up skills from `~/.claude/skills/` (global) and `.claude/skills/` (project-local).

---

## Usage

Just describe your idea naturally in Claude Code:

```
> I want to build a tool that helps freelancers manage invoices
```

```
> I need an app for tracking my gym workouts
```

```
> Help me plan a multiplayer word game
```

Spec Vibe Coding triggers automatically and walks you through each design phase. You can go through them in order or jump directly to any phase.

### Quick-start phrases

| You say | What happens |
|---------|-------------|
| `I want to build...` | Starts the project blueprint |
| `requirements` / `PRD` | Jumps to requirements phase |
| `architecture` / `tech stack` | Jumps to system design |
| `UI` / `interface design` | Jumps to UI/interface design |
| `let's start coding` / `tasks` | Generates development task prompts |
| `quality check` | Runs consistency review across all docs |
| `skip` / `next` | Moves to the next phase |
| `progress` / `status` | Shows overall progress across phases |

---

## Phase breakdown

### Phase 0 — Project blueprint
Turns a vague idea into a structured project blueprint: problem statement, target users, core features, tech direction, and estimated complexity.

### Phase 1 — Requirements (PRD)
Produces a complete product requirements doc covering user personas, feature list with acceptance criteria, core user flows, constraints, and success metrics.

### Phase 2 — System design
Translates requirements into a technical architecture: tech stack recommendation with tradeoffs, component diagram, data model, API design, and third-party services.

### Phase 3 — UI / interface design
For UI projects: page map, user flows, page state matrix (normal / empty / loading / error), layout descriptions, design direction, and component inventory.

For non-UI projects (CLI, API, library): interface inventory, interaction flows, input/output specs, state matrix, and error message drafts.

### Phase 4 — Development tasks
Breaks the project into 1–2 hour tasks, each with a self-contained AI coding prompt you can paste directly into Claude Code or any other AI tool. Every prompt includes context, prior work, data models, API spec, UI spec, constraints, acceptance criteria, and out-of-scope boundaries.

### Phase 5 — Quality check
Cross-references all documents: coverage check (every PRD feature has matching architecture, UI, and tasks), consistency check (field names match across docs), completeness check (no missing acceptance criteria), and scope check (is the task list realistic for your timeline?).

---

## Output structure

After running through Spec Vibe Coding, your project will have:

```
your-project/
├── .spec-vibe/
│   ├── 00-blueprint.md        ← Project blueprint
│   ├── 01-requirements.md     ← Requirements (PRD)
│   ├── 02-system-design.md    ← System design
│   ├── 03-ui-design.md        ← UI / interface design
│   ├── 04-dev-tasks.md        ← Development tasks & AI prompts
│   └── 05-quality-report.md   ← Quality check report
├── src/
│   └── ... (your code)
└── ...
```

These files are the design source of truth for your project. When you get confused during development ("what exactly should this feature do?"), check `.spec-vibe/` for the answer.

---

## Core principles

**Design before code** — A few hours of structured thinking saves days of rework. The design documents give your AI coding tools the context they need to do their job well.

**Learn by doing** — You don't need to know what a PRD or system architecture is. Spec Vibe Coding guides you through the process and you'll pick up professional software design thinking along the way.

**Don't block, guide** — You can skip any phase or jump ahead at any time. The quality check will catch anything important that was missed. Progress beats perfection.

**Language follows you** — All documents and responses are generated in whatever language you use. Speak Chinese, get Chinese docs. Speak English, get English docs.

**Keep documents alive** — When you add a feature mid-project, Spec Vibe Coding proactively notes which downstream documents need updating.

---

## References

The `references/` directory contains supporting material used when building this skill:

- `ai-guidance.md` — Principles for designing AI-friendly software specs
- `quick-reference.md` — Condensed phase reference

---

## License

MIT — see [LICENSE](LICENSE).
