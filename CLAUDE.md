# CLAUDE.md — LioFruts (Liofilizaciones Quindío)

E-commerce website for Colombian freeze-dried fruits. Single-page vanilla HTML/CSS/JS site with WhatsApp-based ordering.

## Project Overview

- **Stack:** Vanilla HTML5, CSS3 (custom properties), JavaScript (no frameworks)
- **Fonts:** Fredoka One (headings) + Nunito (body) via Google Fonts
- **Integrations:** Web3Forms (contact form), WhatsApp (orders), Google Reviews (testimonials)
- **Market:** Colombia (Spanish, COP currency)
- **URL:** https://liofruts.co/

## Execution System — How Work Gets Done

### Phase 1: GSD Drives the Work
All planning, research, phased execution, and building flows through the GSD framework.
- Use `/gsd:do` for freeform tasks, `/gsd:plan-phase` for planning, `/gsd:execute-phase` for execution
- GSD handles: roadmapping, phase planning, code execution, atomic commits, state management
- GSD agents: gsd-planner, gsd-executor, gsd-researcher, gsd-debugger, gsd-verifier, etc.

### Phase 2: Subagents Verify & QA
Once GSD finalizes work, verification subagents review, audit, and verify the output.
- Nothing is considered done until the appropriate subagents have signed off
- **GSD builds it, subagents check it.**

## Automatic Verification Pipeline

After GSD completes any phase or task, the following verification agents run **automatically** — no manual invocation needed. Nothing is considered done until all relevant agents have signed off.

### Run Order (most critical first)

| Order | Agent | What It Checks | When It Runs |
|-------|-------|----------------|--------------|
| 1 | **security-auditor** | XSS in innerHTML/onclick patterns, form input sanitization, Web3Forms honeypot, CSP headers, exposed API keys | Every change |
| 2 | **code-reviewer** | JS code quality, CSS organization, DRY violations, dead code, inline event handler patterns, global scope pollution | Every change |
| 3 | **error-detective** | Edge cases, failure modes, null/undefined states, broken user flows, race conditions, input boundary errors | Every change |
| 4 | **performance-engineer** | Image sizes/formats (WebP), DOM particle creation, render-blocking resources, animation performance (transform/opacity only), LCP/CLS/FID | Every change |
| 5 | **accessibility-tester** | WCAG 2.1 AA compliance, keyboard navigation, focus-visible states, color contrast (4.5:1 min), ARIA labels, skip-to-content link, screen reader support | Every change |
| 6 | **test-automator** | Generate test cases for changed code, validate cart logic, form submission, carousel behavior, accordion states, localStorage persistence | Every change |
| 7 | **gsd-verifier** | Post-execution quality checks — ensures GSD phase output meets spec, no regressions introduced | Every change |
| 8 | **seo-specialist** | Meta tags, structured data (Product schema), OG images, heading hierarchy, sitemap.xml, robots.txt, hreflang, Core Web Vitals | Content or structural changes |
| 9 | **ui-designer** | Visual consistency, brand color usage, spacing tokens, typography hierarchy, depth system, mobile responsiveness | UI changes |
| 10 | **gsd-ui-checker** | Validates UI implementation matches design spec — pixel-level comparison, responsive behavior | UI changes |
| 11 | **ux-researcher** | User flow analysis, cart UX, minimum order communication, WhatsApp ordering friction, mobile touch targets (44x44px min) | UI changes |
| 12 | **architect-reviewer** | File organization, CSS architecture, JS module patterns, scalability concerns | Structural changes |
| 13 | **gsd-integration-checker** | Validates external service integrations — Web3Forms submission, WhatsApp URL generation, Google Fonts loading | Structural changes |
| 14 | **compliance-auditor** | Colombian e-commerce regulations (Ley 1581 de 2012), consumer data protection, pricing display requirements, privacy policy | Pre-launch |
| 15 | **penetration-tester** | Form injection, XSS vectors, WhatsApp URL manipulation, cart state tampering | Pre-launch |
| 16 | **debugger** | Investigates and fixes any bugs flagged by other agents in the pipeline — acts as cleanup crew | When issues are flagged |

### Pipeline Rules
- Agents 1–7 run on **every** change — no exceptions (security, quality, error detection, testing, verification)
- Agents 8–11 run based on change type (content, UI, structural)
- Agents 12–15 run on structural changes or pre-launch
- Agent 16 (debugger) runs whenever any other agent flags an issue that needs investigation
- If any agent flags a critical issue, GSD must fix it before proceeding
- The pipeline runs again after fixes to verify resolution

## Always Do First
- **Invoke the `frontend-design` skill** before writing any frontend code, every session, no exceptions.
- **Invoke `ui-ux-pro-max`** for any design decisions — consult the style database, color palettes, and UX guidelines.

## Brand Identity

### Colors (CSS Custom Properties)
```
--yellow: #FFE000        --yellow-light: #FFFBDC    --yellow-dark: #E6C800
--green: #2E7D32         --green-light: #E8F5E9     --green-mid: #4CAF50
--orange: #FF7A00        --orange-light: #FFF3E0
--dark: #1A1A1A          --gray: #6B7280            --white: #FFFFFF
```

### Typography
- Headings: `'Fredoka One', cursive` — font-weight: 400
- Body: `'Nunito', sans-serif` — font-weight: 400/600/700/800
- Tight tracking on large headings, generous line-height (1.7) on body

### Brand Assets
- Always check `Brand_assets/` before designing — it contains the logo, product images, and hero images.
- Use real assets. Do not use placeholders where real assets exist.
- Logo: `Brand_assets/liofruts-logo.jpg` (circular, yellow border)

## Frontend Rules

### Output Defaults
- Single `index.html` file, all styles inline, unless user says otherwise
- Mobile-first responsive design
- Breakpoints: 1024px, 768px, 480px

### Anti-Generic Guardrails
- **Colors:** Never use default Tailwind palette. Use the brand colors above.
- **Shadows:** Use layered, color-tinted shadows with low opacity. Never flat `shadow-md`.
- **Animations:** Only animate `transform` and `opacity`. Never `transition-all`. Use spring-style easing.
- **Interactive states:** Every clickable element needs hover, focus-visible, and active states. No exceptions.
- **Spacing:** Use intentional, consistent spacing tokens.
- **Depth:** Surfaces should have a layering system (base → elevated → floating).

### Reference Images
- If a reference image is provided: match layout, spacing, typography, and color exactly.
- Screenshot your output, compare against reference, fix mismatches, re-screenshot. Do at least 2 comparison rounds.

## Local Server
- **Always serve on localhost** — never screenshot a `file:///` URL.
- Start the dev server: `node serve.mjs` (serves the project root at `http://localhost:3000`)
- `serve.mjs` lives in the project root. Start it in the background before taking any screenshots.
- If the server is already running, do not start a second instance.

## Screenshot Workflow
- Puppeteer is installed at `C:/Users/nateh/AppData/Local/Temp/puppeteer-test/`. Chrome cache is at `C:/Users/nateh/.cache/puppeteer/`.
- **Always screenshot from localhost:** `node screenshot.mjs http://localhost:3000`
- Screenshots are saved automatically to `./temporary screenshots/screenshot-N.png` (auto-incremented, never overwritten).
- After screenshotting, read the PNG with the Read tool — Claude can see and analyze the image directly.

## Known Issues (From Audit — 2026-03-27)

These are the prioritized issues identified during the full project audit. Use GSD to plan and fix them systematically:

### Critical
1. XSS risk in cart rendering — `innerHTML` with product data (lines 1574-1585)
2. Implicit `event` object in `addToCart` — fails in strict mode (line 1504)
3. No spam protection on contact form — needs honeypot field
4. Cart state lost on page refresh — needs localStorage persistence

### Performance
5. Oversized images — favicon 745KB, infusiones 808KB, main-picture-2 734KB (need WebP + compression)
6. Continuous DOM creation from fruit particles — no cap on concurrent elements
7. No hero image preload — hurts LCP

### Accessibility
8. Properties section cards not keyboard accessible — onclick on divs without tabindex/role
9. No `:focus-visible` styles on any interactive elements
10. No skip-to-content link
11. Gray text contrast (#6B7280) borderline for small text

### SEO
12. No Product structured data for rich snippets
13. No sitemap.xml or robots.txt
14. OG image is the small logo — needs dedicated 1200x630 social sharing image

### UX
15. No back-to-top button on very long page
16. Minimum order requirement not communicated until cart
17. Hardcoded reviews labeled as "verified by Google" — misleading

## Installed Resources

### GSD Framework
- Commands: `.claude/commands/gsd/` (37 commands)
- Agents: `.claude/agents/gsd-*.md` (15 GSD agents)
- Core: `.claude/get-shit-done/` (workflows, templates, references, libs)
- Hooks: `.claude/hooks/`
- Use `/gsd:help` for command reference

### Skills (`.claude/skills/`)
| Skill | Purpose |
|-------|---------|
| `frontend-design` | Production-grade frontend interfaces, anti-AI-slop guardrails |
| `seo-audit` | SEO optimization for HTML/CSS/JS projects |
| `ui-ux-pro-max` | Design intelligence — 67 styles, 161 color palettes, 99 UX guidelines |
| `superpowers` | Spec-driven planning, TDD, subagent-driven development, code review workflows |
| `ecc-security-review` | Security checklist — XSS, CSRF, input validation, secrets management |
| `ecc-frontend-patterns` | Frontend component patterns, accessibility, performance |

### Verification Subagents (`.claude/agents/`)
| Agent | Role |
|-------|------|
| `security-auditor` | Vulnerability analysis, compliance, risk evaluation |
| `code-reviewer` | Code quality, best practices, security review |
| `error-detective` | Proactively finds edge cases, failure modes, null states, broken flows |
| `test-automator` | Generates test suites, runs tests, validates coverage |
| `debugger` | Dedicated bug investigation, root cause analysis, systematic fixing |
| `performance-engineer` | Bottleneck identification, Core Web Vitals |
| `accessibility-tester` | WCAG compliance, assistive technology support |
| `seo-specialist` | Technical SEO audits, keyword strategy, structured data |
| `ui-designer` | Visual interfaces, design systems, component aesthetics |
| `ux-researcher` | User behavior analysis, usability, persona development |
| `architect-reviewer` | System design, architectural patterns, technology choices |
| `compliance-auditor` | Regulatory compliance (GDPR, Colombian Ley 1581, consumer protection) |
| `penetration-tester` | Offensive security testing, vulnerability exploitation |
| `content-marketer` | Content strategy, SEO-optimized marketing content |
| `frontend-developer` | Frontend application building, multi-framework expertise |

## Deployment Rules
- This workspace is a **test environment**. All changes here are local only.
- **Never push to GitHub or deploy to any live URL without explicit permission from the user first.**
- Before any `git push` or deployment command, stop and ask: "¿Confirmas que quieres publicar estos cambios en el sitio en vivo?"
- The user must say yes before proceeding.
