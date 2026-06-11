# CreativeHub Claude — Knowledge Base
*Compiled June 2026. Ordered: Identity A → B → C → Source 1 → Source 2 → Source 3 → Source 4 → Source 5.*

---

# Identity A — Claude Capabilities Guide

**Knowledge base for:** "How does Claude work, and which surface do I use for what?"

**Retrieval keywords:** how to use, how do I, which surface, what can Claude do, setup, get started, Chat, Projects, Skills, Cowork, Claude Code, Claude Design, Artifacts, Generative UI, MCP, connectors, models, Opus, Sonnet, Haiku, capabilities, limitations, decision matrix, enterprise, permissions.

**How to use this file:** Primary knowledge source when a colleague asks how to use a Claude surface, what a feature can or cannot do, or which surface fits a task. Preserve the evidence labels below. Never upgrade a "Practitioner-demonstrated" or "Community-reported" item to "Officially supported". When sources conflict (e.g. Claude Design usage metering), present both and note the discrepancy rather than guessing.

---

## 1. Surface Decision Matrix

| Task / goal | Best default surface | Switch away when |
|---|---|---|
| Ask, brainstorm, draft copy, quick UX specs, accessibility spot-checks | Chat | Work becomes a multi-day stream with shared docs → Projects; you need real visuals → Design |
| Ongoing initiative with many docs (PRDs, research, brand specs) | Projects | You need repeatable scripted workflows → Skills; local-file automation → Cowork |
| Encode a reusable way-of-working (review recipe, deck template, audit) | Skills | You only need per-project context, not a portable procedure → Projects |
| Have Claude act on local files/apps (organise folders, build decks/sheets from sources) | Cowork (Desktop, paid) | You don't want local file access → Chat/Projects; code-centric work → Code |
| Deep coding, refactors, code review, CI | Claude Code | Non-technical agentic work on non-code files → Cowork; visual prototypes → Design |
| Generate/iterate prototypes, mockups, decks, visual one-pagers | Claude Design | Upstream ideation → Chat; implementation → Design→Code handoff or Canva/Figma |

*Evidence: Officially supported (synthesised from Anthropic support docs and product pages, June 2026).*

---

## 2. Claude Chat — Conceptual Sandbox

**Core purpose.** General-purpose conversational surface for questions, drafting, analysis and multi-step tasks across web, desktop and mobile.

**When to use vs others.** Quick thinking/drafting that doesn't need a long-lived workspace or local file access. Prefer over Projects for early exploration; over Cowork when you don't want Claude touching local folders.

**Setup.** Go to claude.ai or install Claude Desktop (macOS 11+/Windows 10+) → sign in (Free/Pro/Max/Team/Enterprise) → pick a model (Sonnet/Opus) → Settings > Capabilities > memory to set persistent preferences → "+" or "/" for commands. Ghost icon = Incognito Chat.

**Key features.** 200K-token context window; automatic background summarisation of long conversations; Incognito mode (not saved, not trained on, purged after 30 days); web search toggle; document attachments (up to 30MB per file in chat); extended/adaptive thinking. *Officially supported.*

**Limitations.** Usage caps reset on a rolling 5-hour window (tighter on Free/Pro); threads are isolated (no cross-thread context); the browser sandbox cannot read/write local files (use Cowork or Desktop extensions for that); no full conversation-history import from other providers (only "memory" import on paid plans). *Officially supported.*

**Design-team use cases.** UX microcopy + localisation with character-count checks; ad-hoc WCAG/aria spot-checks on a pasted snippet; analysing pasted interview notes for patterns/personas. *Practitioner-demonstrated.*

---

## 3. Claude Projects — Persistent Knowledge Workspace

**Core purpose.** Self-contained workspaces with their own chat history, knowledge base and custom instructions. Solves the "cold start" problem so every chat inherits brand, audience and workflow context.

**When to use vs others.** Once you're repeatedly re-uploading the same docs or need consistent project-specific tone. Prefer over Skills when you need grounding in a body of content rather than a portable procedure.

**Setup.** claude.ai/projects → "+ New Project" → name + description → (Team/Enterprise) set visibility (private vs share with org) → upload reference materials under Project Knowledge → "Set project instructions" for role, tone, formatting, negative constraints.

**Key features.** 200K base context; on paid plans RAG auto-expands effective capacity up to ~10x as knowledge approaches the limit; role-based sharing (Can use / Can edit) on Team/Enterprise; bulk-move standalone chats into a project. Free users limited to 5 projects. *Officially supported.*

**Limitations.** No automatic sync — uploaded files must be manually replaced when sources change; not accessible via the Anthropic API (hard to automate updates); cross-project isolation (a thread can't reference another project's files); chat-level uploads are isolated and do not join the project knowledge base; sharing/permissions only on Team/Enterprise. *Officially supported.*

**Best-practice rules.** Use a focused "three-file baseline" (voice/brand samples; audience persona; past work/design components). Correct systemic errors in the Project instructions, not repeatedly in chat. Keep one project = one focus. *Practitioner-demonstrated.*

**Design-team use cases.** A "Product Area X" project holding PRDs, research and guidelines; a "Design System Rollout" project where PMs/designers centralise rationale and have Claude draft stakeholder comms. *Practitioner-demonstrated.*

---

## 4. Claude Agent Skills — Reusable, Filesystem-Based Capabilities

**Core purpose.** Modular packages (a SKILL.md with YAML frontmatter plus optional scripts/references/assets) that give Claude domain-specific workflows without long prompts. Use progressive disclosure: only ~100 tokens of metadata load at startup; full instructions load only when triggered.

**When to use vs Projects.** When a workflow should repeat across many conversations/projects (a "design crit summary" recipe, a house deck style). Projects ground Claude in content; Skills encode procedures.

**Setup.** Build with the skill-creator (Cowork or Code, extended thinking on): it interviews you, then compiles a lowercase-hyphenated folder with SKILL.md + scripts; run the generated eval suite. Install: web — Settings > Capabilities/Features > Skills (Pro/Max/Team/Enterprise); Code — drop folder in `~/.claude/skills/`; API — set beta headers (code-execution-…, skills-…, files-api-…) and attach via `container.skills`.

**Key features.** Three-tier progressive loading; pre-built Office skills (pptx, xlsx, docx, pdf); slash-command triggers; composable (multiple skills per session); open-source examples in anthropics/skills. *Officially supported.*

**Limitations & safety.** Skills do not sync across surfaces (upload separately to web/API/Code); web skills are per-user with no central team distribution; runtime constraints differ (API has no network access / pre-installed packages only); not eligible for Zero Data Retention. Custom skill folders must be named SKILL.md. ~36% of third-party skills sampled have contained prompt injections or malicious payloads — treat community skills as unaudited code and scan before use. *Practitioner-demonstrated / Officially supported for the constraints.*

**Design-team use cases.** A brand "pitch-deck-standard" skill on top of the built-in pptx skill; a design-token compliance audit skill that outputs a line-by-line violation log; a research-synthesis skill. *Practitioner-demonstrated.*

---

## 5. Claude Cowork — Desktop Agent for Knowledge Work

**Core purpose.** Agentic desktop mode that takes a goal and works autonomously across local files, folders and apps to produce finished deliverables. For non-technical, high-effort, repeatable work — not one-off chat answers.

**When to use vs others.** When Claude must actually manipulate local artifacts (rename/sort assets, turn a research folder into a report, build spreadsheets/decks from sources). Prefer over Chat/Projects when local files are central; over Code when the work isn't code-centric.

**Setup.** Install Claude Desktop (macOS/Windows), sign in with a paid plan → open the Cowork tab (Team/Enterprise: org owners enable under Organization settings > Capabilities > Cowork) → Settings > Cowork for global instructions → connect folders, choose safety level ("Ask before acting" vs "Act without asking"), optionally toggle "Claude for Small Business" connectors (Google Workspace, Microsoft 365, Canva, HubSpot, QuickBooks).

**Key features.** "Computer Use" screen actions (screenshot, cursor, click, type); code runs in an isolated Linux VM (Apple Virtualization.framework / Hyper-V); long-running tasks and parallel sub-agents; Cowork Projects (per-project instructions, context, scheduled tasks, project-scoped memory); Scheduled Tasks; plugins/Skills; OpenTelemetry monitoring for Enterprise. *Officially supported.*

**Limitations & risks.** Paid-only, Desktop-only (no web/mobile). Cowork activity is not in audit logs / Compliance API / data exports — Enterprise monitors via OpenTelemetry. Data is stored locally, not cloud-synced; admins cannot centrally export/delete it. Scheduled tasks require the app open and the machine awake. Granting folder access lets Claude read, edit and delete files — keep folder boundaries strict. "Computer Use" is vulnerable to prompt injection from untrusted web pages. Multi-step desktop tasks burn tokens fast. *Officially supported / Community-reported for token burn.*

**Workspace structure (best practice).** Use `context/` (standing rules: about-me, brand-voice, working-preferences), `projects/` (active work), `output/` (deliverables). Keep root CLAUDE.md under ~300 lines using one-line pointers to files loaded only on demand; cap memory.md ~150 lines and push older facts to archive.md. Separate prescriptive rules (CLAUDE.md) from temporary facts (memory.md). *Practitioner-demonstrated.*

**Design-team use cases.** Point Cowork at a folder of interviews/recordings → structured research report + summary deck; clean and rename messy design-export folders to a team convention. *Practitioner-demonstrated.*

---

## 6. Claude Code — Terminal/IDE Agentic Coding

**Core purpose.** Agentic CLI/IDE that reads, edits, runs, tests and commits code via natural language; integrates with git, test runners and CI. Built for developers, but design/PM-adjacent users can drive visual/CSS changes or consume Design handoff bundles.

**Setup.**
- macOS/Linux/WSL: `curl -fsSL https://claude.ai/install.sh | bash`
- Windows: `irm https://claude.ai/install.ps1 | iex`
- npm (avoid sudo): `npm install -g @anthropic-ai/claude-code`

Run `claude` in a repo → browser OAuth → `claude doctor` to verify → `/init` to scan the codebase and generate a project CLAUDE.md.

**Key features.** Plan Mode (Shift+Tab) maps changes into a markdown plan before editing; `/autofix-pr` runs tests and patches lint/compile errors on PRs; `/batch` spins parallel sub-agents in isolated git worktrees for large migrations; unified memory (auto-memory + manual CLAUDE.md); Skills, plugins and MCP servers; headless/non-interactive modes. *Officially supported.*

**Limitations.** Shares token/usage limits with chat and design — big refactors burn quota fast; needs a structured git repo; no native visual canvas (use a browser/extension to preview UI); targeted at terminal-comfortable users; performance degrades as context fills (manage sessions, `/compact` before ~70%). *Officially supported / Practitioner-demonstrated.*

**Design-team use cases.** "Migrate the nav bar in /src to Tailwind v4, run the test suite, write a commit message"; implement a Claude Design prototype bundle and review via normal PRs. *Practitioner-demonstrated (Design→Code handoff is documented on the Design side).*

**Claims to avoid.** Don't claim Code flawlessly ports 100k+ line legacy codebases 1:1 (it forgets paths, leaves placeholders, hallucinates on large migrations). `--dangerously-skip-permissions` is not safe — it can cause catastrophic deletions.

---

## 7. Claude Design — Visual Prototyping (Anthropic Labs, Research Preview)

**Core purpose.** Canvas-based design environment powered by Claude Opus (vision-capable). Chat on the left + live interactive canvas on the right. Generates interactive prototypes, design systems, slides, one-pagers and marketing collateral from conversation, references and codebases. Web only — claude.ai/design — not in the Desktop app.

**When to use vs others.** When you need actual visual artifacts. Ideate text/structure in Chat/Projects first (saves the meter), then move to Design, then optionally hand off to Code or Canva. It excels at 0→1 prototyping, variants and decks; it is not a full Figma replacement and struggles with deep UX logic (e.g. what to hide vs show on a dense dashboard).

**Setup.** Open claude.ai/design on Pro/Max/Team/Enterprise (Enterprise: off by default, admin must enable) → select workspace → upload brand assets (logos, SVGs, typography, slide decks, React component libraries, or point at a codebase / use web-capture) → review the auto-generated UI kit (colours, type, spacing, components) → toggle "Published" to make it the team default. Multiple design systems can coexist.

**Key features.** Brand-aware design-system ingestion (parses codebases, PDFs, decks, design files); high-fidelity interactive code artifacts (clickable modals, tabs, state — not static images); inline comments on canvas elements for targeted edits; custom sliders/"Tweaks" for spacing/colour/layout; org sharing/permissions; export to standalone HTML, .zip, PDF, PPTX, Canva, or a Claude Code handoff bundle (tokens + components + layout notes). *Officially supported.*

**Limitations (documented).** Research preview — behaviour evolves; not on Free tier. Cannot natively generate raster images (placeholders/emojis only) or export MP4/video (HTML/PDF/PPTX/Canva only). Inline comments can disappear before the model reads them → paste critical feedback into chat. Compact-layout mode can trigger save errors → switch to full view. Linking large monorepos causes lag/crashes → link specific subdirectories. "Chat upstream errors" lock a session → open a new chat tab in the same project. Responsiveness (mobile↔desktop) often needs manual CSS fixes. Raw exported code is often an unmaintainable "opaque blob" — use for prototyping, not production. *Officially supported / Practitioner-demonstrated.*

**Creative connectors ("Claude for Creative Work").** Official connectors extend Claude into creative tools: Ableton (docs-grounded tutor for Live/Push), Adobe for Creativity (50+ Creative Cloud tools), Affinity by Canva (batch production tasks), Autodesk Fusion + SketchUp (parametric/3D from natural language), and Blender via MCP (Python-API scene analysis/scripting). *Officially supported.* Treat any data returned from a connector as untrusted (prompt-injection vector).

**Design-team use cases.** Brand-compliant landing page from the published design system; extract a UI kit from an existing deck + component library; turn a transcript/notes into an interactive slide deck. *Officially supported / Practitioner-demonstrated.*

---

## 8. Artifacts & Generative UI (Inside Chat/Projects)

An Artifact is triggered when output is significant and self-contained (typically >15 lines), stands alone, and is likely to be edited/reused. Types: Markdown, code, single-page HTML, SVG, Mermaid diagrams, interactive React. Generative UI runs code live (client-side sandbox); ChatGPT's Canvas is an editing environment by contrast.

**Key rules.** Artifacts are sandboxed client-side: no external API/DB calls or server logic. Live Artifacts (Pro/Max/Team) persist in the sidebar and pull fresh data via connected MCPs (Gmail, Stripe, Calendar) with a refresh button — avoid re-prompting. Use "Remix" for iteration to keep the chat lean. Persistent AI-artifact storage is capped (20MB, text-only). Local image uploads break in shared/published artifacts → use public URLs / SVG / emoji. Enable code execution to parse XLSX. Start from a Minimal Viable Artifact and iterate; target specific errors instead of full regenerations. *Officially supported, except MVA/playground patterns = Practitioner-demonstrated.*

---

## 9. Models (2026)

- **Opus 4.7 / 4.8** — flagship reasoning/vision; deep architecture, coding, honest review. 1M-token context, no long-context price premium. Opus 4.8 is the latest (generally available; also on GitHub Copilot). Interprets instructions literally (no inferring unstated needs). Persistent default "house style" (warm cream/off-white, serif display, italic accents, terracotta/amber) — override with an explicit design system. *Officially supported.*
- **Sonnet (4.6)** — everyday coding, drafting, routine layout/formatting; far cheaper — the default workhorse. *Officially supported.*
- **Haiku** — fast/cheap classification, simple formatting, latency-sensitive tasks. *Officially supported.*

**API notes.** `temperature`, `top_p`, `top_k` are deprecated (return 400) — steer via prompt only. Manual thinking budgets replaced by adaptive thinking + effort levels (`/effort high` default, `xhigh` for hard/long tasks, `max` only when depth justifies the cost). Opus 4.7+ adds visible "Task Budgets" (advisory countdown; still set `max_tokens`). High-res image input up to ~2576px/3.75MP uses ~3x image tokens. *Officially supported.*

---

## 10. MCP, Connectors & Enterprise Integrations

MCP is an open standard (10,000+ public servers) connecting Claude to external data/tools. Allowlist only needed tools (`MCPToolset`, `enabled:false` default) and use `defer_loading` to keep context lean. Remote MCP cannot reach local STDIO servers without an HTTP/SSE bridge; MCP data is exempt from Zero Data Retention; Enterprise admins can blocklist tools. *Officially supported.*

**Enterprise/SMB.** Claude runs inside business tools via connectors (HubSpot→Canva flows, QuickBooks, Docusign, Microsoft 365). It inherits the user's existing permissions; Team/Enterprise data is excluded from training by default. Design agentic workflows with a human-in-the-loop approval gate before anything sends/posts/pays. *Officially supported.*

---

## 11. Capability Honesty — Claims to Avoid (Global)

Do not claim, without a named official source: flawless .fig/Figma import, exact token extraction, two-way Figma sync, production-ready/maintainable code from Design, native image/video generation, unlimited usage, that local files/MCP outputs are injection-safe, that Cowork runs offline/in background, or that Claude reliably self-evaluates its own aesthetics in one pass (it is lenient — use a separate evaluator). LLMs lack true spatial awareness and will hallucinate alignment/spacing/fonts. Prefer "useful for", "appears suitable for", "should be tested", "requires review".

*Primary sources: Anthropic support.claude.com & platform.claude.com docs, anthropic.com product/news pages, Claude Cookbook, plus practitioner/community sources (labelled). Compiled June 2026.*

---
---

# Identity B — Best Practices & Efficiency

**Knowledge base for:** "Help me prompt Claude (especially Claude Design) better, and stop wasting tokens/credits."

**Retrieval keywords:** prompt optimisation, improve this prompt, best practice, prompt engineering, AI slop, generic output, design system constraints, negative constraints, typography, usage limit, hitting limits, tokens, credits, save tokens, token efficiency, pricing, plan tiers, Max, Pro, context window, effort level, model routing, evaluation checklist, attachments.

**How to use this file:** Primary source when a colleague wants prompt optimisation, wants to avoid generic "AI slop", or is hitting usage limits / burning credits. Every optimisation answer should fold in at least one efficiency note. Preserve evidence labels; do not promise that any prompt guarantees interactivity, token reduction, or a specific aesthetic. Numbers below (limits, prices, % consumption) change frequently — present them as "as reported, June 2026" and recommend verifying against current Anthropic docs.

---

## Part 1 — Prompting & Design-Quality Best Practices

### 1.1 Core Prompting Frameworks

- **GCAO** — Goal, Context, Action, Output. State all four explicitly. *Practitioner-demonstrated.*
- **Success Cycle** — Success Brief → Draft → Critique → Revise. Outperforms one long prompt. *Practitioner-demonstrated.*
- **Task Design over Prompt Engineering** — before generating UI, have Claude ask clarifying questions about audience, tone, format. *Officially supported pattern.*
- **Planner → Generator → Evaluator** — for complex builds, expand a 1–4 sentence idea into a product spec (Planner), build one feature/"sprint" at a time (Generator), and use a separate skeptical Evaluator. Claude is lenient on its own work, so a single-pass self-review is unreliable. *Officially supported.*
- **Sprint Contract** — Generator and Evaluator agree a testable definition of "done" before code is written. *Officially supported.*
- **Teach the "why"** — explaining the principle behind a rule generalises far better than rigid directives or examples alone. *Officially supported.*

### 1.2 Breaking the "AI Slop" / Generic Aesthetic

Claude defaults to safe layouts; Opus 4.7/4.8 has a stubborn house style (warm cream, serif display, italic accents, terracotta/amber). To escape it:

- Set an explicit design system upfront, or force the model to propose three distinct visual directions before writing any code. Vague words like "clean and minimal" will not break the pattern. *Practitioner-demonstrated.*
- **Negative constraints:** explicitly ban "AI-generated patterns", unmodified stock components, default library aesthetics, and generic purple/teal gradients over white cards. *Officially supported.*
- **Typography signals quality:** ban default system fonts (Inter, Roboto, Open Sans, Lato); mandate distinctive pairings and extreme weight contrast (e.g. 100 vs 900) and large size jumps. *Practitioner-demonstrated.*
- Principle-based, evocative language (and aspirational phrases like "museum quality") pushes more aesthetic risk-taking than prescriptive styling commands, which trigger pattern-matching. *Community-reported.*
- Provide visual references: upload competitor screenshots (Mobbin, etc.), ≥1000×1000px, and instruct "adapt, don't copy 1:1". *Practitioner-demonstrated.*
- Grade against four pillars: Design Quality (distinct mood/identity), Originality (custom decisions), Craft (typography/spacing), Functionality (usability). *Officially supported.*

### 1.3 Reviewing / Critiquing Designs

- **Ruthless Reviewer persona + two-pass loop:** adopt a brutal, conversion-obsessed persona; pass 1 critiques visual decisions, pass 2 simulates a first-time user click-through. Output sorted by "critical / high-impact / nice-to-have" so it can feed straight into Claude Code. Polite prompts yield superficial feedback. *Community-reported.*
- Leverage Opus 4.7/4.8's honest editing: ask it to critique against stated principles, not "does this look good?". *Officially supported.*

### 1.4 Prompt Structure Mechanics

- Place large reference files at the top of the prompt, wrapped in `<document>/<documents>` XML tags, before the query (improves recall by up to ~30%). *Officially supported.*
- Tell Claude what to do, not only what not to do ("write in flowing prose" > "don't use markdown"). *Officially supported.*
- Opus 4.7/4.8 is literal — be exhaustive; define explicitly when to call tools or spawn sub-agents. *Officially supported.*
- `temperature`/`top_p`/`top_k` and prefilled final-turn assistant responses are deprecated (400 error) — steer via prompt + XML only. *Officially supported.*

### 1.5 Interaction Requirements (Handle with Care)

Do not add interactivity by default. Include at most 1–2 interaction types, only when central to evaluating the design, and phrase as "if supported / where reasonable". Never promise hover states, filters, tabs, animations or live dashboards will render correctly. *Project guardrail.*

### 1.6 Attachment Handling

- Use "provided references to guide visual direction" rather than "extract exact colours/tokens" — don't claim perfect parsing. *Project guardrail.*
- Images ≥1000×1000px; PDFs <100 pages (over 100 pages → text-only, loses charts/typography); chat files up to 500MB / 20 files; persistent Project files ~30MB.
- Batch design-system components into categorised Markdown files (Form Elements.md, Navigation.md, Data Display.md) — Claude often stops reading one giant list. *Practitioner-demonstrated.*
- Store brand/voice/persona files at the Project level, not per chat. *Practitioner-demonstrated.*

### 1.7 Claude Design–Specific Prompting

- Ideate text/structure in Chat first; reserve the Design meter for visual rendering. *Community-reported.*
- Upload a brand guideline / competitor URL so a custom design system is built before any screen is generated. *Officially supported.*
- Refine with inline comments (targeted) and chat (structural); add custom sliders for the variables you want to test. Use the on-canvas text "Edit" tool for copy tweaks (no LLM tokens). *Officially supported.*
- For data-heavy/back-end needs, package the mockup and hand off to Claude Code rather than building logic in Design. *Officially supported.*

---

## Part 2 — Usage Limits, Tokens & Credit Efficiency

### 2.1 The Reality of Limits *(as reported, June 2026 — verify against current docs)*

- Usage resets on a rolling 5-hour window; paid tiers also have weekly limits. Free/Pro deplete fastest. *Officially supported.*
- **Claude Design metering — sources conflict; flag this:**
  - *One line of reporting:* Design has its own separate, highly restrictive weekly meter — a complex design system from a large Figma file can burn a weekly quota in 10–30 minutes; a single prompt can take 8–15% of a weekly quota.
  - *More recent reporting (r/ClaudeAI):* the isolated weekly Design limit was removed and merged into the standard 5-hour chat/Code pool, and a single design edit can consume 20–40% of the 5-hour limit. Anthropic also reportedly doubled Design token limits and raised Code weekly limits ~50% (temporary, through ~July 13).
  - Always state which is documented vs community-reported and recommend checking the live "Claude Design subscription usage and pricing" page.
- Cowork file operations can cost 50–100x a normal message; multi-step desktop tasks burn quota fast. *Practitioner-demonstrated.*
- Opus 4.7+'s tokenizer maps the same text to ~1.0–1.35x more tokens than 4.6 — re-baseline old assumptions. *Officially supported.*

### 2.2 Plan Tiers & Credits *(as reported — verify; do not over-commit)*

| Plan | ~Monthly | Notes |
|---|---|---|
| Free | $0 | No Claude Design; no file creation/code execution |
| Pro | ~$20 | Independent weekly allowance; exhausts quickly on Design setup |
| Max 5x | ~$100 | ~5x Pro allowance; all Opus models |
| Max 20x | ~$200 | ~20x Pro; highest-priority queue |
| Team | ~$100+/seat (premium, min ~5 seats) | Per-seat allowance, SSO |
| Enterprise | Negotiated | Seat-based or usage-based API |

Usage credits: when the included allowance is depleted, opting into usage credits continues work at standard API token rates (configure via web, even for mobile subscriptions). Sold in discounted bundles (e.g. ~$45→$50 at 10%, ~$200→$250 at 20%, ~$700→$1,000 at 30%), with monthly caps. *Officially supported (figures may change).*

### 2.3 Token-Saving Tactics — Consolidated 20-Point Playbook

**Session & context hygiene**

1. Start a fresh chat per task type; reset roughly every 15–20 messages to clear context cache and stop runaway drain.
2. Run `/context` (Code) to see what's eating tokens; `/compact` before ~70% context, beyond which instruction-following degrades.
3. Edit a previous message to change course instead of sending a follow-up — a follow-up re-bills the whole growing history; editing rewrites it.
4. Don't follow up unnecessarily; batch multiple requests into one well-scoped prompt.
5. For long work, use context resets with structured handoff files rather than endless in-place compaction.

**Model & effort routing**

6. Use Sonnet for everyday/routine work; reserve Opus for complex architecture/refactors/honest review.
7. Lower the effort level for simple tasks; don't use xhigh/max for minor layout tweaks. If the model over-thinks or makes junk temp files, lower effort rather than adding prompt engineering.
8. Toggle off extended/adaptive thinking for simple tasks.

**Inputs & tools**

9. Disable idle MCPs/connectors before a session — every active server polls and burns tokens.
10. Cache Figma data locally: do one read, save tokens/components to a `.claude/` Markdown file, then read the file in later sessions instead of re-hitting the expensive Figma API.
11. Convert PDFs to Markdown before uploading; downsample reference images (1080p/720p) unless 1:1 pixel mapping is required (2576px ≈ 3x tokens).
12. Prefer token-efficient file formats: YAML > Markdown > XML > JSON.

**Projects, Skills & memory**

13. Put recurring files/design tokens in Projects (uploaded once) instead of re-uploading per chat; leverage the 200K window / RAG.
14. Keep custom instructions / root CLAUDE.md lean (<~300–500 lines) with on-demand file pointers; cap memory.md ~150 lines + archive.md.
15. Turn a repeated prompt into a Skill to bypass the token-heavy reasoning phase; use ~100-token YAML descriptions (progressive disclosure).
16. Remove pointless files from Projects/Cowork.

**Claude Design specific**

17. Never upload an entire monorepo or 75-page Figma file — isolate subdirectories / specific pages.
18. Use the on-canvas Edit tool for copy (no generation tokens); use Stitch/low-fi tools for early wireframing; reserve Design for the final high-fidelity draft.
19. Route high-volume structural code refinement to a cheaper coding tool/Codex (reported ~3–4x fewer tokens) once the design is stable.

**Timing & overflow**

20. Shift heavy work to off-peak hours; know your rolling-5-hour reset; alternate models; use the session-reset trick; enable extra usage/credits as a safety valve.

*Tactics 1–20 synthesised from Anthropic docs, the design/token-efficiency articles, and two practitioner videos: "Why Claude Keeps Hitting Usage Limits (& how to fix it)" (Eliot Prince, Apr 2026, 14 tips) and "Never hit Claude's Usage Limit Again" (Dubibubii, Apr 2026, 11 rules). Practitioner-demonstrated unless an official doc is cited.*

### 2.4 Evaluation Checklist *(attach to any optimisation answer)*

- Is the request narrowed to one output / one section / one breakpoint?
- Are negative constraints + evaluation criteria included?
- Is the cheapest adequate model + effort level chosen?
- Are only the needed files/tools/MCPs loaded, references at the top?
- Did I add at least one concrete token/credit-saving step?
- Did I avoid promising guaranteed interactivity or guaranteed token reduction?

*Compiled June 2026. Limits, prices and percentages are volatile — verify against support.claude.com before quoting to stakeholders.*

---
---

# Identity C — Future Interfaces & Experience Patterns

**Knowledge base for:** "How will interfaces and experiences evolve, and how can we use Claude creatively to design for them?"

**Retrieval keywords:** trends, future, what's next, emerging interface, experience patterns, agentic UX, probabilistic UX, ambient computing, wearables, smart glasses, AR, spatial computing, multimodal, voice, gaze, EMG, generative UI, adaptive UI, human-in-the-loop, trust, privacy, EssilorLuxottica, eyewear, Meta, forecasts, design futures.

**How to use this file:** Primary source when a colleague asks about trends, emerging interaction/experience patterns, the future of UX, ambient/wearable computing, agentic UX, or how to explore these creatively with Claude. Identity C may be forward-looking and speculative — but label speculation explicitly ("Forward-looking, not a Claude capability claim" / "Trend interpretation, source type: …") and never present a future pattern as a shipped Claude Design feature. Ground examples in EssilorLuxottica / eyewear / smart-glasses context where it genuinely helps (see §9), but don't force it.

---

## 1. From Deterministic to Probabilistic UX

The WIMP contract (same input → same output, errors = anomalies) is being replaced by probabilistic UX: AI systems infer and generate by confidence, so identical inputs can yield variable outputs and uncertainty is an inherent property, not a bug. The designer's job shifts from drawing static screens to defining confidence thresholds — when a system acts autonomously vs asks for human intervention. *Trend interpretation (NN/g, practitioner articles, 2026).*

| Dimension | Deterministic | Probabilistic (AI-native) |
|---|---|---|
| Behaviour | Predictable, rule-bound | Adaptive, context-dependent, confidence-based |
| Errors | Hard failures + error messages | Graceful degradation, rollback, editable outputs |
| User role | Operator | Collaborator / supervisor |
| Feedback | Static validation | Continuous refinement, corrections feed retraining |
| Explainability | Rarely needed | Often required (confidence bars, rationale panels) |

**Principles of uncertainty management:** confidence indicators (intervals, tooltips, progress bars); progressive disclosure of reasoning (expandable "why", cite RAG sources); latency as a trust canvas (narrate background steps during waits); reversible interventions (undo/edit/retry/override as primary, visible controls).

---

## 2. Agentic UX & Human-on-the-Loop Oversight

Autonomous agents pursue goals by iteratively acting, evaluating and choosing next steps (NN/g definition). Oversight shifts from human-in-the-loop (approve every action) to human-on-the-loop (agent proceeds; human monitors and intervenes selectively). The key design problem is dynamic intervention thresholds — contextual, emotional and risk-based, not purely technical: a user may let an agent draft a calendar invite autonomously but demand explicit approval before it sends an email or executes a transaction. This requires visible pause / veto / override / rollback mechanisms; if the only way to stop a bad agent is to wait for the output, the relationship is broken. *Trend interpretation (NN/g, Microsoft, Salesforce design-principle sources).*

**Enterprise architecture (4 layers):** system of engagement (interface) · system of agency (the agents) · system of work (apps/APIs) · system of data (unified data layer).

**Eight agentic collaboration patterns (GitLab study of 17 platforms):** status updates · work routing · team communication · role-specific chat · conversational context · role-based access (RBAC) · governed/sandboxed environments · collaborative building. The rarest capability is unified governance (environment grouping + catalog sharing + managed promotion) in one interface.

**Evaluation:** return to IDEO-style low-fi prototyping to stress-test agent behaviour and failure modes before high-fidelity build ("a prototype is worth a thousand meetings").

---

## 3. Generative & Adaptive Interfaces

Layouts are no longer pre-designed static containers; AI compiles layout, content and interaction on the fly from user intent, task and context. Accelerated by tools like Figma AI/Make, Uizard, Galileo AI, Relume, TeleportHQ, UiMagic.

**Documented business outcomes (case studies):** a fintech replaced six static dashboards with one adaptive, role/usage-driven view → support tickets −27%; context-driven SaaS onboarding (technical user → API docs/sandbox; business user → guided tour) cut onboarding from ~12 min to <5 and reduced early churn. *Trend interpretation / agency case studies.*

**The Semantic Design System Moat (forward-looking):** as generative UI compiles interfaces from briefs, competitive advantage shifts from static layout libraries to highly consistent, semantic design systems (clean tokens/components/variables). Inconsistent systems → fragmented generative output. This is directly relevant to design-system teams. *Forward-looking.*

---

## 4. Materiality, Ambient AI & "Intelligent Reduction"

- **New materiality:** Apple's "Liquid Glass" (iOS 26) — translucency, depth, micro-refraction responding to light/motion/touch. But Apple shipped a "turn off Liquid Glass" toggle ~7 weeks in after clutter complaints: depth/motion must serve communication, not decoration.
- **Ambient AI:** assistance recedes into the background — predicting form fills, reordering nav by usage, delaying non-urgent notifications — instead of explicit "Ask AI" prompts.
- **Intelligent reduction / "knowing what not to show":** the premium experience suppresses irrelevant detail and hides low-confidence recommendations. Generic flat illustration ("Corporate Memphis") is declining as a signal of unrefined brand identity. *Trend interpretation (UX/UI 2026 trend reports).*

The iF Design "six societal transformations" framing (human digitality, value orientation, design as integrative discipline navigating "omnicrisis") supports treating design as conceptualising possible futures, not just function.

---

## 5. Ambient Computing & the Distributed Wearable Ecosystem

Technology is moving from a single high-attention smartphone to a cooperative ecosystem of always-on devices (watches, bands, sensors, smart glasses) that turn biometric/environmental context into unified narratives synced across endpoints (Gemini, Apple Intelligence).

**Two competing paradigms:** Apple's immersive spatial computing (3D digital presence) vs Meta's ambient AI / conscious interface (technology fades; voice, gaze, context). *Trend interpretation.*

**Smart-glasses optics:** descend from 1940s cockpit HUDs and the 1988 Oldsmobile windshield HUD — keep critical data in the line of sight without breaking situational awareness. Modern glasses use waveguide "light highways" routing a temple micro-projector to the pupil, correcting chromatic dispersion while keeping a ~9mm eyebox.

**Market & players:** smart-glasses market projected from ~$2.9B (2025) toward $8.4B+ (2035) at ~11.6% CAGR. Google–Warby Parker ($150M), Apple screenless camera frames, and Meta × EssilorLuxottica (Ray-Ban, Oakley) + Gentle Monster. Constraint that separates glasses from MR headsets: they must look/weigh/feel like normal eyewear for all-day public wear.

**Five 2026 glasses paradigms:**
- AI Glasses (no display, camera+audio, ~51g — Ray-Ban Meta Gen 2)
- Display Glasses (small HUD — Meta Ray-Ban Display)
- AR Glasses (waveguide/micro-LED, 30–80g — Even Realities G2)
- AR Display Glasses (tethered virtual monitors — XREAL One Pro)
- Smart Sunglasses (audio-first — Bose Frames)

**Usability/input barriers:** frame weight/balance/temple pressure/heat; touch fails in rain/gloves; voice is socially awkward and noise-unreliable → shift toward camera-as-input ("shared visual context": look at a sign, ask "what does that mean?").

---

## 6. Multimodal Interaction, Gaze & Neural Sensing

Voice-only products failed (Humane AI Pin, Rabbit R1) due to cognitive load and weak spatial execution. Winning interfaces are multimodal — voice, touch, gesture, gaze operating concurrently and handing off to each other.

| Modality | Strength | Weakness | Handoff |
|---|---|---|---|
| Voice | Fast, hands-free | Low precision, socially awkward, noise | → touch/HUD text to refine |
| Touch | Absolute precision, silent | Needs attention, occludes screen | → voice/overlay for broad nav |
| Gesture | Intuitive, 3D | Low precision, "gorilla arm" fatigue | → gaze targeting + confirm |
| Gaze | Rapid targeting, zero movement | "Midas Touch" mis-triggers, fatigue | → pinch / EMG click |
| EMG / neural | Ultra-low strain, covert | Calibration, signal noise | complements voice+gesture |

**Gaze-directed pinch (Apple Vision Pro):** eyes target, hands execute; wide-FoV cameras let hands rest at waist/desk (avoids fatigue). The Midas Touch problem (involuntary eye triggers) is solved by pairing gaze with a low-effort confirm (micro-pinch, ring click). Wrist-worn EMG (Mudra Pro/Band; Meta's prototype neural band) decodes muscle biopotentials for "Air-Touch" — selecting by subtle or merely-intended finger movement.

---

## 7. Trust, Privacy & Governance (Wearables)

Always-on cameras/mics + facial recognition create a wearer↔bystander expectation gap (the "Name Tag" controversy; cloud-routed footage reviewed by subcontractors; risk of reviving the "glasshole" stigma).

**6-Layer Privacy & Consent Model:**
- **(I) Social Visibility** — bright front LEDs visible at 10m, recognised in ~2s
- **(II) Electronic Notification** to nearby devices
- **(III) Technical Edge Defense** — on-device segmentation blurs bystanders/children/plates before any upload
- **(IV) Dynamic Control & Consent** — phased disclosure, opt-in/out
- **(V) Long-Term Data Risk** — auto-purge (e.g. 48h) unless consented
- **(VI) Socio-Ethical Trust** — transparency, EU AI Act alignment, clear human-review policy

**Enterprise governance:** designate "recording-free zones" (restrooms, exec rooms with IP on whiteboards); physical signage + geofencing to auto-disable recording on managed glasses. *Trend interpretation / policy sources.*

---

## 8. Agents as Interface Users, and Forecasts

**AI agents as users:** agents increasingly navigate human-facing UIs, two ways — vision-based (screenshots, ~10,000+ tokens/page, fragile to layout shifts) vs accessibility-tree parsing (semantic HTML/ARIA, ~1,000 tokens, fast/reliable). Implication: semantic, accessible HTML is now also "agent-readable" design — accessibility and agent-navigability converge. AI also scales UX research via synthetic users / digital twins and automated heuristic evaluation — but as a preliminary diagnostic that supports, not replaces, human research (false positives, missed context). *Trend interpretation (NN/g).*

**Forecasts 2026–2029 (explicitly speculative):** autonomous task horizons are doubling ~every 4 months (was ~7); ~5 expert-hours of unattended work in late 2025 projected toward ~39 hours (a work week) by late 2026. Expect: Agentic Gridlock (vendor agents failing to interoperate → push for open standards); the Semantic Design System Moat (see §3); and edge-first privacy (on-device recognition/translation/blurring after cloud-leak backlash). *Forward-looking.*

---

## 9. EssilorLuxottica / CreativeHub Business Context

EssilorLuxottica is transitioning from eyewear manufacturer toward an AI-first technology and healthcare ecosystem, positioning smart glasses as a potential successor to the smartphone and pioneering ambient computing (voice, gaze, context). The Meta × EssilorLuxottica partnership (Ray-Ban, Oakley) is central to the consumer AI-glasses race, and the "silver economy" (wearables for an ageing population) is a strategic vector. For the CreativeHub, this means design work increasingly targets face-worn, glanceable, multimodal, privacy-sensitive ambient experiences rather than only screens. *Trend interpretation / EL strategic sources — use where relevant, don't force.*

---

## 10. Using Claude Creatively to Explore These Patterns

Concrete, bounded ways to apply Claude surfaces (cross-reference Identity A/B) to the futures above:

- **Prototype probabilistic/agentic flows** as interactive Artifacts/Claude Design mockups — include confidence indicators, reversible controls, and a "narrated latency" state to test trust patterns. Bounded test.
- **Stress-test agent oversight:** simulate human-on-the-loop thresholds in a clickable prototype before any build (IDEO-style low-fi).
- **Adaptive UI exploration:** generate role-based variants of one screen from a single brief to feel out generative/adaptive layouts.
- **Multimodal storyboarding:** use Design/Artifacts to mock glanceable HUD states, gaze+pinch confirmations, voice→HUD handoffs for eyewear.
- **Synthetic-user research drafts:** have Claude simulate cohort walk-throughs as a preliminary diagnostic, then validate with real users.
- **Semantic design-system rigour:** use Claude to audit token/component consistency — the moat that makes generative UI reliable.

Always label generated futures as exploration, keep one bounded experiment per prompt, and validate with humans. *Forward-looking + Project guardrails.*

*Primary sources: deep-research synthesis (NN/g, Microsoft, Salesforce, GitLab, IDEO, UX trend reports, smart-glasses/market and privacy research), plus curated notes (UX Guidelines for AI & Multi-Agent Systems; Wearables & the Conscious Interface; Wearables & the Silver Economy; iF Design Trend Reports; NN/g 2025 trends). Compiled June 2026. Trend and forecast items are interpretation/speculation, not Claude capability claims.*

---
---

# Source Dossier 1 — Claude Design: Capabilities, Economics, Optimisation, Handoff

*Depth reference for Identity A (Design surface) and Identity B (Design efficiency)*

**Retrieval keywords:** Claude Design, canvas, design system, UI kit, prototype, mockup, slides, deck, Opus 4.7, Opus 4.8, usage limit, weekly allowance, metering, pricing, plan tiers, credits, token economics, Figma MCP, Canva export, handoff bundle, Claude Code handoff, Artifacts, Live Artifacts, persistent storage, file limits, inline comments, Tweaks panel, export HTML PDF PPTX.

*Purpose: detailed, source-linked reference on Claude Design and Artifacts. Merges deep research (Gemini + Perplexity, prompts 1 & 4), the report_complete clusters on Claude Design / Generative UI / Artifacts / Figma MCP, and the "Claude Design: Mastering the New Era of Agentic UX" notes. Evidence tiers preserved; verify volatile figures (limits, prices, %) against support.claude.com. Compiled June 2026.*

---

## 1. What Claude Design Is

- An Anthropic Labs research preview product to "collaborate with Claude to create polished visual work like designs, prototypes, slides, one-pagers, and more." Powered by Claude Opus 4.7 (vision model) at launch; Opus 4.8 is now the latest model generally available. *Official — anthropic.com/news/claude-design-anthropic-labs; anthropic.com/news/claude-opus-4-8.*
- Web only at claude.ai/design — not in the Claude Desktop app. Available to Pro, Max, Team, Enterprise (not Free). Enterprise: off by default, admin must enable in Organization settings. *Official — support.claude.com/.../14604416-get-started-with-claude-design.*
- Dual-pane: chat (left) + live interactive canvas (right). Outputs are interactive code artifacts (clickable modals, tabs, state), not static rasters. *Official.*

**Documented use cases:** realistic prototypes (shareable, no PR/code review); product wireframes/mockups (with Claude Code handoff); rapid design explorations/variants; pitch decks (outline → on-brand deck → PPTX or Canva); marketing collateral (landing pages, social, campaign visuals); "frontier design" (code-powered prototypes with voice/video/shaders/3D/built-in AI). *Official — launch blog.*

**Positioning (honest):** excels at 0→1 prototyping, variants, decks; not a full Figma replacement; struggles with deep UX logic (what to hide vs show on dense dashboards). Optimal pipeline: concept in Chat → visuals in Design → implementation in Code. *Practitioner/Community — Design review articles, r/ClaudeAI.*

---

## 2. Inputs, Design-System Ingestion

- **Import from anywhere:** text prompt; upload images + documents (DOCX, PPTX, XLSX); point at a codebase (React component libraries on GitHub) for design-system extraction; web-capture tool to grab elements from a live site. *Official — launch blog.*
- **Design-system engine:** parses codebases, PDFs, slide decks and design files to extract reusable components, colour palettes, typography, spacing grids, layout patterns → auto-generates a UI kit. Toggle "Published" to make it the team default. Multiple design systems can coexist (product lines / sub-brands) without cross-contamination. *Official — support.claude.com/.../14604397-set-up-your-design-system-in-claude-design.*
- Upload reference screenshots/competitor images for "make it look like this"; vision models replicate structure. *Official.*

**Caveats:** treat Figma uploads as a starting point, not 1:1 — it frequently misses component variables, disabled states, line-height, and hallucinates type scales/fonts. LLMs lack true spatial awareness (textual, not experiential, layout reasoning) → alignment/spacing/tiny-text errors. *Practitioner/Community — Figma MCP cluster, Generative UI cluster.*

---

## 3. Editing, Iteration, Export, Handoff

- Iterate via conversation, inline comments on canvas elements (targeted edits: padding, type scale, colour), direct text edits, and adjustment knobs/custom sliders (spacing/colour/layout/animation speed); changes can apply across the whole design. *Official.*
- On-canvas text "Edit" tool changes copy without consuming generation tokens. *Practitioner.*
- **Exports:** standalone HTML; download as .zip (multi-file/React); PDF; PPTX; Send to Canva (becomes editable Canva elements via HTML import); internal org URLs; "save as folder"; handoff bundle for Claude Code (single packaged instruction set: tokens + components + layout notes). *Official — launch blog; canva.com/newsroom/news/canva-claude-design.*
- No native Design→Figma export. Figma flows run via Claude Code + MCP (see §6). *Official silence / Not guaranteed.*

**Canva friction (community):** direct HTML export can flatten to an un-editable rasterisation, especially without Canva premium. Workaround: have Claude format to exact pixel dimensions (e.g. 1080×1350) and export as PPTX, then upload to Canva for full vector editability. *Community — r/canva.*

---

## 4. Documented Limitations & Bugs

- Research preview — behaviour/limits evolve; currently lacks audit logs and usage tracking. *Official — pricing/usage article.*
- Cannot natively generate raster images (placeholders/emojis only) or export MP4/video (HTML/PDF/PPTX/Canva only). *Practitioner.*
- Inline comments can disappear before the model reads them → paste feedback into chat. *Official.*
- Compact-layout mode triggers save errors → switch to full view to save. *Official.*
- Linking large monorepos causes lag/browser crashes → link specific subdirectories. *Official.*
- "Chat upstream errors" lock a session → open a new chat tab in the same project. *Official.*
- Mobile↔desktop responsiveness often needs manual CSS. *Practitioner.*
- Raw exported code is often an unmaintainable "opaque blob" (embedded SVG + inline styles) → prototyping, not production. *Practitioner — Generative UI cluster.*
- Unsubscribing can lock you out of Design projects → export data first via privacy controls. *Community — HN.*

---

## 5. Metering, Plans, Credits, Token Economics

**Documented conflict — present both, do not pick one:**

- *Official (support.claude.com/.../14667344-claude-design-subscription-usage-and-pricing, May 2026):* Claude Design is "priced and metered independently from the rest of Claude," with its own weekly allowance that resets every 7 days and never draws from chat or Claude Code limits. Per-user allowances on Pro / Max 5x / Max 20x / Team seats / legacy Enterprise seats. *Official.*
- *Community (r/ClaudeAI, used in deep research):* the isolated weekly Design limit was reportedly removed and merged into the standard 5-hour chat/Code pool; a single design edit can consume ~20–40% of that 5-hour limit; Anthropic reportedly doubled Design token limits and raised Code weekly limits ~50% (temporary, ~through July 13). *Community-reported.* Recommend: verify the live pricing article before quoting.

**Plan tiers (as reported — verify):** Free ($0, no Design); Pro (~$20, independent weekly allowance, exhausts fast on system setup); Max 5x (~$100, ~5x Pro, all Opus); Max 20x (~$200, ~20x Pro, priority queue); Team (Standard ~1.25x Pro/session, Premium ~6.25x Pro, min ~5 seats, SSO); Enterprise (negotiated; seat-based or usage-based at API rates with a one-time intro credit ~20 prompts). *Official — pricing pages; figures volatile.*

**Usage credits:** when the allowance is depleted, opting in continues work at standard API token rates. Discounted bundles, e.g. ~$45→$50 (10%), ~$200→$250 (20%), ~$700→$1,000 (30%), with monthly caps. *Official — support.claude.com/.../12429409 & /14246112.*

**API token economics (for usage-based Enterprise):** Opus 4.6/4.7/4.8 = $5/MTok input, $25/MTok output. Prompt caching: cache writes 1.25x (5-min) / 2x (1-hour); cache reads 0.1x and don't count against ITPM → reuse design systems/briefs via cache to cut long-prompt cost up to ~90%. Token-efficient tools beta cuts output tokens up to ~70%; Batch API gives ~50% discount on non-interactive bulk jobs. Opus 4.7+ tokenizer maps the same text to ~1.0–1.35x more tokens than 4.6. *Official — platform.claude.com/docs/en/about-claude/pricing; claude.com/blog/token-saving-updates.*

---

## 6. Figma & MCP Handoff (Extraction vs Injection)

**Officially supported (data extraction, via Claude Code — not the Design UI):**

- Official Figma plugin: `claude plugin install figma@claude-plugins-official` → tokenised OAuth → read live nodes, design tokens, component metadata. *Official (Figma-side) / Practitioner (Anthropic-side).*
- Remote MCP transport: `claude mcp add --transport http figma https://mcp.figma.com/mcp --scope user`. Uses `get_design_context` (screenshots + structural metadata). Runs locally; only active in Figma "Dev Mode" so files aren't continuously sent to cloud. *Official — figma.com/blog/introducing-claude-code-to-figma.*
- Claude Code → Figma: Claude captures real browser UI (prod/staging/localhost) and converts screens to editable Figma frames. *Official from Figma.*

**Practitioner push/injection (NOT guaranteed):** community tools (e.g. "FigClaw", browser-MCP + `evaluate_script` on the figma global) grant Claude write-access to draw vectors/auto-layout/variables directly in Figma. Fragile, unsupported, breaks on UI/API changes; uses your API keys. *Community — r/FigmaDesign, cianfrani.dev.*

**3-part Figma MCP prompt structure (to avoid failures):** (1) what to build, (2) target Figma file URL, (3) exact name of the published design-system library. Missing any → connector fails or draws unlinked random shapes. *Practitioner — Figma MCP cluster.*

**Multi-tool token routing:** ideate low-fi in Google Stitch (free, ~15s mobile layouts) → first hi-fi draft in Claude Design → manual vector tweaks in Figma → structural code refinement in Codex (~3–4x fewer tokens). Don't build basic design-system components (buttons, type scales, disabled states) with AI — it hallucinates states and burns tokens; build foundations manually, then teach the AI to use them. Group components into categorised .md skill files (Form Elements, Navigation, Data Display) — AI stops reading giant lists. *Practitioner — Figma MCP cluster.*

---

## 7. Artifacts & Generative UI (Depth)

- **Trigger:** significant, self-contained content (>15 lines), likely to be edited/reused. Types: Markdown, code, single-page HTML, SVG, Mermaid, interactive React. Available on all plans incl. Free (unlike Design). *Official — support.claude.com/.../9487310.*
- Sandboxed client-side: no external API/DB calls, no server logic. *Official.*
- AI-powered artifacts: embed a text API to Claude → shareable apps; usage bills to each user's own subscription, not the creator's (scales to thousands). *Official.*
- MCP integration (Pro/Max/Team/Enterprise): artifacts connect to Asana, Google Calendar, Slack, custom servers; each user authenticates individually. *Official.*
- Persistent storage: 20MB/artifact, text-only, personal vs shared modes, published artifacts only (dev-time storage calls fail). *Official.*
- Live Artifacts persist in the sidebar and pull fresh data via connected MCPs with a refresh button — avoid re-prompting. *Officially supported.*
- **Efficiency:** start from a Minimal Viable Artifact and iterate; "Remix" for iteration to keep chat lean; target specific errors instead of full regenerations; local image uploads break in shared artifacts → use public URLs/SVG/emoji; enable code execution to parse XLSX. *Practitioner + Official.*

---

## 8. File Limits (Apply to Design Inputs Indirectly)

Documents: PDF, DOCX, CSV, TXT, HTML, ODT, RTF, EPUB, JSON, XLSX (XLSX needs code execution). Images: JPEG, PNG, GIF, WebP. Per chat: up to 20 files, 500MB/file, images up to 8000×8000px. Projects: 30MB/file, unlimited files (bounded by context). PDFs >100 pages → text-only (loses charts/typography). Images ≥1000×1000px recommended. *Official — support.claude.com/.../8241126 & /12111783.*

---

## 9. Key Claims to Avoid (Design)

No native image/video generation; no unlimited usage; not production-ready/maintainable code; no flawless Figma import or exact token extraction; no native Design→Figma; no two-way sync as an official feature; Design is web-only (not Desktop). Don't claim Design self-evaluates aesthetics reliably in one pass — use a separate evaluator. *Project guardrail + sources above.*

*Sources: anthropic.com/news (claude-design-anthropic-labs, claude-for-creative-work, claude-opus-4-8); support.claude.com help articles (14604416, 14604397, 14667344, 9487310, 8241126, 12111783, 12429409, 14246112, 9797557); platform.claude.com/docs/pricing; figma.com/blog; canva.com/newsroom; plus practitioner/community (Design review articles, r/ClaudeAI, r/canva, r/FigmaDesign, cianfrani.dev, Design Systems Collective, Ocasio Consulting) and report_complete clusters. June 2026.*

---
---

# Source Dossier 2 — Claude Surfaces: How-To & Ecosystem

*Depth reference for Identity A (capabilities)*

**Retrieval keywords:** Chat, Projects, Skills, Agent Skills, SKILL.md, Cowork, Claude Code, Claude Design, setup, install, onboarding, how-to, decision matrix, which surface, features, limitations, use cases, MCP, connectors, creative connectors, enterprise, Team, permissions, scheduled tasks, RAG, context window, models.

*Purpose: detailed, source-linked how-to for each Claude surface. Merges deep research (Gemini + Perplexity prompt 2), the report_complete clusters (Official docs, MCP, Cowork, Projects, Practitioner workflows/Skills, Enterprise, Workflow architecture), and "Claude Design: Mastering the New Era of Agentic UX." Evidence tiers preserved. Compiled June 2026 — verify volatile details against support.claude.com / platform.claude.com.*

---

## 0. Ecosystem Framing

Claude evolved from a chatbot into a multi-surface agentic ecosystem; the value comes from routing work to the right surface rather than treating it as a "glorified search engine." Four agentic surfaces sit on top of Chat/Projects: Claude Code (terminal coding), Cowork (desktop knowledge work), Claude Design (visual prototyping), with Skills and MCP as the cross-cutting extension layers. *Practitioner — "Mastering the New Era of Agentic UX."*

| Task | Best surface | Switch when |
|---|---|---|
| Ask, brainstorm, draft, quick specs/accessibility checks | Chat | multi-day shared-doc stream → Projects; real visuals → Design |
| Ongoing initiative w/ many docs (PRDs, research, brand) | Projects | reusable scripted workflow → Skills; local-file automation → Cowork |
| Encode a reusable procedure (review recipe, deck template, audit) | Skills | only per-project context needed → Projects |
| Act on local files/apps (organise, build decks/sheets from sources) | Cowork (Desktop, paid) | no local access wanted → Chat/Projects; code-centric → Code |
| Deep coding, refactors, review, CI | Claude Code | non-code agentic work → Cowork; visual prototypes → Design |
| Prototypes, mockups, decks, visual one-pagers | Claude Design | upstream ideation → Chat; implementation → Design→Code/Canva |

*Evidence: Official (synthesised from Anthropic docs/product pages).*

---

## 1. Claude Chat

**Purpose:** general-purpose conversational surface (web/desktop/mobile) for questions, drafting, analysis, multi-step tasks. **When:** quick thinking/drafting not needing a long-lived workspace or local files. Over Projects for early exploration; over Cowork when you don't want local file access.

**Setup:** claude.ai or Claude Desktop (macOS 11+/Win 10+) → sign in → model selector (Sonnet/Opus) → Settings > Capabilities > View and edit memory → "+"/"\"/\" for options → ghost icon = Incognito Chat.

**Features:** 200K context; automatic background summarisation; Incognito (not saved/trained, purged 30 days); web search; attachments up to 500MB/file (20/chat); extended/adaptive thinking; memory import from some providers. *Official — support.claude.com/.../8114491, /11817273, /12260368.*

**Limits:** rolling 5-hour usage window (tighter Free/Pro) + weekly limits; threads isolated; browser sandbox can't read/write local files; no full chat-history import from other providers. *Official.*

**Design use cases:** UX microcopy + localisation with char-count checks; ad-hoc WCAG/aria checks on a snippet; clustering pasted interview notes into personas/JTBD. *Practitioner.*

---

## 2. Claude Projects

**Purpose:** self-contained workspaces with own chat history, knowledge base and custom instructions; persistent context across threads. **When:** initiative big enough for its own corpus; you're re-uploading the same docs or need consistent project tone. Over Skills when you need content grounding, not a portable procedure.

**Setup:** claude.ai/projects → "+ New Project" → name + description → (Team/Enterprise) visibility (private vs share org) → upload to Project Knowledge → "Set project instructions" (role, tone, format, negative constraints).

**Features:** 200K base; paid plans RAG auto-expands ~10x as knowledge nears the limit (retrieves relevant chunks); cached content reused doesn't re-count against limits; role-based sharing (Can use / Can edit) on Team/Enterprise; bulk-move standalone chats in. Free = 5 projects max. *Official — support.claude.com/.../9517075; anthropic.com/news/projects.*

**Limits:** no auto file-sync (replace manually); not API-accessible; cross-project isolation; chat-level uploads stay isolated (don't join project KB); sharing only Team/Enterprise. *Official.*

**Best practice:** "three-file baseline" (voice/brand; audience persona; past work/components); fix systemic errors in instructions not in chat; one project = one focus; archive completed projects. *Practitioner.*

**Cowork Projects differ:** local desktop workspaces with own instructions, scheduled tasks, context (folders/URLs), project-scoped memory; stored locally, no cloud sync, no Team/Enterprise sharing yet. *Official — support.claude.com/.../14116274.*

---

## 3. Claude Agent Skills

**Purpose:** reusable, filesystem-based packages (SKILL.md + optional scripts/references/assets) giving domain workflows via progressive disclosure (metadata always loaded ~100 tokens; instructions load on trigger; references/scripts load as needed). **When vs Projects:** when a workflow repeats across many conversations/projects (review recipe, house deck style). Projects ground in content; Skills encode procedures.

**Setup:** build with skill-creator (Cowork/Code, extended thinking) → it interviews you → compiles lowercase-hyphen folder with YAML-frontmatter SKILL.md + scripts → run the eval suite. Install: web Settings > Capabilities/Features > Skills (Pro/Max/Team/Enterprise); Code `~/.claude/skills/`; API beta headers (code-execution-2025-08-25, skills-2025-10-02, files-api-2025-04-14) + `container.skills`.

**Features:** three-tier loading; pre-built Office skills (pptx, xlsx, docx, pdf); slash-command triggers; composable; open-source examples in anthropics/skills. *Official — platform.claude.com/docs/.../agent-skills/overview; github.com/anthropics/skills.*

**Limits/safety:** no cross-surface sync (deploy to web/API/Code separately); web skills per-user, no central team distribution; runtime differs (API = no network, pre-installed packages only); not ZDR-eligible; folder must be named SKILL.md. ~36% of sampled third-party skills contained prompt injections/malicious payloads — scan community skills as unaudited code. *Official + Practitioner.*

**Design use cases:** brand "pitch-deck-standard" skill atop built-in pptx; design-token compliance audit skill (line-by-line violation log); research-synthesis skill. *Practitioner.*

---

## 4. Claude Cowork

**Purpose:** agentic desktop mode; takes a goal and works autonomously across local files/folders/apps to produce finished deliverables. **When:** Claude must manipulate local artifacts (rename/sort assets, folder→report, build sheets/decks from sources). Over Chat/Projects when local files central; over Code when not code-centric.

**Setup:** install Claude Desktop (macOS/Win), sign in paid → Cowork tab (Team/Enterprise: enable under Organization settings > Capabilities > Cowork) → Settings > Cowork global instructions → connect folders, choose "Ask before acting" vs "Act without asking" → optional "Claude for Small Business" connectors (Google Workspace, Microsoft 365, Canva, HubSpot, QuickBooks).

**Features:** "Computer Use" screen actions (screenshot/cursor/click/type); code in isolated Linux VM (Apple Virtualization.framework / Hyper-V); long-running + parallel sub-agents; Cowork Projects; Scheduled Tasks; plugins/Skills; 15 SMB agentic templates; OpenTelemetry monitoring (Enterprise). *Official — anthropic.com/product/claude-cowork; support.claude.com/.../13345190, /14479288, /14477985, /13837440.*

**Limits/risks:** paid + Desktop only; activity not in audit logs/Compliance API/exports (Enterprise → OpenTelemetry); data local-only, admins can't centrally export/delete; scheduled tasks need app open + machine awake; folder access allows read/edit/delete (keep boundaries strict); "Computer Use" vulnerable to prompt injection from untrusted pages; multi-step tasks burn tokens (50–100x a normal message). *Official + Practitioner.*

**Workspace structure:** `context/` (about-me, brand-voice, working-preferences), `projects/`, `output/`; root CLAUDE.md < ~300 lines w/ on-demand pointers; memory.md ~150-line cap + archive.md; separate prescriptive rules (CLAUDE.md) from temporary facts (memory.md). *Practitioner.*

**Design use cases:** interviews folder → research report + summary deck; clean/rename messy export folders to team convention. *Practitioner.*

---

## 5. Claude Code

**Purpose:** agentic CLI/IDE that reads, edits, runs, tests, commits code via natural language; git + CI integration.

**Setup:**
```bash
# macOS/Linux/WSL
curl -fsSL https://claude.ai/install.sh | bash
# Windows
irm https://claude.ai/install.ps1 | iex
# npm (no sudo)
npm install -g @anthropic-ai/claude-code
```
Run `claude` in a repo → browser OAuth → `claude doctor` → `/init` (scans repo, generates CLAUDE.md). Needs Node 18+, macOS 13+/Win 10+/Linux/WSL.

**Features:** Plan Mode (Shift+Tab) writes a plan before editing; `/autofix-pr` runs tests + patches lint/compile errors on PRs; `/batch` parallel sub-agents in isolated git worktrees (large migrations); unified memory (auto-memory + CLAUDE.md); Skills/plugins/MCP; `@claude` on GitHub; headless modes; `/effort` levels; `/compact`; `/context`. *Official — code.claude.com/docs; support.claude.com/.../14552382, /14554922, /14554000.*

**Limits:** shares usage limits with chat/Design (big refactors burn quota); needs a git repo; no native visual canvas (use browser/extension); terminal-comfortable users; context degrades as it fills (compact before ~70%). *Official + Practitioner.*

**Design use cases:** "Migrate nav bar in /src to Tailwind v4, run tests, write commit msg"; implement a Design handoff bundle, review via PRs. Use Git worktrees for parallel agents; avoid `--dangerously-skip-permissions` (catastrophic-deletion risk); don't claim flawless 100k+-line legacy migration. *Practitioner.*

---

## 6. Claude Design

(Full dossier in Source Dossier 1.) **Summary:** web-only (claude.ai/design) canvas + chat, Opus-powered, Pro/Max/Team/Enterprise research preview. Ingests brand assets/codebases into a published design system; generates interactive prototypes/decks; inline comments + sliders; exports HTML/zip/PDF/PPTX/Canva/Code handoff. No native image/video gen, web-only, metering caveats. *Official.*

---

## 7. Cross-Cutting: MCP, Connectors, Enterprise & Security

- MCP open standard (10,000+ public servers). Allowlist needed tools (`MCPToolset`, default `enabled:false`); `defer_loading:true` keeps tool descriptions out of context until queried; `mcpResourceToContent` injects resources as content blocks. Remote MCP needs HTTP/SSE (no direct local STDIO); MCP data exempt from ZDR; Enterprise admins can blocklist tools; store secrets in OS keychain via Desktop manifest, not the prompt. *Official — MCP cluster.*
- **Creative connectors ("Claude for Creative Work"):** Ableton, Adobe (50+ CC tools), Affinity by Canva, Autodesk Fusion, SketchUp, Blender (MCP→Python API). *Official.*
- **Enterprise/SMB:** Claude runs inside business tools (HubSpot→Canva, QuickBooks, Docusign, Microsoft 365); inherits user permissions; Team/Enterprise data excluded from training by default. Design agentic flows with a human-in-the-loop approval gate before send/post/pay; treat MCP/connector output as untrusted (injection vector). *Official — Enterprise cluster.*

---

## 8. Models (2026)

Opus 4.7/4.8 (flagship reasoning/vision, 1M context, literal instruction-following, house style: warm cream/serif/terracotta — override explicitly; deprecated temperature/top_p/top_k → 400; effort levels high/xhigh/max; Task Budgets advisory; hi-res image input ~2576px = 3x tokens). Sonnet 4.6 = cheap everyday workhorse. Haiku = fast/cheap simple tasks. Match model to task. *Official — Opus 4.7/4.8 cluster; platform.claude.com/docs.*

*Sources: support.claude.com (8114491, 9517075, 14116274, 13345190, 14479288, 14477985, 13837440, 14552382, 14554922, 11817273, 12260368), platform.claude.com/docs (agent-skills, pricing, home), code.claude.com/docs, anthropic.com (claude-cowork, claude-for-creative-work, projects), github.com/anthropics (skills, claude-code), plus report_complete clusters and "Mastering the New Era of Agentic UX." June 2026.*

---
---

# Source Dossier 3 — 2026 Competitive Landscape: AI-Assisted UI/UX Design

*Depth reference for Identity A (positioning) and Identity B (tool routing)*

**Retrieval keywords:** competitor, comparison, vs, alternative, Figma, Figma Make, Figma AI, Google Stitch, Vercel v0, ChatGPT Canvas, Gemini Canvas, generative UI, Lovable, Replit, UX Pilot, Uizard, Framer, pricing, when to choose Claude Design, design-to-dev handoff, maturity, market landscape.

*Purpose: detailed, source-linked comparison of Claude Design vs the 2026 AI-design ecosystem. Merges deep research (Gemini + Perplexity prompt 3) and the report_complete "Ecosystem & Competitor Comparisons" cluster. Present comparisons neutrally; mark beta/experimental status. Prices/credits are volatile (June 2026) — verify before quoting. Distinguish official capability from reviews/community.*

---

## 1. The Market Shift (Context)

The historical split between visual canvas and functional code is dissolving: models now turn aesthetic intent into interactive HTML/React. The design system becomes the primary artifact; individual static screens become ephemeral. The bottleneck moves from visual production to visual judgment and curation — designers act as constraint-setters and judges. *Trend interpretation — UX Tigers, agency reviews.*

**Corporate signal:** Anthropic launched Claude Design on April 17, 2026 (Anthropic Labs research preview), three days after CPO Mike Krieger left Figma's board; the announcement reportedly coincided with a ~7% single-day drop in Figma stock. *Community/news.*

**Risks of the new paradigm:** "aesthetic mode collapse" (outputs converge to generic SaaS averages); teams skipping IA/user-flows/accessibility because polished mockups are cheap; de-skilling / cognitive offloading (HCI research). *Practitioner/academic.*

Research (Canvil, GenUI studies) finds AI embedded in existing tools (Figma, Claude Code, brand systems) adopts better than standalone "magic UI generators," especially when it exposes control over constraints and design systems.

---

## 2. Tool-by-Tool

### Claude Design
- **Positioning:** conversational, brand-aware design canvas integrated with Claude Code and the Claude ecosystem; multi-modal "frontier design" (voice, video, shaders, 3D, built-in AI). Opus 4.7/4.8 engine; output interactive HTML/CSS/JS.
- **Strengths:** brand-aware design-system inference from codebases/files; code-aware handoff (bundles to Claude Code); inline comments + Tweaks Panel sliders (no regeneration cost); multi-source input (DOCX/PPTX/XLSX/URL/GitHub).
- **Weaknesses:** research preview (evolving, thin docs); Opus 4.7 can take minutes to render a page (hinders rapid exploration); weak on hard-to-describe micro-interactions/motion timing; spatial text prompts ("move button slightly left") break layout — point at elements instead; limited third-party ecosystem; no native Figma export.
- **Handoff:** ZIP (clean HTML/CSS), Claude Code bundle, Canva, PDF, PPTX, internal URL.
- **Pricing:** included in Pro/Max/Team/Enterprise; per-user weekly allowances (see Dossier 1 metering conflict). No separate SKU.
- **Maturity:** new (Apr 2026) on mature Claude models; early enterprise adoption. *Official + Practitioner/Community.*

### Figma (Design + AI + Make)
- **Positioning:** the mature collaborative UI/UX standard; AI as an acceleration layer.
- **AI features:** content (replace/shorten/translate/suggest), image (make/edit/vectorize), canvas utility (rename layers, search-with-image, find-more-like), layout synthesis (First Draft text-to-UI, Figma Agent beta from May 20 2026, Figma Make prompt-to-code using your design system, Figma Sites no-code publishing).
- **Handoff (mature):** Dev Mode → HTML/CSS/Tailwind/SwiftUI/Jetpack Compose preserving tokens; Code Connect maps components to GitHub/Storybook; Figma MCP Server lets Claude Code/Cursor/VS Code read canvas + push "code to canvas."
- **Weaknesses:** AI imports often break Auto Layout / type sizes / library mapping; Make code not production-ready (needs accessibility/responsiveness work); complex seat pricing.
- **Pricing:** Free Starter; Pro ~$16/mo full seat (Dev ~$12, Collab ~$3); Enterprise up to ~$90/mo full seat; AI gated to paid full seats; shared pool of ~3,000 AI credits/month.
- **Maturity:** most mature; AI is evolutionary. *Official (Figma docs) + community.*

### Google Labs Stitch
- **Positioning:** free AI-native "vibe design" canvas (Google Labs). Gemini 3 Flash (standard) / Gemini 3.1 Pro (experimental).
- **Features:** infinite canvas; persistent design agent + Agent Manager (parallel variations); automatic screen stitching + Play preview; voice commands; DESIGN.md import/export of design rules; Direct Edit pencil + global palette (no prompt credits); Stitch SDK (@google/stitch-sdk) + MCP server; exports to Google AI Studio / Antigravity.
- **Weaknesses:** Labs beta; "pretty but useless UI" (inconsistent padding, mismatched fonts, unrealistic placeholders); much stronger on mobile than web; limited design-system/production integration.
- **Pricing:** free in Labs (~300 daily credits/Google account).
- **Maturity:** rapidly evolving experiment; great for early alignment/wireframing, cheap on tokens. *Official (Google) + community.*

### Vercel v0
- **Positioning:** developer-first; prompt-to-production React + Next.js + Tailwind + shadcn/ui code. 6M+ developers, 80,000+ enterprise teams, ~$42M ARR (Mar 2026).
- **Features:** multi-page app generation (App Router); agentic (web search, inspect live sites, debug TS); VS Code-style editor; Git panel (branches/PRs); full-stack sandbox + DB (Snowflake/AWS); visual Design Mode updating React.
- **Weaknesses:** "component-to-app gap" (no auth/storage/payments/APIs out of the box); React/Next/Vercel lock-in; token-based billing unpredictable.
- **Pricing:** Free ($5/mo credits); Premium $20/mo (Figma import, API); Team $30/user/mo; Enterprise custom.
- **Maturity:** mature within dev community; one-stack depth. *Official + reviews.*

### ChatGPT Canvas
Side-panel document/code editor (GPT-5.5/5.4), not a design tool. Good for UX-copy ideation, transcript synthesis, basic wireframe code blocks. No design-system awareness, no Figma ingest, no folder parsing, no sliders/voice. Free/Plus/Pro; ~$20/mo Plus. Mature general feature, low design specialisation. *Official + reviews.*

### Gemini Canvas / Generative UI
Gemini 3 / 2.5 Pro workspace; strong SVG rendering, consistent padding, good at abstract aesthetic prompts ("cold restraint"), handles dense dashboards. Dynamic View / Visual Layout / AI Mode in Search = generative UI experiments (model-decided layouts, limited designer control, gated to Google AI Pro/Ultra, little export/handoff). Ephemeral prototyping; no deployment/DB/version control. *Official (Google) + reviews.*

### Other Entrants
- **Lovable** — full-stack app builder (React/TS + Supabase, auth, Stripe); Visual Edits (no prompt cost), Plan Mode, prompt queue (≤50); expanded to data/decks/marketing (Mar 2026); struggles with complex backend logic, dropped Figma import. Free (5 daily credits) / Pro $25 / Business $50.
- **Replit Agent Design Canvas** (Agent 4, Mar 2026) — infinite board beside running app; sketch→component; responsive frames; "make this a real app" provisions DB/auth; Figma import/MCP. Canvas free; app conversion paid.
- **UX Pilot** — AI UX flows, predictive heatmaps, design scoring, Figma export; free + ~$15–29/mo.
- **Uizard** — sketches/prompts→UI, React/CSS handoff; free + ~$12–39/mo.
- **Framer AI** — text-to-site for marketing pages (GPT-4o assisted).

---

## 3. Neutral Comparison Matrix

| Tool | Persona | Strengths | Weaknesses | Handoff | Pricing | Maturity |
|---|---|---|---|---|---|---|
| Claude Design | Designers, PMs, founders, marketers | Brand-aware, code-aware handoff, multi-modal prototypes, sliders/comments | Research preview, slow render, thin ecosystem, no native Figma export | Claude Code bundle, HTML/ZIP/PDF/PPTX/Canva | Bundled in Pro/Max/Team/Ent, per-user allowance | New (2026), mature models |
| Figma (AI/Make) | Pro UI/UX designers | Design-system depth, collaboration, prototyping, mature ecosystem | AI imports break layout, Make code not prod-ready, seat complexity | Dev Mode, Code Connect, MCP, Sites | Free→~$16–90/seat, 3,000 AI credits/mo | Very mature |
| Google Stitch | Prototypers, creative teams | Fast prompt/sketch→UI, voice, DESIGN.md, SDK, free | Labs beta, "pretty but useless", mobile>web | HTML, AI Studio, Antigravity, SDK | Free (~300 credits/day) | Experimental |
| Vercel v0 | Frontend/React devs | High-quality React/Tailwind code, full-stack sandbox | Component-to-app gap, stack lock-in, token billing | In-code, Git PRs, Vercel deploy | Free→$20–30/user + credits | Mature (dev) |
| ChatGPT Canvas | Writers/coders | Strong text/code editing | No design canvas/system, no Figma | Copy-paste, file download | Free/Plus/Pro (~$20) | Mature, low design |
| Gemini Canvas/GenUI | Business, students, prototypers | SVG rendering, abstract aesthetics, generative UI | Experimental, limited control/export | Mostly stays in Gemini/Search | Google AI Pro/Ultra | New experimental |
| Lovable | Founders, no-code | Full-stack apps, Visual Edits, Plan Mode | Weak complex backend, dropped Figma import | GitHub sync, Vercel/Netlify | Free→$25/$50 | Active prod tool |
| Replit Agent | Full-stack builders, PMs | Sketch→app, DB/auth provisioning, responsive frames | App conversion needs paid plan | Live sandbox apps, Figma MCP | Canvas free, app paid | Mar 2026 |

---

## 4. Claude vs ChatGPT/Gemini — UX Philosophy

Claude's Artifacts/Design are an execution/compilation sandbox (React/HTML runs live client-side, persistent storage up to 20MB, MCP-extensible, Skills/commands/Code automation). ChatGPT Canvas is a collaborative editing environment (version history, inline comments, no structural execution). Gemini is a linear chat with workspace extensions. Claude is superior at premium polished UI out-of-the-box and at large-context analysis (200K–1M, spots contradictions in 150+ page docs), with a more natural writing tone. But Claude has strict rate limits / "out of compute" events, no native image/video generation (vs DALL-E/Sora), and a token economy that burns fast on heavy iterative work. *Practitioner/Community + report cluster.*

---

## 5. When to Choose Claude Design (and When Not)

**Choose it when:** you want a unified AI design→code workflow (esp. teams on Claude Code); prototypes need rich interactivity (voice/video/3D/AI); you want brand-consistent output from day one via codebase inference; you value conversational exploration + direct manipulation with PMs/non-designers.

**Prefer alternatives when:** standardised design at scale with large teams on mature design systems (Figma); developer-led React/Next web UI (v0); zero-budget early experimentation (Stitch / Uizard / UX Pilot free tiers); content-first writing/coding (ChatGPT Canvas / Gemini). *Synthesised, June 2026.*

*Sources: anthropic.com/news/claude-design-anthropic-labs; figma.com & help.figma.com; blog.google (Stitch, Gemini 3); vercel.com/blog (v0); reviews (LogRocket, UX Tigers, XDA, Anima, Banani, Taskade, UI Bakery); ACM/IEEE HCI papers; report_complete "Ecosystem & Competitor Comparisons" cluster. June 2026.*

---
---

# Source Dossier 4 — Emerging Interfaces & Experience Patterns (2025–2028)

*Depth reference for Identity C (trends & future-interface design)*

**Retrieval keywords:** agentic UX, probabilistic UX, human-on-the-loop, autonomy, ambient computing, smart glasses, wearables, Ray-Ban Meta, Apple Vision Pro, waveguide, EssilorLuxottica, generative UI, adaptive UI, Liquid Glass, multimodal, voice, gaze, EMG, neural band, trust, privacy, 6-layer model, agents as users, accessibility tree, forecasts, 2026, 2027, 2028.

*Purpose: detailed, source-linked reference on emerging interaction/experience paradigms. Merges deep research (Gemini + Perplexity prompt 4), report_complete emerging-paradigm syntheses, and curated notes (UX Guidelines for AI & Multi-Agent Systems; Wearables & the Conscious Interface; Wearables & the Silver Economy; iF Design Trend Reports; NN/g 2025 trends). "Observed practice" = current products/research; "Speculation" = reasoned 2–3-year predictions (label explicitly; never a Claude capability claim). Compiled June 2026.*

---

## 1. Agentic & Probabilistic UX

**Definitions.** Agentic UX: AI acts as a semi-autonomous agent that plans, decides and performs multi-step tasks across apps/the physical world. Probabilistic UX: outcomes are non-deterministic — the same input can yield variable quality, so uncertainty is an inherent property, not a failure. Designers shift from drawing screens to defining confidence thresholds for autonomous action vs human intervention. *Observed — NN/g "A Concrete Definition of an AI Agent"; probabilistic-UX articles; GUI-agent surveys (arXiv).*

**Deterministic → probabilistic shift:** behaviour predictable→adaptive; errors hard-fail→graceful degradation/rollback/editable; user operator→supervisor; validation static→continuous (corrections feed retraining); explainability rarely→often required. *report_complete + UX Guidelines note.*

**Observed agentic UI patterns (2024–26):** delegation canvases / task briefs (goal, constraints, resources, success criteria); plan previews with editable steps; simulation / dry-run modes for high-risk tasks; mixed-initiative corrections (agent updates the plan, not just the answer); agent state/memory panels ("what I know / assumptions / context").

**Design principles:** design for outcomes not screens; progressive autonomy (assistive → semi → autonomous as trust grows); legible intent & capability; tunable risk (scope, reversibility, notification intensity); graceful failure & repair flows. Uncertainty-management toolkit: confidence indicators, progressive disclosure of reasoning (cite RAG sources), latency as a trust canvas (narrate background steps), reversible interventions (undo/edit/retry/override as primary controls). *Observed — Google People+AI, IBM, Microsoft, NN/g.*

**Human-on-the-loop oversight.** Move from approve-every-action (in-the-loop) to monitor-and-intervene (on-the-loop). Key problem = dynamic intervention thresholds (contextual/emotional/risk-based): autonomous calendar drafts OK, explicit approval for sending email/transactions. Needs visible pause/veto/override/rollback; if the only stop is waiting for the output, oversight is broken. *Observed.*

**Enterprise architecture (4 layers):** engagement (interface) · agency (agents) · work (apps/APIs) · data (unified layer). GitLab's 8 agentic collaboration patterns: status updates, work routing, team communication, role-specific chat, conversational context, RBAC, governed/sandboxed environments, collaborative building (rarest: unified governance). Evaluate with IDEO low-fi prototyping ("a prototype is worth a thousand meetings"). *Observed.*

**Open problems:** measuring impact vs usability (agents complete tasks but cause side effects → need metrics beyond task completion); multi-agent ecosystems / cross-vendor mediation; users over/under-trust by framing. *Speculation: standardised delegation patterns across Apple/Google/Microsoft; agent-as-colleague role metaphors; agent-level permissions/policy (RBAC for agents); on-device eyewear agents acting on what you see/hear.*

---

## 2. Ambient Computing & Context-Aware Experiences

Computation recedes into the background, embedded in spaces/objects/wearables (multimodal AI + edge compute respond in situ, not in an app session). *Observed — Thoughtworks, ambient-AI sources.*

**Observed patterns:** environment-anchored UI (Vision Pro anchors windows to furniture/walls); peripheral cues over central focus (haptic taps, subtle light, one line of text); context-aware modality adaptation (voice/haptics while walking, visuals when seated); multi-device orchestration (offload heavy work to phone/PC; glasses/speakers as I/O).

**Principles for ambient/spatial UX:** respect the environment (translucent, light, adapts to real lighting); comfort/ergonomics (content near resting gaze, wider not taller — Vision Pro guidance, hit targets ~60pt); anchor to meaningful objects/activities/people; favour glances over sessions; design for social acceptability (signal active sensors). *Observed — Apple visionOS guidelines, NN/g AR usability.*

**New materiality:** Apple "Liquid Glass" (iOS 26) — translucency/depth/micro-refraction; Apple shipped a "turn off Liquid Glass" toggle ~7 weeks in after clutter complaints → depth/motion must serve communication. "Intelligent reduction" / "knowing what not to show" — premium UX suppresses irrelevant detail, hides low-confidence recommendations. Corporate-Memphis flat illustration declining. *Observed/Trend — UX trend reports.*

**Open problems:** context-inference reliability (driving vs walking, private vs public) — misclassification = safety/privacy risk; cross-vendor orchestration; invisible complexity ("logic in the walls"). *Speculation: scene-level policies ("in meetings, urgent-only via haptics"); shared mixed-reality contexts; contextual eyewear defaults (caption-only in noise, minimal while driving).*

---

## 3. Post-Smartphone Wearables & Smart Glasses

**Device spectrum:** audio-first AI glasses (Ray-Ban Meta — camera/speakers/assistant, fashion-first, ~51g); spatial headsets (Apple Vision Pro — high-fidelity MR, bulky, focused sessions); prototype display AR glasses (monocular/small-FoV for nav/translation, sometimes neural-wristband/ring control). Two paradigms: Apple immersive spatial computing vs Meta ambient AI / conscious interface. *Observed.*

**Optics:** descend from 1940s cockpit HUDs and the 1988 Oldsmobile windshield HUD; modern waveguide "light highways" route a temple micro-projector to the pupil, correcting chromatic dispersion with a ~9mm eyebox. *Observed.*

**Market & players:** ~$2.9B (2025) → $8.4B+ (2035) at ~11.6% CAGR (some forecasts higher). Google–Warby Parker ($150M), Apple screenless camera frames, Meta × EssilorLuxottica (Ray-Ban, Oakley) + Gentle Monster. Constraint vs MR headsets: must look/weigh/feel like normal eyewear for all-day public wear.

**Five 2026 glasses paradigms:**
- AI Glasses (no display, camera+audio, ~51g — Ray-Ban Meta Gen 2, Xiaomi)
- Display Glasses (small HUD — Meta Ray-Ban Display, Brilliant Labs Halo)
- AR Glasses (waveguide/micro-LED, 30–80g — Even Realities G2 36g, INMO GO 3, Vuzix Z100)
- AR Display Glasses (tethered virtual monitors — XREAL One Pro, RayNeo Air 4 Pro)
- Smart Sunglasses (audio-first — Bose Frames, Reebok by Lucyd)

**Observed eyewear UX patterns:** glanceable text-minimal overlays ("smallest screen in the world"); glasses-first aesthetics (social acceptability drives adoption); micro-experiences not apps (translation on hearing a phrase, hands-free capture/recall "remember this"); spatial ergonomics (white type on translucent glass, bold weights, ~60pt targets); camera-as-input ("shared visual context").

**Input barriers:** weight/balance/temple pressure/heat; touch fails in rain/gloves; voice socially awkward + noise-unreliable. **Principles:** design for intermittent not continuous attention; minimal high-contrast type; obvious capture signalling + fast sensor kill-switch; battery-aware short high-value interactions; cross-device choreography (glasses capture/glance, larger screen for deep work). *Observed.*

**Open problems:** app model/distribution (stores vs agent skills vs micro-experience marketplaces); public interaction norms (always-on cameras, private voice); accessibility without stigma. *Speculation: mainstream "companion glasses" by ~2027 (nav/translation/light agent, heavy work still on phone); agent-centric eyewear (agent front instead of home screen); multi-accessory mesh (glasses + pin + ring + earbuds).*

---

## 4. Generative & Adaptive UI

Front-end where layouts/components/flows are assembled in real time by AI from goals/context, not hard-coded. *Observed — Google "Generative UI"; MAxPrototyper; GenUI studies.*

**Observed patterns:** prompt-to-screen; multi-agent design collaborators (theme/layout/content agents, human-guided); runtime personalisation (structure, not just content); evaluation tooling (EvAlignUX). **Documented outcomes:** fintech replaced 6 static dashboards with 1 adaptive role/usage-driven view → support tickets −27%; context-driven onboarding (technical→API docs/sandbox, business→guided tour) cut onboarding ~12min→<5 and reduced churn.

**Principles:** constrain the space (UI grammars, design tokens, component libraries models compose safely); make adaptation explainable; maintain consistency/identity; human-in-the-loop oversight. **Open problems:** stability vs personalisation (over-personalisation harms learnability); robustness/safety (mis-generated UI can hide controls / break accessibility); versioning/QA of runtime-variable UIs.

*Speculation: pattern-level generation (generate structured flows conforming to design systems, not pixels); continuous interface adaptation by device/attention/task; agent-designed micro-HUDs for glasses.* **The Semantic Design System Moat:** as generative UI compiles from briefs, advantage shifts from static layout libraries to consistent semantic design systems; inconsistent tokens → fragmented output. Directly relevant to design-system teams.

---

## 5. Voice, Gaze & Multimodal Input

Voice-only products failed (Humane AI Pin, Rabbit R1) — cognitive load, weak spatial execution. Winning interfaces are multimodal (voice + touch + gesture + gaze, concurrent, handing off). A 2026 scoping review (103 studies) finds gaze + speech compelling for hands-busy/eyes-busy contexts. *Observed.*

| Modality | Strength | Weakness | Handoff |
|---|---|---|---|
| Voice | Fast, hands-free, high bandwidth | Low precision, awkward, noise | → touch / HUD text |
| Touch | Absolute precision, silent | Needs attention, occludes | → voice / overlay |
| Gesture | Intuitive, 3D | Low precision, gorilla-arm fatigue | → gaze targeting + confirm |
| Gaze | Rapid targeting, zero movement | "Midas Touch" mis-triggers, fatigue | → pinch / EMG click |
| EMG/neural | Ultra-low strain, covert | Calibration, signal noise | complements voice+gesture |

**Patterns:** gaze-to-select + pinch-to-confirm (Vision Pro; wide-FoV cameras let hands rest); voice-first + ambient visual hints (chips/captions/cards); combined gaze+speech+gesture deictic ("put this there"); hands-free capture/recall. Wrist-worn EMG (Mudra Pro/Band, Meta prototype neural band) decodes muscle biopotentials for "Air-Touch"/intended-movement selection. Midas Touch solved by pairing gaze with a low-effort confirm.

**Principles:** redundancy/fallback for critical actions; clear mode/focus indication; low-effort micro-gestures; error-tolerant natural language + confirmation for ambiguity. *Speculation: multimodal default for wearables; learned personal command "languages"; shared multimodal AR spaces. Observed + speculation.*

---

## 6. Trust, Control, Safety & Privacy

Trust depends on performance, transparency, fairness, prior experience, social context; even top GenAI has mid-teens % inaccuracy → critical use + oversight. *Observed — trust SLRs, NN/g.*

**Patterns:** transparent boundaries/capabilities; stepwise confirmation for high-impact actions; activity histories/logs; explanation snippets ("I recommended this because…"); personalisation with boundaries. IDEO: successful assistants are intuitive, social, trusted, multimodal, nurturing (trust is emotional + accuracy).

**Principles:** obvious close-at-hand control surfaces (fast pause/undo/revoke); communicate uncertainty qualitatively; support verification/audit; align with social norms.

**Wearable privacy backlash:** always-on cameras/mics + facial recognition; "Name Tag" controversy; cloud-routed footage reviewed by subcontractors; risk of reviving "glasshole" stigma.

**6-Layer Privacy & Consent Model:**
- **(I) Social Visibility** — front LEDs visible at 10m, recognised ~2s
- **(II) Electronic Notification** to nearby devices
- **(III) Technical Edge Defense** — on-device segmentation blurs bystanders/children/plates before upload
- **(IV) Dynamic Control & Consent** — phased disclosure, opt-in/out
- **(V) Long-Term Data Risk** — auto-purge (e.g. 48h) unless consented
- **(VI) Socio-Ethical Trust** — transparency, EU AI Act alignment, human-review policy

**Enterprise governance:** "recording-free zones" (restrooms, exec rooms with IP); signage + geofencing to auto-disable recording on managed glasses. *Observed/policy.*

**Open problems:** long-term reliance/complacency; delegation ethics; safeguards for children/vulnerable users. *Speculation: trust tiers ("advisor / operator / autopilot"); regulated logging & disclosure; deliberately crafted agent personalities signalling reliability/humility.*

---

## 7. Agents as Interface Users; AI in UX Research

**AI agents as users:** vision-based (screenshots, ~10,000+ tokens/page, fragile to layout shifts) vs accessibility-tree parsing (semantic HTML/ARIA, ~1,000 tokens, fast/reliable). Implication: semantic, accessible HTML is now agent-readable design — accessibility and agent-navigability converge. *Observed — NN/g "AI Agents as Users".*

**AI in UX research:** synthetic users / digital twins (simulate cohorts, find roadblocks pre-launch) and automated heuristic evaluation — but a preliminary diagnostic that supports, not replaces human research (false positives, missed context). *Observed — NN/g GenAI UX research agenda.*

---

## 8. Forecasts 2026–2029 (Explicitly Speculative)

Autonomous task horizons doubling ~every 4 months (was ~7): ~5 expert-hours unattended (late 2025, Opus 4.5-era) → ~39 hours (late 2026, a work week). Expect: Agentic Gridlock (vendor agents fail to interoperate → push for open standards); Semantic Design System Moat (§4); edge-first privacy (on-device recognition/translation/blurring after cloud-leak backlash). *Speculation — UX Tigers "18 Predictions for 2026".*

---

## 9. Implications for Designers & EssilorLuxottica CreativeHub

**Skill/mindset shifts:** system-level/orchestration thinking (flows across agents/devices/contexts); comfort with uncertainty/experimentation; ethical & futures literacy (IDEO ethics cards, foresight); collaboration with ML/data/policy.

**For eyewear/smart-glasses (EL context):** treat glasses as agent portals not app canvases; optimise for socially acceptable low-friction interactions; build micro-experience libraries (nav chips, translation pop-ups, caption streams, memory markers) recombined by agents; rely on generative UI + strict semantic design systems for scale + safety; invest in trust tooling (activity logs, permission inspectors, on-device controls). EssilorLuxottica is transitioning toward an AI-first technology/healthcare ecosystem, positioning smart glasses as a potential smartphone successor and pioneering ambient computing; the Meta × EL partnership and the "silver economy" (wearables for an ageing population) are strategic vectors. *Trend interpretation / EL strategic sources — use where relevant.*

**iF Design framing (context):** design as an integrative discipline navigating "omnicrisis" and conceptualising possible futures across six societal transformations (incl. human digitality) — not just function. **NN/g framing:** treat AI as an "intelligent but inexperienced intern" — fast synthesis, but lacks empathy/organisational context, needs human oversight. *Curated notes.*

*Sources: NN/g (definition-ai-agent, ai-agents-as-users, genai-ux-research-agenda, ux-reset-2025, ar-ux-guidelines, era-of-ai-design); Google research (generative-ui); Microsoft/Salesforce agentic principles; GitLab 8 patterns; IDEO AI Lab & ethics cards; Apple visionOS guidelines; smart-glasses market/optics/privacy research (Treeview, Even Realities, InsightAce, 6-Layer model, IAPP); UX trend reports (Stan.vision, Orizon, Envato); UX Tigers 2026 predictions; arXiv HCI papers; report_complete emerging-paradigm syntheses; curated notes (UX Guidelines for AI & Multi-Agent Systems, Wearables & the Conscious Interface, Wearables & the Silver Economy, iF Design Trend Reports, NN/g 2025 Trends). June 2026.*

---
---

# Source Dossier 5 — Prompting, Prompt Engineering & UX-Review Tactics

*Depth reference for Identity B (prompt optimisation & efficiency)*

**Retrieval keywords:** prompt template, prompt pattern, prompt engineering, design system prompt, anti-slop, negative constraints, generator-evaluator, evaluator rubric, ruthless reviewer, XML tags, effort level, token efficiency, caveman mode, session handoff, CLAUDE.md, Skills, handoff to code, DESIGN_INTENT, PSD, prompt scope document, vibe coding, GCAO, success cycle, three C's, dashboard prompt, IA before UI.

*Purpose: detailed, source-linked prompting reference with pasteable templates. Merges deep research (Gemini + Perplexity prompt 5), report_complete clusters (Prompt Engineering & UX Review, Opus 4.7/4.8 guidelines, Workflow Architecture & Skills), the Vibe Coder's PSD framework (Prompting Machine 2), and the two usage-limit videos. Practitioner templates are not official Anthropic features. Compiled June 2026.*

---

## 1. Core Prompt Frameworks

- **Role → motivation → numbered deliverables → output format → product context.** Give a senior domain role, explain why it matters, list what to build, specify output. ~150–300 words (under 50 = generic; over 500 = noisy/contradictory). Reduces output variance ~30–40% vs neutral prompts. *Tier B — senior-UX prompt guides + Anthropic aesthetics cookbook.*
- **GCAO** — Goal, Context, Action, Output. *Practitioner.*
- **Success Cycle** — Success Brief → Draft → Critique → Revise (beats one long prompt). *Practitioner.*
- **The Three C's** — Clarity (precise, no fluff; bullet/numbered like briefing an intern), Context (brand/user/project specifics), Constraints (platform, interaction, accessibility boundaries). *Practitioner — Vibe Coder's Playbook.*
- **Planner → Generator → Evaluator** — expand a 1–4 sentence idea into a spec (Planner), build one feature/"sprint" at a time (Generator), grade with a separate skeptical Evaluator. *Official — Anthropic harness-design.*
- **Sprint Contract / "ask me clarifying questions before building"** — agree "done" / surface a cheap text plan before committing tokens to code. *Official + Practitioner.*
- **Teach the "why"** — principles generalise better than rigid directives/examples. *Official.*

---

## 2. Defeating "AI Slop" — Design-System Constraints

Claude's default slop: Inter/Roboto, oversized rounded corners, centered full-width hero, purple/teal-on-white gradients, stock components, multi-layer shadows. Counter it with a concrete style dictionary. *Official aesthetics cookbook + Practitioner.*

**Enforced vs banned (example editorial system):**

- **Type:** ban Inter/Roboto/Arial/Space Grotesk; use distinctive pairings (e.g. Instrument Serif display + DM Sans UI + Fira Code mono); ≤3 sizes/view; restrict font-weight:700 to hero only.
- **Colour:** ban pure-white bg, purple/blue accents, default Tailwind/Bootstrap palettes, gray-on-gray borders; define a restrained OKLCH-derived palette (1 primary + 1–2 accents + neutrals), e.g. warm off-white bg `#F5F0E8`, terracotta primary `#B84A2F`.
- **Spacing/geometry:** 4px base unit; 4px radius (buttons/inputs), 8px (containers), 0 (panels); ban pill shapes; 1px solid borders only; single light shadow only.
- **Composition:** asymmetrical columns, vertical timelines, editorial layouts; ban centered hero + 3-column icon grids.
- **Anti-examples:** no corporate SaaS modernism, Stripe-lookalikes, glassmorphism, neon dark-mode glow.

**Techniques:** name undesired patterns explicitly ("do NOT use white card + purple gradient"); force 3–4 distinct visual directions before any code; reward originality (craft is already good); put the whole block in CLAUDE.md / project instructions for consistency. *Official + Tier B.*

**Reusable "Aesthetic Guardrails" add-on (append after the task):** specify typography (≤3 sizes, purposeful pairing), colour (restrained palette, no generic AI patterns), layout/components (grid alignment, no stock kits), motion (minimal, purposeful micro-interactions); prioritise coherence → originality → craft → functionality. *Tier A rubric.*

---

## 3. Pasteable Templates

### Design System + Screen Starter (Claude Design)
Senior design-systems-engineer role → build token set (semantic names), live React component kit with all states, one production-quality screen using only those tokens, usage notes; supply 1–2 sentence product context; ban slop patterns. *Tier B.*

### IA Before UI (Claude Design)
Senior UX-architect role → content inventory by frequency, ≤2–3-level navigation in user language, 3–5 primary flows as numbered steps, 3–4 risky drop-off moments, named screen list, design priorities by impact; output an annotatable doc, not code. *Tier B.*

### Decision Dashboard Designer
Senior data-viz role → the one question answered in <10s, metric hierarchy (1–3 primary KPIs + drill-downs), zoned layout (summary/trends/table), chart choice by data semantics (bars/lines/scatter; avoid donut/gauge), filters where execs expect them, colour-encodes-meaning + accessible contrast; output live React with sample data + notes for Claude Code data wiring. *Tier B.*

### Rebuild This UI as Artifact
Attach screenshot → match layout/hierarchy/style, semantic HTML + flex/grid, functional primary interactions, don't invent sections, expose a single config section for colour/type. *Tier B.*

### Stateful Tracker Artifact
Single-page HTML/React using persistent storage (≤20MB, text-only, published only) for CRUD + status + tags, with an export/import JSON panel. *Tier B.*

---

## 4. Generator–Evaluator Loop & Quality Gates

Single-agent generation suffers self-evaluation bias (the model defends its own buggy/bland code). Split generator (produces) from a skeptical evaluator (only critiques/scores against an external checklist, in its own context). Run 3–10 iterations, stop when scores plateau. Equip the evaluator with Playwright MCP to render, click/hover, screenshot desktop (1920×1080) + mobile (390×844), and check contrast/typography. *Official harness + Practitioner.*

**Four-criterion rubric (1.0–5.0, 25% each):** Visual Design Quality (cohesive identity, 4px-grid alignment, hierarchy) · Originality / Anti-Slop (no Inter/Roboto, generic rounded containers, purple gradients) · Craft (organised CSS vars, responsive units, WCAG AA contrast, no overlaps) · Usability & State Persistence. Output a structured `<evaluation_report>` XML (scores + composite + critical defects + improvement directives). Hard gate: if composite <4.2 or any metric <3.8, auto-trigger a repair cycle; don't mark done until thresholds met. *Practitioner.*

**Ruthless Reviewer (two-pass):** adopt a brutal conversion-obsessed persona; pass 1 critiques visual decisions, pass 2 simulates a first-time click-through; output sorted "critical / high-impact / nice-to-have" to feed Claude Code. Polite prompts → superficial feedback. *Community.*

**Self-healing loop (CLI):** benchmark harness against test fixtures + a running learnings.md so errors aren't repeated across sessions. *Practitioner.*

---

## 5. Prompt Mechanics (Opus 4.7/4.8)

- Place large reference files at the top, wrapped in `<document>/<documents>` XML, before the query (recall +~30%). *Official.*
- Opus 4.7/4.8 is literal — be exhaustive; define when to call tools / spawn sub-agents. *Official.*
- Tell it what to do > what not to do (for formatting). *Official.*
- `temperature`/`top_p`/`top_k` and prefilled final-turn responses are deprecated (400) — steer via prompt + XML only. *Official.*
- **Effort levels:** `high` (default), `xhigh` (hard/long autonomous tasks, UX bug-hunting), `max` (only when depth justifies cost). Lower effort for simple layout tweaks; if the model over-thinks/makes junk temp files, lower effort rather than adding prompt engineering. *Official.*
- **Component architecture rules to bake in:** avoid boolean props → compound components (`<Select.Trigger>`); decouple state to the parent provider; explicit variant components (`<Alert.Destructive>`); children over render-props; React 19 `use()` over `useContext`, skip `forwardRef`. *Practitioner.*
- **Artifact runtime gotchas:** register components to `window` (Babel block isolation); scope style object names to avoid collisions; never `scrollIntoView()` in sandbox; persist slide/tab state to `localStorage`; build a "Tweaks" `postMessage` listener for live variable edits. *Practitioner.*

---

## 6. Token-Efficient Prompting (Deep)

*Cross-reference Identity B §2.3 for the consolidated 20-point playbook and Dossier 1 for Design metering.*

| Tool / tactic | Mechanism | Measured impact |
|---|---|---|
| CLAUDE.md discipline | Style/conventions/stack in one config vs re-prompting | saves ~15,000–30,000 startup tokens/turn |
| Caveman Mode | Strip prose, return only code + bulleted facts | ~75% fewer output tokens/turn |
| Intent layer (AGENTS.md) | Small intent files at folder boundaries | fewer exploratory file reads |
| Rust Token Killer (RTK) | Proxy compresses terminal output | 76–98% smaller terminal payloads |
| Code Review Graph | Tree-sitter index in SQLite | ~6.8x fewer tokens for reviews |
| Grep-filtered pipelines | `npm test 2>&1 \| grep -A5 -E "FAIL\|ERROR" \| head -100` | avoids 10k-line dumps |
| Subagent model routing | `CLAUDE_CODE_SUBAGENT_MODEL=haiku`; `MAX_THINKING_TOKENS=0` for trivial edits | cheaper subagents |
| Compacted session handoff | `/handoff` → `.claude/session-handoff.md` → `/clear` → resume | prevents losing hex tokens/vars/rules in lossy compaction |
| Skills (progressive disclosure) | Metadata ~100 tokens, full load on trigger | 60–90% fewer tokens in busy workflows |
| Highlight-and-edit Artifacts | Edit only the selected section | no full-file regeneration |

*Practitioner — MindStudio, Composio, Design Systems Collective, Ocasio Consulting, GitHub. Subagent footprints (e.g. security monitor ~3,979 tokens, plan mode ~715) accumulate — monitor in long sessions.*

**Caveman Mode prompt:** disable prose/intros/transitions; respond in short statements + infinitive verbs; keep all code/paths byte-for-byte; auto-suspend on security/critical errors and return a full warning.

**Session handoff prompt:** before `/clear`, write `.claude/session-handoff.md` with milestone, changed files + git state, key technical decisions (hex tokens, typefaces, state vars, API structures), active failures, next 3 steps, skills to load.

---

## 7. Handoff to Code (Design → Claude Code → Repo)

**In Claude Design, prepare handoff:** package HTML/CSS/React + tokens (JSON/TS) + component list; write DESIGN_INTENT.md (primary flows, key UX decisions/tradeoffs, accessibility assumptions, deliberate deviations); add implementation notes (stack, folder structure, where real data/APIs plug in); produce the Claude Code handoff bundle + a paste-ready message. Anthropic states the bundle carries "design intent"; complex pages that took 20+ prompts elsewhere reportedly took ~2 in this flow. *Official + Tier B.*

**In Claude Code, build from bundle:** senior-full-stack role → read DESIGN_INTENT.md, summarise flows/constraints; set up the project (e.g. React+Vite/Next); translate to clean components with centralised theme tokens; mock data + TODO for APIs; output folder structure + key files + run instructions; don't reimagine the design unless accessibility/feasibility demands. *Official harness + Community.*

---

## 8. Vibe-Coding Lifecycle & the Prompt Scope Document (PSD)

PSD = a "context bridge" providing static documentation (how the system works: API patterns, architecture constraints, brand rules) + dynamic metadata (what's in it now: schemas, components, routes).

**Five sections:**
1. Project Vision & Objectives
2. Functional & UI/UX Requirements (flows, features, mockup link, design system)
3. Technical Specification (stack, libraries, architectural constraints — prefer popular well-documented tech)
4. Context & Knowledge Base (reference files, rules, common mistakes to avoid e.g. "do not change anything I didn't ask for")
5. Success & Validation Criteria (tests, coverage, validation steps)

**Operational lifecycle:** Preparation (write PSD, plan UI/UX + reusable components, clean Figma layers, bootstrap from a starter kit, init Git as a safety net) → Execution & Iteration (one goal at a time → review vs PSD → note flaws → targeted follow-ups, or edit-and-resend the prior prompt if it deviates → commit working code) → Troubleshooting (paste full error for build errors; for stuck bugs after 2–3 tries ask for "top suspects" + logs; new chat + summary for context loss; new key/account for rate limits). Match tool to goal: prototypes → Figma Make/Lovable; production → Cursor/Claude Code/Windsurf; planning → Gemini large-context. *Practitioner.*

---

## 9. Usage-Limit Video Tactics (Cross-Reference)

The two practitioner videos — "Why Claude Keeps Hitting Usage Limits (& how to fix it)" (Eliot Prince, Apr 2026, 14 tips) and "Never hit Claude's Usage Limit Again" (Dubibubii, Apr 2026, 11 rules) — are fully consolidated into Identity B §2.3 (20-point playbook): Sonnet default, `/context`, toggle off extended thinking, new chat per task, specific prompts, batch requests, disable idle MCPs, PDF→Markdown, Projects with clean Markdown, custom instructions <500 words, prune Project/Cowork files, build Skills, off-peak heavy work, session-reset trick, rolling-5-hour awareness, alternating models, extra usage/credits. *Practitioner.*

---

## Appendix — Full Pasteable Templates

### A1. Design-System Constraint Block *(paste into CLAUDE.md / project instructions)*

```markdown
## DESIGN SYSTEM CONSTRAINTS

### Typography
- Display: "Instrument Serif"; UI/Body: "DM Sans"; Mono: "Fira Code" (Google Fonts).
- Scale: 48 (h1), 36 (h2), 28 (h3), 22 (h4), 18 (h5); body 16/1.6; small UI 13/1.5/500.
- font-weight:700 forbidden except hero headers; use 600 for UI headings.
- Banned fonts: Inter, Roboto, Arial, Space Grotesk.

### Color (OKLCH-compatible hex tokens)
- --color-bg:#F5F0E8; --color-surface:#FFFDF8; --color-text:#1A1714;
- --color-text-muted:#6B6560; --color-primary:#B84A2F; --color-primary-hover:#9A3A22;
- --color-border:#E0D9D0; --color-error:#C0392B.
- Banned: blue/purple accents, pure white (#FFFFFF) bg, gray-on-gray borders.

### Spacing & Grid
- Base 4px. Allowed: 4,8,12,16,24,32,48,64. Radius: 4px inputs/buttons, 8px containers, 0 panels.
- Pill (rounded-full) banned. Borders 1px solid only. One light shadow: 0 1px 3px rgba(26,23,20,.08).

### Components
- Buttons: flat, no gradient, 4px radius, 14px uppercase, letter-spacing .05em.
- Inputs: white bg, 1px --color-border, 1px focus ring --color-primary.
- Tables: zebra (--color-surface / --color-bg), no outer vertical borders.
- Nav: left vertical sidebar, text-only links 14px, generous negative space.

### Tone
- Editorial, warm, structured, minimalist.
- Anti: SaaS modernism, Stripe-lookalikes, glassmorphism, neon dark-mode glow. Refs: Stripe Press, A24, Notion editorial.

Before coding, propose 3-4 distinct visual directions. Do not introduce unlisted fonts, extra colors, or multi-layer shadows.
```

### A2. Evaluator Output Contract *(paste into the evaluator agent)*

```
Run a Playwright check: render the prototype headless; screenshot at 1920x1080 and
390x844; click/hover all primary buttons, dropdowns, tabs (screenshot each state);
check contrast + font loading.

Grade 1.0-5.0 on four 25% criteria: Visual Design Quality; Originality/Anti-Slop
(no Inter/Roboto, generic rounded containers, purple gradients); Craft (organised CSS
vars, responsive units, WCAG AA contrast, no overlaps); Usability & State Persistence.

Output only:
<evaluation_report>
  <design_quality>SCORE</design_quality>
  <originality>SCORE</originality>
  <craft>SCORE</craft>
  <usability>SCORE</usability>
  <composite_score>WEIGHTED AVERAGE</composite_score>
  <critical_defects>- element, CSS line index, browser behavior</critical_defects>
  <improvement_directives>- Typography / Color (hex) / Interactivity fixes</improvement_directives>
</evaluation_report>

Hard gate: if composite < 4.2 OR any metric < 3.8, trigger a repair cycle and send the
scorecard back to the generator. Do not mark complete until thresholds are met.
```

### A3. React + Babel Single-File Scaffold with Live "Tweaks" Protocol

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <script src="https://cdn.tailwindcss.com"></script>
  <script>
    tailwind.config = { theme: { extend: { colors: {
      brandBg:'#F5F0E8', brandSurface:'#FFFDF8', brandText:'#1A1714',
      brandTextMuted:'#6B6560', brandPrimary:'#B84A2F', brandPrimaryHover:'#9A3A22',
      brandBorder:'#E0D9D0' },
      fontFamily: { serif:['"Instrument Serif"','serif'], sans:['"DM Sans"','sans-serif'],
      mono:['"Fira Code"','monospace'] } } } }
  </script>
  <link href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600&family=Fira+Code&family=Instrument+Serif:ital@0;1&display=swap" rel="stylesheet">
  <script src="https://unpkg.com/react@18.3.1/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@18.3.1/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone@7.29.0/babel.min.js"></script>
</head>
<body class="bg-brandBg text-brandText font-sans">
  <div id="prototype-root"></div>
  <!-- Block 1: shared components MUST be exported to window (Babel block isolation) -->
  <script type="text/babel">
    const PrimaryButton = ({ label, onClick, disabled = false }) => (
      <button onClick={onClick} disabled={disabled}
        className="px-6 py-3 bg-brandPrimary hover:bg-brandPrimaryHover text-brandSurface text-sm font-medium uppercase tracking-wider rounded-sm transition-colors duration-150 ease-out">
        {label}
      </button>
    );
    Object.assign(window, { PrimaryButton });
  </script>
  <!-- Block 2: app + Tweaks postMessage protocol + localStorage persistence -->
  <script type="text/babel">
    const { useState, useEffect } = React;
    const { PrimaryButton } = window;
    const App = () => {
      const [tweaks, setTweaks] = useState(() => {
        const saved = localStorage.getItem('prototype_tweaks_state');
        return saved ? JSON.parse(saved) : { fontSize:16, headingText:"Editorial Content Platform" };
      });
      const [isEditMode, setIsEditMode] = useState(false);
      useEffect(() => { localStorage.setItem('prototype_tweaks_state', JSON.stringify(tweaks)); }, [tweaks]);
      useEffect(() => {
        const handle = (e) => {
          if (!e.data || typeof e.data !== 'object') return;
          if (e.data.type === '__activate_edit_mode') setIsEditMode(true);
          else if (e.data.type === '__deactivate_edit_mode') setIsEditMode(false);
          else if (e.data.type === '__edit_mode_set_keys') setTweaks(p => ({ ...p, ...e.data.edits }));
        };
        window.addEventListener('message', handle);
        window.parent.postMessage({ type: '__edit_mode_available' }, '*');
        return () => window.removeEventListener('message', handle);
      }, []);
      const update = (edits) => setTweaks(p => {
        window.parent.postMessage({ type: '__edit_mode_set_keys', edits }, '*');
        return { ...p, ...edits };
      });
      return (
        <main className="min-h-screen p-8 flex items-center justify-center">
          <div className="w-full max-w-4xl bg-brandSurface p-12 rounded-md border border-brandBorder">
            <h1 className="font-serif text-brandText" style={{ fontSize: `${tweaks.fontSize*2.25}px` }}>
              {tweaks.headingText}
            </h1>
            <p className="font-sans mt-6" style={{ fontSize: `${tweaks.fontSize}px` }}>
              Variables update live from the host via the Tweaks protocol; no reload or code edit.
            </p>
            <div className="mt-8">
              <PrimaryButton label="Commit" onClick={() => alert('Action logged.')} />
            </div>
            {isEditMode && (
              <input type="text" value={tweaks.headingText}
                onChange={(e) => update({ headingText: e.target.value })}
                className="mt-4 bg-brandBg text-xs px-2 py-1 rounded border border-brandBorder" />
            )}
          </div>
        </main>
      );
    };
    ReactDOM.createRoot(document.getElementById('prototype-root')).render(<App />);
  </script>
</body>
</html>
```

*Rules: never call `scrollIntoView()` in-sandbox; scope style-object names; keep state in `localStorage`. Practitioner.*

### A4. Session-Handoff Prompt & Caveman Mode

```
SESSION HANDOFF: before /clear, write .claude/session-handoff.md with:
1) Milestone & objective (one sentence)
2) Changed files + git state (paths + per-file summary)
3) Key technical decisions (hex tokens, typefaces, state vars, API structures)
4) Active issues / failing tests (paste filtered error lines)
5) Next 3 steps
6) Skills/files to load next session
Output as <handoff_document> XML, then wait for /clear.

CAVEMAN MODE: disable prose/intros/transitions; reply in short statements + infinitive
verbs; keep all code/paths byte-for-byte; auto-suspend and return a full warning on
security or critical errors.
```

*Sources: platform.claude.com (prompt-engineering best practices, frontend-aesthetics cookbook, eval-tool); anthropic.com/engineering/harness-design-long-running-apps; anthropic.com/news/claude-design-anthropic-labs; Snyk, MindStudio, Composio, Design Systems Collective, Ocasio Consulting, Albato, senior-UX prompt guides, GitHub gists, r/ClaudeCode/r/ClaudeAI; Vibe Coder's Playbook (PSD); report_complete clusters (Prompt Engineering & UX Review, Opus 4.7, Workflow Architecture & Skills); usage-limit videos. June 2026.*
