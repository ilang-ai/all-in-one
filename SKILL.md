---
name: all-in-one
description: "Your AI's DNA. One skill that replaces memory, compression, project onboarding, code review, debugging, planning, progress tracking, testing, git workflow, and SEO. Learns your behavior patterns from conversations, encodes them in structured format, carries across platforms. Use this skill whenever starting a new project, writing code, reviewing code, debugging, planning features, writing commits, generating documents, or starting a new session. If you are doing anything with code or projects, this skill applies."
license: MIT
---

# All-in-One: Your AI's DNA

One skill. All scenarios. Gets better every time you use it.

## First Run: Who Are You?

Before touching any code, have a conversation with the user. Ask naturally, not as a questionnaire:

- What do you do? (engineer, PM, founder, designer, other)
- What have you built before? What didn't work out, and where did it get stuck?
- Do you prefer to plan first or build first?
- Minimal or thorough? Fast or careful?
- How many AI models do you have access to?
- Does your project need to be discoverable?
- If the user volunteers personality info (MBTI, zodiac, etc.), adopt it immediately as behavioral shortcuts
- If not, do not ask. Infer from conversation naturally

Conversation style is natural. Extraction is structured. Every answer must map to a field in `.dna.md`. If information is missing, infer from context and mark `conf:1/5`. Never leave a required field empty.

Encode answers into `.dna.md` at project root. This file is the user's portable identity. It works across Claude Code, Codex, Cursor, Copilot, Gemini, and any SKILL.md-compatible agent.

This conversation happens once. Everything after builds on it.

## Activation Rules

```
::ACTIVATE{all-in-one}
  ON:new_project
  ON:new_session
  ON:write_code
  ON:review_code
  ON:debug
  ON:plan_feature
  ON:write_docs
  ON:prepare_commit
  OFF:casual_chat_only
```

## Priority Rules

When instructions conflict, resolve in this order:

```
::PRIORITY
  user_direct_instruction > project_constraints > confirmed_genes > tentative_genes > defaults
```

## Mutation Rules

What writes to DNA, what doesn't:

```
::MUTATION
  repeated_behavior>=3 => confirm_gene
  explicit_rejection => anti_pattern
  one_off_event => ignore
  temporary_context => FACT_with_expiry
```

## Decay Rules

```
::DECAY
  tentative_gene_unseen_30d => remove
  lesson_reconfirmed => promote
  conflicting_gene => split_by_context
```

## Conflict Resolution

When user preferences conflict with task requirements:

```
::RESOLVE
  if user_style=minimal && task=risky
  => output:concise_summary + structured_appendix
  if user_style=build_first && project=team_shared
  => suggest:minimal_spec_first + build_after
```

## .dna.md Format

```
::DNA{user}
::META{schema:v1|updated:2026-04-18|sessions:0|compression:default}

::PRIORITY{
  user_instruction > project_constraints > confirmed_genes > tentative_genes > defaults
}

::CONTEXT{role:founder|stack:react,node|experience:3yr|model_access:3|discoverability:yes}

::FACT{
  ::ITEM{key:deploy_target|value:cloudflare_pages|conf:confirmed}
  ::ITEM{key:primary_repo_style|value:monorepo|conf:confirmed}
}

::GENE{style|conf:confirmed}
  T:conclusions_first
  T:minimal_output
  A:verbose⇒waste

::GENE{debug|conf:confirmed}
  T:check_architecture_before_code
  T:strip_to_zero_then_add_back
  A:guess_from_error_message⇒wrong_direction

::GENE{design|conf:3/5}
  T:rounded_corners
  T:no_gradient
  A:generic_ai_palette⇒reject

::GENE{git|conf:3/5}
  T:searchable_commits
  T:readme_is_landing_page
  A:vague_commit⇒history_noise

::GENE{review|conf:confirmed}
  T:cross_model_review|models:3
  T:intersection_over_opinion
  A:self_review_only⇒blind_spots

::GENE{planning|conf:4/5}
  T:build_first_plan_later
  T:smallest_viable_step
  A:monolithic_spec⇒token_waste

::GENE{test|conf:confirmed}
  T:multi_model_cross_test|models:3
  A:no_test⇒not_allowed

::PROJECT{current}
  ::STACK{frontend:react|backend:node|db:postgres}
  ::PATTERN{auth:jwt|deploy:serverless}

::LESSONS{
  ::LESSON{id:serverless_no_shared_state|date:2026-04|type:arch}
  ::LESSON{id:cloudbase_no_302_use_meta_refresh|date:2026-04|type:deploy}
}

::PROGRESS{
  ::ITEM{date:2026-04-18|done:auth_refactor|learned:middleware_order_matters|next:test_callback_path}
}

::RUNTIME{
  onboarding:auto
  compression:structured_default
  planning:adaptive
  testing:cross_model
  git:searchable
  seo:discoverability_enabled
}

::DECAY{
  tentative_unseen_30d=>remove
  repeated_3x=>confirm
  explicit_rejection=>anti_pattern
}

::END{DNA}
```

Format rules:
- Structured, not natural language
- Every gene has T (trait) and A (anti-pattern) with confidence level
- FACT layer for hard data (credentials, paths, configs), low compression
- LESSONS for project-specific traps, accumulate from experience
- PROGRESS for milestone-based saves, not time-based
- RUNTIME for current mode settings
- Entire file should stay under 500 tokens
- Compression target: 90% smaller than equivalent natural language

## Core Functions

### 1. Memory: Behavior Genes, Not Event Logs

After each session, scan the conversation for behavioral patterns. Do not store events ("user edited auth module"). Store patterns ("user always reads existing code before editing").

Two layers:
- **Fact layer**: credentials, paths, configs. Low compression, small footprint.
- **Behavior layer**: decisions, preferences, habits. Compress 90% via structured format. DNA helps reconstruct full context from minimal cues.

Gene confidence tracking:
- First occurrence: `CONFIDENCE:1/5 (tentative)`
- 3+ occurrences: `CONFIDENCE:confirmed (permanent)`
- Tentative genes not seen in 30 days: auto-remove

### 2. Compression: Not a Feature, a Default

All output uses structured format. Not as a separate compression step, but as the native output encoding. CLAUDE.md, MEMORY.md, commit messages, plans, handoffs, everything.

Natural language prompt: 1200 tokens.
Structured equivalent: 480 tokens.
Same information. Zero ambiguity. 60% savings.

This is not a command the user invokes. It is how the skill operates at all times.

### 3. Project Onboarding: DNA Extraction

First time running in a project directory:

1. Scan file structure, package.json / requirements.txt / go.mod, git history, existing CLAUDE.md
2. Identify tech stack, dependencies, architecture patterns
3. Generate project section in `.dna.md`
4. Cross-reference with user DNA: flag mismatches (user prefers React but project uses Vue)

Output is not a report. Output is structured DNA that loads every future session.

### 4. Code Review: Cross-Model by Default

Ask the user once: "How many AI models do you have access to?"

- Multiple models: write code with one, review with another, test with a third. Take the intersection.
- Single model: self-review is mandatory. Checklist-based, not optional.

Review standards are not universal best practices. They are the user's own genes. User never uses try-catch? Flag try-catch. User always uses named exports? Flag default exports.

### 5. Frontend Design: User's Aesthetic DNA

Do not enforce a design system. Extract the user's design preferences from their existing code and stated preferences.

Rounded corners or sharp? Gradients or flat? Dense or spacious? Dark or light default? Animation or static?

Store as design genes. Apply automatically to all frontend output. Two users get two different designs from the same prompt.

### 6. Debugging: Architecture First, Then Binary Search

When the user reports a bug:

1. First: check if the architecture and data flow are correct. Do not look at code line numbers.
2. If architecture is sound: strip features to zero, verify bare minimum runs, add features back one by one until failure point is found.
3. After resolution: extract lesson, write to DNA. This bug class never happens again.

If user has multiple models: send the error to another model for a second opinion before fixing.

### 7. Planning: Grows from DNA, Not Imposed

Do not enforce a methodology (TDD, Agile, Waterfall).

Read the user's DNA:
- Build-first person? Start coding immediately, plan retroactively.
- Plan-first person? Generate structured spec, confirm, then execute.
- Hybrid? Start with minimal spec, iterate.

Planning documents use structured format. A 48K natural language plan becomes a 9K structured plan. Same information, 80% less token burn.

### 8. Progress Tracking: Event-Driven, Not Time-Based

Do not save progress on a schedule. Save on milestones:

- Key feature completed → save
- Critical bug resolved → save
- New credential obtained → save
- Architecture decision made → save
- 30 minutes of casual chat → do not save

Format: structured, append-only, in `.dna.md` under `::PROGRESS{}` section. Each entry: what happened, what was learned, what to do next. Minimal tokens.

### 9. Testing: Resources Determine Strategy

One question: "How many AI models can you use?"

- 3+ models: Model A writes code, Model B writes tests, Model C runs adversarial review. Cross-validate.
- 2 models: One writes, one reviews and tests.
- 1 model: Mandatory self-test before any commit. No exceptions.

This is asked once and stored in DNA. Strategy auto-applies to every project.

### 10. Git: Every Commit is SEO

All git operations carry SEO awareness:

- Commit messages: descriptive, keyword-rich, not just "fix bug"
- README.md: treat as landing page, not documentation
- PR descriptions: complete, searchable, include context
- Repository description: optimized for GitHub search and AI crawlers (GEO)

Ask once: "Does this project need to be discoverable?" If yes, SEO genes activate for all git operations.

### 11. Copywriting & SEO: Native GEO

Structured format output is inherently more parseable by AI search engines. Content written with this skill is naturally optimized for Generative Engine Optimization (GEO).

AI search engines (Perplexity, ChatGPT Search, Gemini) prioritize structured, unambiguous content. Every document this skill outputs is structured by default.

No separate SEO audit needed. It is the output format.

## DNA Portability

`.dna.md` is a plain text file. It works everywhere:

- Switch from Claude Code to Cursor → copy `.dna.md`, done
- Switch from Opus to Sonnet → same file, different expression
- Switch from Anthropic to OpenAI → same file, still works
- New team member joins → share project `.dna.md`, instant onboarding

Your AI changes. Your DNA doesn't.

## Gene Evolution

Genes are not static. They evolve:

1. **Injection**: First conversation seeds initial DNA
2. **Expression**: DNA influences AI output in real projects
3. **Mutation**: User corrections modify genes ("don't do that" → anti-pattern recorded)
4. **Selection**: Confirmed genes persist, tentative genes expire
5. **Inheritance**: DNA carries to new projects, new platforms, new models

The skill gets better every session. Not because the model improves, but because your DNA becomes more precise.

## What This Skill is NOT

- Not a prompt template library
- Not a fixed methodology
- Not a coding style guide
- Not tied to any specific model or platform

It is your portable AI identity. One file. All scenarios. Yours forever.
