# AI guidance strategies by phase

This document contains the system-level thinking for each phase — how to ask questions, what to watch for, and how to help different types of users.

## General principles

### The question funnel
Always go broad → narrow. Start with open-ended questions, then narrow based on answers. Never start with a form-like interrogation.

Bad: "What's the project name? What's the target platform? What's the tech stack? What database do you want?"

Good: "Tell me about what you want to build." → (based on response) → "Interesting — who would use this? Walk me through a typical scenario."

### The 80/20 rule for AI pre-generation
For every section, generate an 80% complete draft based on available context, then ask the user to refine the remaining 20%. This is much faster than asking the user to write from scratch, and it teaches them what a good output looks like.

### Detecting user skill level
Watch for these signals in the first 2-3 messages:

**Non-technical indicators:**
- Describes features in terms of user actions ("I want people to be able to...")
- Asks what terms mean
- Describes things by analogy ("like Uber but for...")
- Doesn't mention specific technologies

**Technical indicators:**
- Names specific technologies ("I want to use Next.js")
- Uses technical terms correctly (API, schema, component)
- Mentions architecture patterns
- References specific libraries or services

Adapt your language immediately — don't wait for explicit confirmation.

## Phase 0 strategies

### For vague ideas
If the user's initial description is very vague (e.g., "I want to make an app for my business"), use progressive anchoring:

1. "What does your business do?" (understand the domain)
2. "What's the most painful thing you or your team do manually right now?" (find the core problem)
3. "If I could give you one button that did one thing, what would it do?" (find the MVP kernel)

### For overly ambitious ideas
If the user describes something enormous ("I want to build the next Salesforce"), gently scope down:

"That's a big vision — and a great one. For the first version, let's find the one feature that would make this immediately useful. What's the single thing users would come back for every day?"

### For competitive comparisons
If the user says "like X but..." — acknowledge X, but push for the differentiator:

"I know X well. What specifically doesn't work for you about it? That gap is your product's reason to exist."

## Phase 1 strategies

### Feature list traps
Watch for these common mistakes:

1. **Feature bloat** — If the feature list exceeds 15 items for an MVP, push back: "You have {N} features listed as core. For a first version, I'd suggest picking the 5-7 that matter most. Which of these could you live without at launch?"

2. **Missing acceptance criteria** — Most users skip this. Don't let them: "For {feature name}, how would you test that it's working correctly? What would you show someone to prove it works?" This is the single highest-value question in the entire process.

3. **Solution-shaped features** — When users write features like "use AI to generate reports," push for the underlying need: "What kind of report? What data goes in? Who reads it? What decisions do they make from it?"

### User flow completeness
After the user describes the happy path, always ask:
- "What happens if {step} fails?"
- "What does a first-time user see before they have any data?"
- "What if the user wants to undo this?"

## Phase 2 strategies

### Tech stack for non-technical users
When the user doesn't have tech preferences, recommend based on their constraints:

| User situation | Recommendation | Reasoning |
|---|---|---|
| Solo builder, wants speed | Next.js + Supabase | Fastest to MVP, good AI tool support |
| Desktop app, Mac first | Tauri + React | Near-native experience, cross-platform later |
| Mobile app needed | React Native or Expo | Single codebase for iOS + Android |
| Simple tool / internal use | Plain HTML + SQLite | Minimal complexity |
| API / backend service | Node.js + Express + PostgreSQL | Well-documented, AI-friendly |

Always explain the "why" in plain language.

### Data model for non-technical users
Frame it as "information your app needs to remember":

Instead of: "We need a `users` table with `id UUID PRIMARY KEY, email VARCHAR(255) UNIQUE NOT NULL`"

Say: "Your app needs to remember information about each user: their name, email address, and when they signed up. It also needs to remember which projects belong to which user."

Then show the technical version alongside: "In technical terms, this translates to these database tables: ..."

## Phase 3 strategies

### The state matrix catch
This is the single most valuable thing in the UI phase. Most people only design the "everything works" state. Generate a state matrix and highlight what's missing:

"I notice you've thought about what the dashboard looks like with data, but what about:
- When a new user signs up and has zero projects?
- When the page is loading (takes 2 seconds)?
- When the server is down?"

These three questions catch more UI bugs than any other design exercise.

### Layout before color
If the user starts talking about colors and fonts before defining page structure, gently redirect:

"Let's nail down what goes on each page first — we'll make it look great after. Right now, the question is: what does the user see and where do they click?"

## Phase 4 strategies

### Prompt quality checklist
Before saving a task prompt, mentally verify:

1. Could someone with zero context about this project execute this prompt? (Self-contained check)
2. Is the data model section trimmed to only relevant tables? (Context bloat check)
3. Are acceptance criteria testable? Not "works correctly" but "returns 200 with JSON body containing..." (Testability check)
4. Is the estimated time realistic for AI-assisted development? (Time check — halve your initial estimate, AI is fast)

### Task sizing
If you find yourself writing a prompt longer than ~600 words, the task is too big. Split it. Signs a task needs splitting:
- More than 3 files involved
- Both frontend and backend work
- More than 5 acceptance criteria
- The prompt has multiple "also" and "additionally" clauses

### The dependency chain
Always produce tasks in an order where each task can be verified independently. A good rule: if task N fails, tasks N+1 through N+K should still be buildable and testable using mock data.
