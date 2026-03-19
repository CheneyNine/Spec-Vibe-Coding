# Spec Vibe Coding — Installation & Usage Guide

## What is this

Spec Vibe Coding is a Claude Code skill that guides you through professional software design before writing a single line of code. All design documents are saved as markdown files in the `.spec-vibe/` directory of your project.

## Installation

### Option 1: Copy to the Claude Code skills directory

```bash
# Locate your Claude Code skills directory
# Usually at ~/.claude/skills/ or .claude/skills/ in your project root

# Copy the skill folder
cp -r spec-vibe-coding-skill ~/.claude/skills/spec-vibe-coding
```

### Option 2: Install locally in your project

```bash
# Create the skills directory in your project root
mkdir -p .claude/skills

# Copy the skill
cp -r spec-vibe-coding-skill .claude/skills/spec-vibe-coding
```

## Usage

In Claude Code, just describe your idea naturally:

```
> I want to build a tool that helps freelancers manage invoices
```

Spec Vibe Coding will trigger automatically and guide you through:

1. **Project blueprint** — Structure your idea
2. **Requirements (PRD)** — Define what to build, for whom, and how to verify
3. **System design** — Decide on tech stack and data architecture
4. **UI/Interface design** — Plan screens, layouts, and interaction flows (or CLI/API interfaces for non-UI projects)
5. **Development tasks** — Break down into executable tasks with self-contained prompts
6. **Quality check** — Cross-reference all documents for consistency

Each phase produces a markdown file in `.spec-vibe/`:

```
your-project/
├── .spec-vibe/
│   ├── 00-blueprint.md        ← Project blueprint
│   ├── 01-requirements.md     ← Requirements (PRD)
│   ├── 02-system-design.md    ← System design
│   ├── 03-ui-design.md        ← UI / interface design
│   ├── 04-dev-tasks.md        ← Development tasks & prompts
│   └── 05-quality-report.md   ← Quality check report
├── src/
│   └── ...(your code)
└── ...
```

## Common commands

| You say | What happens |
|---------|-------------|
| "I want to build..." | Start project blueprint |
| "requirements" / "PRD" | Enter requirements phase |
| "architecture" / "tech stack" | Enter system design phase |
| "UI" / "interface design" | Enter UI/interface design phase |
| "let's start coding" / "tasks" | Generate development tasks |
| "quality check" | Run consistency review |
| "skip" / "next" | Jump to next phase |
| "progress" / "status" | Show overall progress |

## Core principles

**Design before code** — AI coding tools are great at writing code, but they need good instructions. Spec Vibe Coding helps you think through the important decisions before you start building.

**Learn by doing** — You don't need to know what a PRD or system architecture is. Spec Vibe Coding guides you through the process with questions and suggestions — you'll pick up professional software design thinking along the way.

**Documents as source of truth** — The markdown files in `.spec-vibe/` are the design source of truth for your project. When you get confused during development ("what exactly should this feature do?"), come back to these documents for the answer.

**Language follows you** — All documents and responses are generated in the same language you use. Speak Chinese, get Chinese docs. Speak English, get English docs.
