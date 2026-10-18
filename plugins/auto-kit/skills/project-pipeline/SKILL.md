---
name: project-pipeline
description: Step-by-step build pipeline for any new web, UI, 3D or video project. Use at the start of every new project, when the user says "new project", "start project", "/project-pipeline", or asks to build a website, landing page, dashboard, web app, game page, 3D scene or motion video from scratch. Orchestrates superpowers (brainstorming, planning, TDD, debugging, verification), ui-ux-pro-max, diagram-design, design-taste-frontend, impeccable, hallmark, DESIGN.md, GSAP, Emil Kowalski's motion skills, playwright-cli, break-ui, web-design-guidelines, web-security-checklist, humanizer, img2threejs, the motion graphics skill and Remotion in the right order.
---

# Project Pipeline

You run new projects through fixed phases. Not every phase applies to every project — decide per project, say which phases you will run and which you skip (one line each, with the reason), then go.

## Phase 0 — Classify (always)

Read the user's request and any existing files. Classify the project as one or more of:

- **WEB** — website, landing page, dashboard, web app, browser game UI
- **3D** — needs a 3D object or scene in the browser
- **VIDEO** — motion graphic, TikTok/Reel, animated explainer, data video

Then post a short plan in this exact shape and wait for "ok" (or changes) before building:

```
Type: WEB (+3D)
Phases: 1 Style → 2 DESIGN.md → 3 Build → 4 Motion → 5 Test → 6 Polish
Skipped: 7 3D-asset (not needed), 8 Video (not a video)
Style proposal: <1 style + 1 alternative, one line each>
Model note: <say if this project would benefit from switching to Opus / high effort>
```

If the user said not to ask, or is clearly away, pick sensible defaults, state them at the top, and continue.

For anything bigger than a single static page: before posting the plan, run superpowers `brainstorming` (keep it short — a few targeted questions, not an interview). If the build has several steps or views, follow up with `writing-plans` and execute the plan with `executing-plans`.

## Phase 1 — Style (WEB, VIDEO)

Pick a concrete named design style instead of "modern" (e.g. neo-brutalism, swiss, editorial, glassmorphism, bento grid, synthwave, claymorphism, wabi-sabi, Y2K, cyberpunk). Define: one font pairing, background color, one accent color, corner radius, shadow style. Back these choices with `ui-ux-pro-max` (search its styles, palettes and font pairings for the product type) instead of picking from memory. Never default to purple gradients or centered-hero + three-card grids.

For page layouts, load `hallmark` and use its macrostructure catalog to pick a page structure that fits the brief (not the usual hero → 3 features → CTA rhythm). Keep the Phase 1 style decision; if hallmark's theme picker disagrees, mention it as the alternative.

## Phase 2 — DESIGN.md (WEB)

If the project root has no DESIGN.md:
- If a real brand look fits (Linear, Stripe, Vercel, Notion, …), download it from `https://getdesign.md/<brand>/design-md` (fallback: GitHub VoltAgent/awesome-design-md).
- Otherwise write a short DESIGN.md yourself from the Phase 1 decisions (colors, type scale, spacing scale, radius, shadows, component rules, do's and don'ts).

All later UI work must follow DESIGN.md.

## Phase 3 — Build (WEB)

Load and follow the `design-taste-frontend` skill and the `impeccable` skill while building. Use realistic copy, never lorem ipsum. Default stack: single index.html with vanilla JS for small things; Vite + React only when the project needs state across many views or the user asks for it. Charts: BKlit UI if it fits, Recharts as fallback.

Also load `emil-design-eng` for component-level polish (states, details, feel). When a library choice comes up (toasts, OTP, command menu, drag and drop, virtualization …), suggest the user runs `/auto-kit:pick-ui-library` (it only starts on explicit invocation). Run every piece of visible copy through `humanizer` before it ships.

For app logic (state, data handling, calculations, game rules — not pure layout), follow superpowers `test-driven-development`. On any bug, test failure or unexpected behavior, switch to `systematic-debugging` before proposing a fix.

## Phase 4 — Motion (WEB)

Add animation only where it helps: entrance of hero, scroll reveals, state changes. Use GSAP + ScrollTrigger from cdnjs for anything beyond simple CSS transitions. Always respect `prefers-reduced-motion`. For each animation, follow `animate` (decides whether it should animate at all, curve, duration, interruption). For drag, swipe, sheets, springs or other gesture-driven UI, load `apple-design`. With more than a few animations or anything scroll-linked, check against `animation-performance`. Skip this phase for tools, dashboards and forms unless the user wants animation.

## Phase 5 — Test (WEB, 3D)

Use `playwright-cli`:
1. Open the page (local file or dev server).
2. Full-page screenshots at 375, 768 and 1440 px into `./screenshots`.
3. Review them yourself: overflow, overlap, tiny text, tap targets under 44px, broken line breaks, console errors.
4. Fix everything, re-screenshot, confirm.
5. Run `break-ui` on every component that shows data (long names, empty states, huge numbers, non-Latin text) and fix what breaks.
6. Run `web-design-guidelines` over the UI files and fix the findings.
7. If the project has a backend, database, login, forms, API keys, paid API calls or gets hosted publicly: run `web-security-checklist` and fix every FAIL.

## Phase 6 — Polish (WEB)

Run impeccable's audit/polish pass and `hallmark audit` over the finished UI and fix what they find. If Phase 4 ran, finish with `find-animation-opportunities` and apply only clear wins. `review-animations` can only be started by the user — tell them to run `/auto-kit:review-animations` for a strict motion review. Then report a short before/after list.

## Phase 7 — 3D asset (3D only)

If a reference image exists in the project, use `/img2threejs` to rebuild it as a procedural Three.js model. Works well for hard-surface objects, poorly for faces and characters — say so if the image is organic. Embed it with orbit controls and soft lighting, then run Phase 5 on the page.

## Phase 8 — Video (VIDEO only)

- Short design-led motion graphics, kinetic text, TikTok/Reel clips with SFX → the motion graphics skill (Miftahul).
- Data-driven or template videos (charts, bar races, swappable JSON data) → Remotion best practices skill.

Always: 9:16 1080x1920 unless told otherwise. Show a storyboard with second-by-second timings first and wait for OK before rendering. Only generated or royalty-free audio. Render to `./out/`. Run the script, on-screen text and caption through `humanizer` before rendering.

## Rules

- Checkpoint after Phase 0 always; after Phase 3 show the result (screenshot) before Motion/Test unless the user said to run straight through.
- If a skill or tool is missing, say which one and continue with the best fallback — never stall.
- Before saying anything is done, fixed or working, run superpowers `verification-before-completion`.
- Skip superpowers' git skills (`using-git-worktrees`, `finishing-a-development-branch`) unless the project already uses git.
- superpowers, ui-ux-pro-max and diagram-design come from separate plugins installed on this machine; if one is missing, say so and continue.
- Keep narration minimal. At the end: what was built, where the files are, what was skipped.

## Extra skills (check every project)

Skills below don't own a phase. In Phase 0, go through each row and list it under "Phases" (with the phase it plugs into) if the "when" condition matches this project, otherwise under "Skipped" with a short reason. Use every matching one — not all of them blindly.

| Skill | Plugs into | When to use |
|---|---|---|
| improve-animations | Phase 6 | Existing project (not greenfield) with a lot of motion code — audit it and plan improvements before touching it |
| web-security-checklist | Phase 5 | Any time the project stores data, has accounts, calls paid APIs or is put online — even if Phase 5 is otherwise skipped |
| humanizer | Any | Any text that gets published: site copy, README, video scripts, captions, posts |
| diagram-design | Phase 3 / docs | The project needs an architecture, flow, timeline, ER, sequence or other technical diagram (on the page, in a README or for planning) |
| requesting-code-review | Phase 6 | Larger codebases or anything with a backend — get a structured review before calling it done |

<!-- Maintained by the weekly automated task. New skills that fit an existing phase are wired into that phase's text; everything else gets a row here. -->
