# CreativeHub Claude — Knowledge Base (Compact)
*June 2026. Order: Identity A → B → C → Source 1 → 2 → 3 → 4 → 5*

---

# Identity A — Claude Capabilities Guide
*When a colleague asks which surface to use or what Claude can/can't do.*

## Surface Decision Matrix

| Task | Best surface | Switch when |
|---|---|---|
| Brainstorm, draft, quick specs | Chat | Multi-day shared docs → Projects; visuals → Design |
| Ongoing initiative with many docs | Projects | Reusable workflow → Skills; local files → Cowork |
| Reusable procedure (review recipe, template) | Skills | Per-project only → Projects |
| Autonomously act on local files/apps | Cowork (paid, Desktop) | No local access wanted → Chat; code-centric → Code |
| Coding, refactors, CI | Claude Code | Non-code agentic work → Cowork; visuals → Design |
| Prototypes, mockups, decks | Claude Design | Ideation → Chat; implementation → Code/Canva |

**Optimal pipeline:** concept in Chat → visuals in Design → implementation in Code.

---

## Claude Chat
200K context; rolling 5-hour usage window; Incognito mode; web search; attachments up to 500MB/20 files. Threads are isolated — no cross-thread context; browser sandbox can't touch local files.
*Use for:* microcopy, WCAG spot-checks, interview note clustering.

## Claude Projects
Persistent workspace with knowledge base + custom instructions. RAG auto-expands capacity ~10x on paid plans. Free = 5 projects max. No auto file-sync; not API-accessible; sharing only on Team/Enterprise.
*Best practice:* three-file baseline (brand voice + persona + past work); one project = one focus; fix systemic errors in instructions, not in chat.

## Claude Agent Skills
SKILL.md packages with progressive disclosure (~100 tokens metadata on load, full instructions on trigger). Install in web (Pro+), `~/.claude/skills/` (Code), or API beta headers. Pre-built Office skills (pptx, xlsx, docx, pdf). Not ZDR-eligible; ~36% of community skills contain prompt injections — scan before use.
*Use for:* portable review recipes, token-compliance audits, deck standards.

## Claude Cowork
Agentic desktop mode. "Computer Use" (screenshot/click/type) + isolated Linux VM. Paid + Desktop only. Data stored locally — no cloud sync, no audit logs (Enterprise → OpenTelemetry). Folder access = read/edit/delete rights; keep boundaries strict. Multi-step tasks burn 50–100x tokens vs a normal message.
*Workspace:* `context/` (rules), `projects/`, `output/`; CLAUDE.md < 300 lines; memory.md < 150 lines + archive.md.

## Claude Code
Agentic CLI. Install: `curl -fsSL https://claude.ai/install.sh | bash` (mac/Linux) or `npm install -g @anthropic-ai/claude-code`. Plan Mode (Shift+Tab), `/autofix-pr`, `/batch` (parallel sub-agents), `/compact` before ~70% context. Shares usage quota with Chat and Design. Avoid `--dangerously-skip-permissions`.

## Claude Design
Research preview, web only (claude.ai/design), Pro/Max/Team/Enterprise. Opus-powered canvas + chat. Ingests codebases/PDFs/decks into a published design system. Outputs interactive HTML/CSS/JS artifacts. Inline comments + Tweaks sliders. Exports: HTML, ZIP, PDF, PPTX, Canva, Claude Code handoff bundle.
**Limitations:** no raster image/video generation; inline comments can disappear → paste feedback into chat; compact-layout mode causes save errors → switch to full view; raw exported code is often an unmaintainable blob (prototyping only, not production).
**Metering conflict (present both):** Official docs say Design has its own independent weekly meter. Community reports say it was merged into the standard 5-hour pool, with a single edit consuming 20–40% of it. Verify at the live pricing page.

## Artifacts & Generative UI
Trigger: output >15 lines, self-contained, likely to be reused. Types: Markdown, code, HTML, SVG, Mermaid, React. Sandboxed client-side — no external API/DB calls. Persistent storage 20MB/artifact, text-only. MCP-connectable on Pro/Max/Team/Enterprise. Start from a Minimal Viable Artifact; use "Remix" for iteration.

## Models (2026)
- **Opus 4.7/4.8** — flagship reasoning/vision, 1M context, literal instruction-following, stubborn house style (override with explicit design system). `temperature`/`top_p`/`top_k` deprecated → steer via prompt only. Effort levels: `high` (default), `xhigh`, `max`.
- **Sonnet 4.6** — everyday workhorse, far cheaper.
- **Haiku** — fast/cheap, latency-sensitive tasks.

## MCP & Enterprise
10,000+ public MCP servers. Allowlist only needed tools (`enabled:false` default); `defer_loading:true` keeps descriptions out of context. Remote MCP needs HTTP/SSE bridge. MCP data exempt from ZDR. Treat connector output as untrusted (injection vector). Team/Enterprise data excluded from training by default.

## Claims to Avoid (Global)
Flawless Figma import, exact token extraction, two-way Figma sync, production-ready code from Design, native image/video generation, unlimited usage, injection-safe MCP outputs, reliable single-pass self-evaluation of aesthetics.

---
---

# Identity B — Best Practices & Efficiency
*When a colleague wants prompt optimisation or is hitting usage limits.*

## Core Prompt Frameworks
- **GCAO** — Goal, Context, Action, Output.
- **Success Cycle** — Brief → Draft → Critique → Revise (beats one long prompt).
- **Planner → Generator → Evaluator** — Claude is lenient on its own work; always use a separate evaluator.
- **Sprint Contract** — agree "done" before writing any code.
- **Teach the "why"** — principles generalise better than rigid rules.
- Prompt length sweet spot: ~150–300 words. Under 50 = generic; over 500 = noisy.

## Breaking "AI Slop"
Opus 4.7/4.8 defaults: Inter/Roboto, oversized rounded corners, centered hero, purple/teal gradients, stock components. To escape:
- Set an explicit design system before any generation.
- Force 3–4 distinct visual directions before writing code.
- **Ban by name:** Inter, Roboto, generic purple/teal gradients, white card + shadow combos, Corporate Memphis illustration.
- Mandate distinctive type pairings with extreme weight contrast (e.g. 100 vs 900).
- Upload competitor screenshots ≥1000×1000px; instruct "adapt, don't copy 1:1".
- Use principle-based / evocative language ("museum quality") over prescriptive commands.

## Prompt Structure Mechanics
- Place large reference files at the top in `<document>` XML tags (recall +~30%).
- Tell Claude what to do, not only what not to do.
- Opus 4.7/4.8 is literal — be exhaustive about when to call tools or spawn sub-agents.
- Max 1–2 interaction types per prompt, phrased "if supported / where reasonable".
- Treat attachments as visual direction references, not exact token sources.

## Reviewing Designs
Ruthless Reviewer persona + two-pass loop: pass 1 critiques visual decisions, pass 2 simulates a first-time user click-through. Output sorted "critical / high-impact / nice-to-have". Polite prompts → superficial feedback.

## Plan Tiers *(as reported, June 2026 — verify)*
| Plan | ~Monthly | Notes |
|---|---|---|
| Free | $0 | No Design, no file creation/code execution |
| Pro | ~$20 | Independent weekly allowance; exhausts fast on Design |
| Max 5x | ~$100 | ~5x Pro; all Opus models |
| Max 20x | ~$200 | ~20x Pro; priority queue |
| Team | ~$100+/seat | Per-seat allowance, SSO |
| Enterprise | Negotiated | Seat-based or usage-based |

Usage credits (when allowance depleted): ~$45→$50 (10%), ~$200→$250 (20%), ~$700→$1,000 (30%).

## Token-Saving Playbook (20 Points)
**Session hygiene:** (1) fresh chat per task type; (2) `/compact` before ~70% context; (3) edit previous messages instead of follow-ups; (4) batch requests into one prompt; (5) use structured handoff files for long work.
**Model routing:** (6) Sonnet for routine, Opus for complex review; (7) lower effort level for simple tasks; (8) toggle off extended thinking when not needed.
**Inputs:** (9) disable idle MCPs before a session; (10) cache Figma data locally in `.claude/` Markdown files; (11) convert PDFs to Markdown; downsample images to 1080p unless 1:1 needed; (12) prefer YAML > Markdown > XML > JSON.
**Projects/Skills:** (13) put recurring files in Projects, not per-chat uploads; (14) keep CLAUDE.md < 300–500 lines; cap memory.md ~150 lines; (15) encode repeated prompts as Skills; (16) prune stale files from Projects/Cowork.
**Design:** (17) never upload a full monorepo — isolate subdirectories; (18) use the on-canvas Edit tool for copy (no generation tokens); (19) route stable code refinement to a cheaper tool (e.g. Codex, ~3–4x fewer tokens).
**Timing:** (20) heavy work at off-peak hours; know your rolling 5-hour reset; alternate models.

## Evaluation Checklist
- Request narrowed to one output / one section / one breakpoint?
- Negative constraints + evaluation criteria included?
- Cheapest adequate model + effort level chosen?
- Only needed files/tools/MCPs loaded, references at the top?
- At least one token/credit-saving step included?
- No promises of guaranteed interactivity or guaranteed token reduction?

---
---

# Identity C — Future Interfaces & Trends
*When a colleague asks about trends, emerging UX patterns, or how to design for them.*
*All items marked Forward-looking or Trend interpretation are speculation — never Claude capability claims.*

## 1. Probabilistic UX
The WIMP contract (same input → same output) is being replaced. AI systems infer by confidence; identical inputs can yield variable outputs. The designer's job shifts from drawing screens to defining **confidence thresholds** — when a system acts autonomously vs asks for intervention.

| Dimension | Deterministic | Probabilistic |
|---|---|---|
| Behaviour | Predictable, rule-bound | Adaptive, confidence-based |
| Errors | Hard failures | Graceful degradation, rollback |
| User role | Operator | Collaborator / supervisor |
| Explainability | Rarely needed | Often required |

**Uncertainty toolkit:** confidence indicators, progressive disclosure of reasoning, latency as a trust canvas (narrate background steps), reversible interventions (undo/edit/retry as primary controls).

## 2. Agentic UX & Human-on-the-Loop
Move from approve-every-action (in-the-loop) to monitor-and-intervene (on-the-loop). Dynamic intervention thresholds are contextual and risk-based: autonomous calendar drafts OK; explicit approval for sending emails or transactions. Needs visible pause/veto/override/rollback at all times.

**Enterprise architecture (4 layers):** engagement (interface) · agency (agents) · work (apps/APIs) · data.
**8 agentic collaboration patterns (GitLab):** status updates, work routing, team comms, role-specific chat, conversational context, RBAC, governed environments, collaborative building.
Evaluate agent behaviour with IDEO-style low-fi prototypes before any high-fidelity build.

## 3. Generative & Adaptive UI
Layouts compiled in real time from user intent, not hard-coded. Documented outcomes: fintech replaced 6 static dashboards with 1 adaptive view → support tickets −27%; context-driven onboarding cut time from ~12 min to <5.
**Semantic Design System Moat (forward-looking):** as generative UI compiles from briefs, competitive advantage shifts from layout libraries to consistent semantic design systems. Inconsistent tokens → fragmented output.

## 4. Ambient AI & New Materiality
- **Ambient AI:** assistance recedes into background (predicting form fills, reordering nav by usage) rather than explicit "Ask AI" prompts.
- **Intelligent reduction:** premium UX suppresses irrelevant detail and hides low-confidence recommendations.
- **Apple Liquid Glass (iOS 26):** translucency + micro-refraction. Apple shipped a "turn off" toggle 7 weeks in after clutter complaints — depth/motion must serve communication, not decoration.
- Generic flat illustration ("Corporate Memphis") is declining.

## 5. Smart Glasses & Wearable Ecosystem
Market: ~$2.9B (2025) → $8.4B+ (2035), ~11.6% CAGR. Meta × EssilorLuxottica (Ray-Ban, Oakley) is central. Key constraint: must look/feel like normal eyewear for all-day wear.

**Five 2026 paradigms:** AI Glasses (no display, ~51g — Ray-Ban Meta Gen 2) · Display Glasses (small HUD) · AR Glasses (waveguide/micro-LED, 30–80g) · AR Display Glasses (tethered monitors) · Smart Sunglasses (audio-first).

**Input barriers:** touch fails in rain/gloves; voice is socially awkward → shift toward **camera-as-input** ("shared visual context"). Design principles: glanceable text-minimal overlays, intermittent not continuous attention, obvious capture signalling, cross-device choreography (glasses capture/glance; phone for deep work).

## 6. Multimodal Input & Gaze

| Modality | Strength | Weakness | Handoff to |
|---|---|---|---|
| Voice | Fast, hands-free | Low precision, noise | Touch / HUD text |
| Touch | Absolute precision | Needs attention | Voice / overlay |
| Gesture | Intuitive, 3D | Gorilla-arm fatigue | Gaze + confirm |
| Gaze | Rapid targeting | "Midas Touch" mis-triggers | Pinch / EMG |
| EMG/neural | Ultra-low strain | Calibration noise | Voice + gesture |

Gaze-to-select + pinch-to-confirm (Apple Vision Pro) solves the Midas Touch problem. Wrist-worn EMG (Meta neural band, Mudra) enables "Air-Touch" from intended finger movement.

## 7. Privacy & Trust (Wearables)
**6-Layer Privacy & Consent Model:**
1. Social Visibility — LEDs visible at 10m
2. Electronic Notification to nearby devices
3. Technical Edge Defense — on-device segmentation blurs bystanders before upload
4. Dynamic Control & Consent — phased disclosure, opt-in/out
5. Long-Term Data Risk — auto-purge (e.g. 48h) unless consented
6. Socio-Ethical Trust — EU AI Act alignment, transparent human-review policy

Enterprise: designate recording-free zones (restrooms, exec rooms); geofencing to auto-disable recording on managed glasses.

## 8. Agents as Interface Users
Vision-based agents: ~10,000 tokens/page, fragile to layout shifts. Accessibility-tree parsing (semantic HTML/ARIA): ~1,000 tokens, fast/reliable. **Implication: accessible HTML is now agent-readable design** — accessibility and agent-navigability converge.

AI in UX research: synthetic users/digital twins are useful as a preliminary diagnostic only — not a replacement for human research.

**Forecasts 2026–2029 (speculative):** autonomous task horizons doubling ~every 4 months; ~39 hours unattended work (a full work week) projected by late 2026. Expect Agentic Gridlock (cross-vendor interop failures) and edge-first privacy (on-device blurring/translation after cloud-leak backlash).

## 9. EssilorLuxottica Context
EL is transitioning toward an AI-first technology/healthcare ecosystem. Smart glasses as a potential smartphone successor. Meta × EL partnership (Ray-Ban, Oakley) + "silver economy" (wearables for ageing population) are strategic vectors. CreativeHub design work increasingly targets face-worn, glanceable, multimodal, privacy-sensitive ambient experiences.

---
---

# Source 1 — Claude Design: Deep Dossier

## What It Is
Research preview at claude.ai/design. Pro/Max/Team/Enterprise only (Enterprise: admin must enable). Dual-pane: chat + live interactive canvas (HTML/CSS/JS artifacts, not static rasters). Not a Figma replacement — best for 0→1 prototyping, variants, decks.

## Design-System Ingestion
Parses codebases, PDFs, slide decks, design files → auto-generates UI kit (colours, type, spacing, components). Toggle "Published" to make it the team default. Multiple design systems can coexist. **Caveat:** treats Figma uploads as a starting point — frequently misses component variables, disabled states, and hallucinates type scales.

## Exports & Handoff
Standalone HTML · ZIP · PDF · PPTX · Canva (via HTML import) · Claude Code handoff bundle (tokens + components + layout notes). No native Design→Figma export. Canva workaround: export as PPTX at exact pixel dimensions, then upload to Canva for full vector editability.

## Known Bugs
- Inline comments disappear → paste feedback into chat instead.
- Compact-layout mode causes save errors → switch to full view.
- Large monorepos cause lag/crashes → link specific subdirectories.
- "Chat upstream errors" lock a session → open a new chat tab.
- Mobile↔desktop responsiveness needs manual CSS.
- Unsubscribing can lock you out → export data first.

## Metering (Conflict — Present Both)
**Official (May 2026):** Design has its own independent weekly meter, never draws from chat/Code limits. **Community:** isolated Design limit reportedly removed, merged into the standard 5-hour pool; single edit = 20–40% of that limit; Anthropic reportedly doubled Design token limits temporarily (~through July 13). **→ Verify the live pricing article before quoting.**

## Token Economics (API/Enterprise)
Opus 4.6/4.7/4.8: $5/MTok input, $25/MTok output. Prompt caching cuts long-prompt cost up to ~90%. Token-efficient tools beta cuts output tokens up to ~70%. Batch API: ~50% discount. Opus 4.7+ tokenizer = ~1.0–1.35x more tokens than 4.6 — re-baseline old estimates.

## Figma MCP Handoff
**Officially supported (extraction via Claude Code only):**
- `claude plugin install figma@claude-plugins-official` → read live nodes/tokens/metadata.
- `claude mcp add --transport http figma https://mcp.figma.com/mcp --scope user` → `get_design_context`.
- Claude Code can convert browser UI (prod/staging/localhost) to editable Figma frames.

**Not guaranteed:** community write-injection tools (FigClaw, etc.) are fragile and unsupported.
**3-part prompt structure to avoid failures:** (1) what to build, (2) target Figma file URL, (3) exact name of the published design-system library.

## Multi-Tool Token Routing
Low-fi in Google Stitch (free) → hi-fi in Claude Design → manual tweaks in Figma → code refinement in Codex (~3–4x fewer tokens). Build design-system foundations manually (buttons, type scales) — AI hallucinates states and burns tokens. Group components into categorised .md files (Form Elements, Navigation, Data Display).

## File Limits
Per chat: 20 files, 500MB/file, images up to 8000×8000px. Projects: 30MB/file. PDFs >100 pages → text-only (loses charts/typography). Images ≥1000×1000px recommended.

---
---

# Source 2 — Claude Surfaces: How-To & Ecosystem

*Detailed setup and feature reference for each surface. Full decision matrix and surface-by-surface how-to. Cross-reference Identity A for routing logic.*

## Key Additions vs Identity A

**Projects — Cowork Projects differ:** local desktop workspaces with own instructions, scheduled tasks, project-scoped memory; stored locally, no Team/Enterprise sharing yet.

**Skills — API install:** beta headers `code-execution-2025-08-25`, `skills-2025-10-02`, `files-api-2025-04-14` + `container.skills`. Open-source examples at `github.com/anthropics/skills`.

**Code — Node requirements:** Node 18+, macOS 13+/Win 10+/Linux/WSL. Key commands: `/init`, `claude doctor`, `@claude` on GitHub, `/effort`, `/compact`, `/context`, `/batch`, `/autofix-pr`.

**MCP — Storage & security:** store MCP secrets in OS keychain via Desktop manifest, not in the prompt. `mcpResourceToContent` injects resources as content blocks. `defer_loading:true` keeps tool descriptions out of context until queried.

**Creative connectors ("Claude for Creative Work"):** Ableton, Adobe (50+ CC tools), Affinity by Canva, Autodesk Fusion, SketchUp, Blender (via MCP → Python API).

---
---

# Source 3 — Competitive Landscape (2026)

## Market Context
The historical split between visual canvas and functional code is dissolving. Design systems become the primary artifact; individual screens become ephemeral. Designers shift from visual production to visual judgment and constraint-setting. Risks: aesthetic mode collapse, skipping IA/accessibility because mockups are cheap, de-skilling.

## Tool-by-Tool Summary

| Tool | Best for | Key strength | Key weakness | Pricing |
|---|---|---|---|---|
| **Claude Design** | Designers, PMs, founders | Brand-aware, code-aware handoff, multi-modal | Research preview, slow render, no native Figma export | Bundled in Pro/Max/Team/Ent |
| **Figma (AI/Make)** | Pro UI/UX designers | Design-system depth, mature ecosystem | AI breaks Auto Layout, Make code not prod-ready | Free → ~$16–90/seat |
| **Google Stitch** | Prototypers, early alignment | Fast, free, voice, DESIGN.md | Labs beta, "pretty but useless", mobile > web | Free (~300 credits/day) |
| **Vercel v0** | Frontend/React devs | High-quality React/Tailwind code, full-stack | Component-to-app gap, stack lock-in | Free → $20–30/user |
| **ChatGPT Canvas** | Writers/coders | Strong text/code editing | No design canvas, no Figma | Free/Plus ~$20 |
| **Gemini Canvas** | Students, business | SVG rendering, abstract aesthetics | Experimental, limited export | Google AI Pro/Ultra |
| **Lovable** | Founders, no-code | Full-stack apps, Visual Edits | Weak backend, dropped Figma import | Free → $25/$50 |
| **Replit Agent** | Full-stack builders | Sketch→app, DB/auth, Figma MCP | App conversion needs paid plan | Canvas free, app paid |

## When to Choose Claude Design
**Yes:** unified design→code workflow on Claude Code; prototypes needing rich interactivity (voice/video/3D/AI); brand-consistent output from codebase on day one; collaborative exploration with PMs/non-designers.
**No:** large teams needing standardised design at scale (Figma); developer-led React/Next (v0); zero-budget early experimentation (Stitch/Uizard); content-first writing/coding (ChatGPT Canvas/Gemini).

## Claude vs ChatGPT/Gemini
Claude: execution/compilation sandbox (React/HTML runs live, persistent storage, MCP-extensible, Skills/Code automation). Superiority: premium polished UI out-of-the-box, large-context analysis (200K–1M). Weakness: strict rate limits, no native image/video generation, token economy burns fast on heavy iteration.

---
---

# Source 4 — Emerging Interfaces & Experience Patterns (2025–2028)

*Full depth reference behind Identity C. "Observed" = current products/research. "Speculation" = reasoned 2–3-year predictions.*

## Agentic UX — Design Patterns
**Observed UI patterns (2024–26):** delegation canvases (goal/constraints/resources/success criteria); plan previews with editable steps; simulation/dry-run modes for high-risk tasks; mixed-initiative corrections; agent state/memory panels ("what I know / assumptions / context").
**Design principles:** outcomes not screens; progressive autonomy (assistive → semi → autonomous as trust grows); tunable risk (scope, reversibility, notification intensity); graceful failure + repair flows.

## Ambient Computing
**Observed patterns:** environment-anchored UI (Vision Pro anchors windows to furniture); peripheral cues over central focus (haptic taps, one line of text); context-aware modality (voice/haptics walking, visuals seated); multi-device orchestration.
**Principles:** respect the environment (translucent, adapts to real lighting); favour glances over sessions; anchor to meaningful objects/activities; signal active sensors.

## Smart Glasses — Technical Detail
Waveguide optics: "light highways" route a temple micro-projector to the pupil; ~9mm eyebox; corrects chromatic dispersion. Descend from 1940s cockpit HUDs and the 1988 Oldsmobile windshield HUD.

**Observed eyewear UX patterns:** glanceable text-minimal overlays ("smallest screen in the world"); micro-experiences not apps (translation on hearing a phrase, hands-free "remember this"); spatial ergonomics (white type on translucent glass, bold weights, ~60pt targets).

**Speculation (2027):** mainstream "companion glasses" (nav/translation/light agent, heavy work stays on phone); agent-centric eyewear (agent front replaces home screen); multi-accessory mesh (glasses + pin + ring + earbuds).

## Generative UI — Depth
**Principles:** constrain the space (UI grammars, design tokens, component libraries); make adaptation explainable; human-in-the-loop oversight; maintain identity/consistency.
**Open problems:** over-personalisation harms learnability; mis-generated UI can hide controls or break accessibility; versioning/QA of runtime-variable UIs.

## Trust & Privacy — Depth
**Trust patterns:** transparent capability boundaries; stepwise confirmation for high-impact actions; activity histories/logs; "I recommended this because…" snippets. IDEO: successful assistants are intuitive, social, trusted, multimodal, nurturing — trust is emotional, not only accuracy.

**Speculation:** trust tiers ("advisor / operator / autopilot"); regulated logging & disclosure standards; agent personalities deliberately designed to signal humility/reliability.

## EssilorLuxottica Design Implications
Treat glasses as agent portals, not app canvases. Build micro-experience libraries (nav chips, translation pop-ups, caption streams, memory markers) recombined by agents. Invest in trust tooling (activity logs, permission inspectors, on-device controls). Rely on generative UI + strict semantic design systems for scale + safety.

---
---

# Source 5 — Prompting, Prompt Engineering & UX-Review Tactics

## Token Efficiency — Advanced Tactics

| Tactic | Mechanism | Impact |
|---|---|---|
| CLAUDE.md discipline | Style/conventions in one config vs re-prompting | ~15,000–30,000 fewer startup tokens/turn |
| Caveman Mode | Code + bulleted facts only, no prose | ~75% fewer output tokens/turn |
| Rust Token Killer (RTK) | Proxy compresses terminal output | 76–98% smaller terminal payloads |
| Code Review Graph | Tree-sitter index in SQLite | ~6.8x fewer tokens for code reviews |
| Grep-filtered pipelines | `npm test 2>&1 \| grep -A5 -E "FAIL\|ERROR" \| head -100` | Avoids 10k-line dumps |
| Subagent model routing | `CLAUDE_CODE_SUBAGENT_MODEL=haiku` | Cheaper subagents |
| Skills (progressive disclosure) | ~100-token metadata, full load on trigger | 60–90% fewer tokens in busy workflows |
| Compacted session handoff | `/handoff` → `.claude/session-handoff.md` → `/clear` → resume | Prevents losing key vars in lossy compaction |

## Generator–Evaluator Loop
Split generator (produces) from a skeptical evaluator (only critiques, in its own context). Run 3–10 iterations, stop when scores plateau. Equip evaluator with Playwright MCP: render headless, screenshot at 1920×1080 + 390×844, click/hover all primary interactions, check contrast.

**Four-criterion rubric (1.0–5.0, 25% each):**
1. Visual Design Quality — cohesive identity, 4px-grid alignment, hierarchy
2. Originality/Anti-Slop — no Inter/Roboto, generic rounded containers, purple gradients
3. Craft — organised CSS vars, responsive units, WCAG AA contrast, no overlaps
4. Usability & State Persistence

**Hard gate:** composite <4.2 OR any metric <3.8 → auto-trigger repair cycle. Do not mark done until thresholds met.

## Handoff: Design → Code → Repo
**In Claude Design:** package HTML/CSS/React + tokens (JSON/TS) + component list. Write `DESIGN_INTENT.md`: primary flows, UX decisions/tradeoffs, accessibility assumptions, deliberate deviations. Produce Claude Code handoff bundle.
**In Claude Code:** read DESIGN_INTENT.md; set up project (React+Vite/Next); translate to clean components with centralised theme tokens; mock data + TODO for real APIs. Don't reimagine the design unless accessibility/feasibility demands it.

## Prompt Scope Document (PSD)
Context bridge for vibe-coding. Five sections:
1. Project Vision & Objectives
2. Functional & UI/UX Requirements (flows, mockup link, design system)
3. Technical Specification (stack, libraries, constraints — prefer popular, well-documented tech)
4. Context & Knowledge Base (reference files, common mistakes to avoid e.g. "do not change anything I didn't ask for")
5. Success & Validation Criteria (tests, coverage, validation steps)

**Lifecycle:** Preparation (write PSD, plan components, init Git) → Execution (one goal at a time, review vs PSD, commit working code) → Troubleshooting (new chat + summary for context loss; paste full error for build failures; ask for "top suspects" + logs after 2–3 stuck tries).

## Pasteable Templates

### A1. Design-System Constraint Block *(for CLAUDE.md / project instructions)*
```markdown
## DESIGN SYSTEM CONSTRAINTS
### Typography
- Display: "Instrument Serif"; UI/Body: "DM Sans"; Mono: "Fira Code" (Google Fonts).
- Scale: 48/36/28/22/18; body 16/1.6; small UI 13/1.5/500.
- font-weight:700 only for hero headers. Banned: Inter, Roboto, Arial, Space Grotesk.
### Color
- --color-bg:#F5F0E8; --color-surface:#FFFDF8; --color-text:#1A1714;
- --color-primary:#B84A2F; --color-border:#E0D9D0; --color-error:#C0392B.
- Banned: blue/purple accents, pure white bg, gray-on-gray borders.
### Spacing & Grid
- Base 4px. Radius: 4px buttons/inputs, 8px containers, 0 panels. Pill banned.
- 1px solid borders only. Single light shadow: 0 1px 3px rgba(26,23,20,.08).
### Tone
- Editorial, warm, structured. Anti: SaaS modernism, glassmorphism, neon glow.
Before coding, propose 3-4 distinct visual directions.
```

### A2. Evaluator Output Contract
```xml
<evaluation_report>
  <design_quality>SCORE</design_quality>
  <originality>SCORE</originality>
  <craft>SCORE</craft>
  <usability>SCORE</usability>
  <composite_score>WEIGHTED AVERAGE</composite_score>
  <critical_defects>- element, CSS line, browser behavior</critical_defects>
  <improvement_directives>- Typography / Color / Interactivity fixes</improvement_directives>
</evaluation_report>
Hard gate: composite < 4.2 OR any metric < 3.8 → repair cycle. Do not mark done until met.
```

### A3. Session Handoff + Caveman Mode
```
SESSION HANDOFF (before /clear):
Write .claude/session-handoff.md with:
1) Milestone & objective (one sentence)
2) Changed files + git state
3) Key technical decisions (hex tokens, typefaces, state vars, API structures)
4) Active failures / failing tests
5) Next 3 steps
6) Skills/files to load next session
Output as <handoff_document> XML, then wait for /clear.

CAVEMAN MODE:
No prose, no intros. Short statements + infinitive verbs. Keep all code/paths byte-for-byte.
Auto-suspend + full warning on security or critical errors.
```

### A4. React + Babel Scaffold with Tweaks Protocol
*(Full HTML scaffold with brand tokens, Instrument Serif/DM Sans/Fira Code, Tailwind config, postMessage Tweaks protocol, and localStorage state persistence. See Source 5 full file for complete code.)*
Key rules: never `scrollIntoView()` in-sandbox; scope style-object names; register shared components to `window` (Babel block isolation).

---
*Compiled June 2026. Volatile facts (prices, limits, quotas, model versions) — verify against support.claude.com / platform.claude.com before quoting.*
