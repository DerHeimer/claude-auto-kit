---
name: project-pipeline
description: Step-by-step build pipeline for any new project. Use at the start of every new project, when the user says "new project", "start project", "/project-pipeline", or asks to build a website, landing page, dashboard, web app, game page, 3D scene, motion video, script, bot or tool from scratch. Classifies the project as WEB, 3D, VIDEO and/or CODE and then uses every skill in the matching bundle — superpowers, ui-ux-pro-max, diagram-design, design-taste-frontend, impeccable, hallmark, DESIGN.md, GSAP, Emil Kowalski's motion skills, apple-design, playwright-cli, break-ui, web-design-guidelines, web-security-checklist, humanizer, img2threejs, the motion graphics skill and Remotion — in the right order, and none from unrelated bundles.
---

# Project Pipeline

You run new projects through fixed phases. The project type decides which **skill bundle** applies (see "Skill bundles" below). Inside a matching bundle you use **every** skill. A bundle skill may only be left out for the exact reason written in its "Only skip if" column — "not needed", "simple project" or "to save time" are not valid reasons. Skills from bundles that don't match the project are not used at all: a website gets every web skill, but no 3D model and no video.

## Phase 0 — Classify (always)

Read the user's request and any existing files. Classify the project as one or more of:

- **WEB** — website, landing page, dashboard, web app, browser game UI, any page with a UI
- **3D** — needs a 3D object or scene in the browser (always also WEB)
- **VIDEO** — motion graphic, TikTok/Reel, animated explainer, data video
- **CODE** — script, CLI, bot, backend/API without own UI, game logic outside the browser (e.g. Roblox/Luau)

A project can have several types (e.g. WEB + CODE for a web app with a separate API). The bundle is then the union.

For anything bigger than a single static page with a complete brief: before posting the plan, run superpowers `brainstorming` (keep it short — a few targeted questions, not an interview).

Then post the plan in this exact shape and wait for "ok" (or changes) before building:

```
Type: WEB (+3D)
Phases: 1 Style → 2 DESIGN.md → 3 Build → 4 Motion → 5 Test → 6 Polish → 7 3D-asset
Skill ledger (WEB + 3D bundle):
  0 brainstorming · writing-plans · executing-plans
  1 ui-ux-pro-max · hallmark
  2 DESIGN.md
  3 design-taste-frontend · impeccable · emil-design-eng · humanizer · test-driven-development
  4 GSAP · animate · apple-design · animation-performance
  5 playwright-cli · break-ui · web-design-guidelines · web-security-checklist
  6 impeccable audit · hallmark audit · apple-design review · find-animation-opportunities · requesting-code-review
  7 img2threejs
  always: systematic-debugging (on bugs) · verification-before-completion
  skipped by rule: improve-animations (new project, not an existing one)
  tell user: /auto-kit:pick-ui-library, /auto-kit:review-animations
Not in this project's bundles: motion graphics skill, Remotion (not a video)
Style proposal: <1 style + 1 alternative, one line each>
Model note: <say if this project would benefit from switching to Opus / high effort>
```

Build the ledger by going through the "Skill bundles" table row by row. Every row whose bundle matches must appear either in a phase line or under "skipped by rule" with its listed reason. If the build has several steps or views, `writing-plans` writes the plan and `executing-plans` runs it.

If the user said not to ask, or is clearly away, pick sensible defaults, state them at the top, and continue.

## Phase 1 — Style (WEB, VIDEO)

Pick a concrete named design style instead of "modern" (e.g. neo-brutalism, swiss, editorial, glassmorphism, bento grid, synthwave, claymorphism, wabi-sabi, Y2K, cyberpunk). Define: one font pairing, background color, one accent color, corner radius, shadow style. Back these choices with `ui-ux-pro-max` (search its styles, palettes and font pairings for the product type) instead of picking from memory. Never default to purple gradients or centered-hero + three-card grids.

For page layouts (WEB), load `hallmark` and use its macrostructure catalog to pick a page structure that fits the brief (not the usual hero → 3 features → CTA rhythm). Keep the Phase 1 style decision; if hallmark's theme picker disagrees, mention it as the alternative.

## Phase 2 — DESIGN.md (WEB)

If the project root has no DESIGN.md:
- If a real brand look fits (Linear, Stripe, Vercel, Notion, …), download it from `https://getdesign.md/<brand>/design-md` (fallback: GitHub VoltAgent/awesome-design-md).
- Otherwise write a short DESIGN.md yourself from the Phase 1 decisions (colors, type scale, spacing scale, radius, shadows, component rules, do's and don'ts).

All later UI work must follow DESIGN.md.

## Phase 3 — Build (WEB, CODE)

WEB: Load and follow the `design-taste-frontend` skill and the `impeccable` skill while building. Use realistic copy, never lorem ipsum. Default stack: single index.html with vanilla JS for small things; Vite + React only when the project needs state across many views or the user asks for it. Charts: BKlit UI if it fits, Recharts as fallback.

Also load `emil-design-eng` for component-level polish (states, details, feel). When a library choice comes up (toasts, OTP, command menu, drag and drop, virtualization …), suggest the user runs `/auto-kit:pick-ui-library` (it only starts on explicit invocation). Run every piece of visible copy through `humanizer` before it ships.

WEB and CODE: for app logic (state, data handling, calculations, game rules — not pure layout), follow superpowers `test-driven-development`. On any bug, test failure or unexpected behavior, switch to `systematic-debugging` before proposing a fix. If the project has more than one component (frontend + API, bot + database …), draw the architecture with `diagram-design` before building and keep it in the README.

## Phase 4 — Motion (WEB)

Always runs for WEB. Pages and landing pages: entrance of hero, scroll reveals, state changes. Tools, dashboards and forms: keep it to feedback and state changes (hover, press, loading, success/error, panel open/close) — no decorative motion unless the user wants it. Use GSAP + ScrollTrigger from cdnjs for anything beyond simple CSS transitions. Always respect `prefers-reduced-motion`. For each animation, follow `animate` (decides whether it should animate at all, curve, duration, interruption). Use `apple-design` for the feel of every interactive component and for drag, swipe, sheets, springs and other gesture-driven UI. Check all motion against `animation-performance`.

## Phase 5 — Test (WEB, 3D)

Use `playwright-cli`:
1. Open the page (local file or dev server).
2. Full-page screenshots at 375, 768 and 1440 px into `./screenshots`.
3. Review them yourself: overflow, overlap, tiny text, tap targets under 44px, broken line breaks, console errors.
4. Fix everything, re-screenshot, confirm.
5. Run `break-ui` on every component that shows data or text (long names, empty states, huge numbers, non-Latin text) and fix what breaks.
6. Run `web-design-guidelines` over the UI files and fix the findings.
7. Run `web-security-checklist` and fix every FAIL. A static page only needs its sections 1, 6 and 8 — that is the checklist's own rule, not a reason to skip it.

## Phase 6 — Polish (WEB, CODE)

WEB: Run impeccable's audit/polish pass, `hallmark audit` and an `apple-design` review over the finished UI and fix what they find. Run `find-animation-opportunities` and apply only clear wins. `review-animations` can only be started by the user — tell them to run `/auto-kit:review-animations` for a strict motion review.

WEB and CODE: get a structured review with superpowers `requesting-code-review` and fix what it finds. Then report a short before/after list.

## Phase 7 — 3D asset (3D)

If a reference image exists in the project, use `/img2threejs` to rebuild it as a procedural Three.js model. Works well for hard-surface objects, poorly for faces and characters — say so if the image is organic. Embed it with orbit controls and soft lighting, then run Phase 5 on the page.

## Phase 8 — Video (VIDEO)

- Direction for every video — script, storyboard, timing, sound design → the motion graphics skill (Miftahul).
- Rendering in Remotion (default for data-driven or template videos: charts, bar races, swappable JSON data) → Remotion best practices skill.

Always: 9:16 1080x1920 unless told otherwise. Show a storyboard with second-by-second timings first and wait for OK before rendering. Only generated or royalty-free audio. Render to `./out/`. Run the script, on-screen text and caption through `humanizer` before rendering.

## Skill bundles

One row per skill. "Bundles" says for which project types the skill is mandatory. "Only skip if" is the complete list of valid reasons to leave it out — if the condition isn't true, use the skill.

| Skill | Phase | Bundles | Only skip if |
|---|---|---|---|
| brainstorming (superpowers) | 0 | WEB, 3D, VIDEO, CODE | Single static page or single small script with a complete brief |
| writing-plans + executing-plans (superpowers) | 0 → 3 | WEB, 3D, VIDEO, CODE | The build is one step / one view |
| ui-ux-pro-max | 1 | WEB, 3D, VIDEO | — |
| hallmark | 1, 6 | WEB, 3D | — |
| DESIGN.md / getdesign | 2 | WEB, 3D | — |
| design-taste-frontend | 3 | WEB, 3D | — |
| impeccable | 3, 6 | WEB, 3D | — |
| emil-design-eng | 3 | WEB, 3D | — |
| pick-ui-library | 3 | WEB, 3D | Manual only: tell the user when a library choice comes up |
| test-driven-development (superpowers) | 3 | WEB, 3D, CODE | No app logic at all (pure layout/content) |
| systematic-debugging (superpowers) | any | WEB, 3D, VIDEO, CODE | No bug occurred |
| diagram-design | 3 / docs | WEB, 3D, CODE | Only one component and no diagram on the page or in the README |
| humanizer | 3, 8, docs | WEB, 3D, VIDEO, CODE | No text gets published (no copy, README, script or caption) |
| GSAP | 4 | WEB, 3D | Only plain CSS transitions are needed |
| animate | 4 | WEB, 3D | — |
| apple-design | 4, 6 | WEB, 3D | — |
| animation-performance | 4 | WEB, 3D | — |
| playwright-cli | 5 | WEB, 3D | — |
| break-ui | 5 | WEB, 3D | — |
| web-design-guidelines | 5 | WEB, 3D | — |
| web-security-checklist | 5 | WEB, 3D; CODE with network, API keys, user data or hosting | — |
| find-animation-opportunities | 6 | WEB, 3D | — |
| review-animations | 6 | WEB, 3D | Manual only: tell the user to run `/auto-kit:review-animations` |
| improve-animations | 6 | WEB, 3D | New project (it is for existing projects with a lot of motion code) |
| requesting-code-review (superpowers) | 6 | WEB, 3D, CODE | — |
| verification-before-completion (superpowers) | end | WEB, 3D, VIDEO, CODE | — |
| img2threejs | 7 | 3D | No reference image exists (then build the model by hand in Three.js and say so) |
| motion graphics skill (Miftahul) | 8 | VIDEO | — |
| Remotion best practices | 8 | VIDEO | The video is not rendered with Remotion |

<!-- Maintained by the weekly automated task. Every new skill gets a row here (with its phase, bundles and the only valid skip reason) and is wired into that phase's text. -->

## Rules

- Checkpoint after Phase 0 always; after Phase 3 show the result (screenshot) before Motion/Test unless the user said to run straight through.
- Before saying anything is done, fixed or working: run superpowers `verification-before-completion` and go through the skill ledger. Every bundle skill must be marked used (with the phase) or skipped by its listed rule. If one is neither, go back and use it.
- If a skill or tool is missing, say which one and continue with the best fallback — never stall.
- Skip superpowers' git skills (`using-git-worktrees`, `finishing-a-development-branch`) unless the project already uses git.
- superpowers, ui-ux-pro-max and diagram-design come from separate plugins installed on this machine; if one is missing, say so and continue.
- Keep narration minimal. At the end: what was built, where the files are, and the final skill ledger (used / skipped by rule / told the user).

License: CC-BY-NC-SA-4.0 — © DerHeimer, https://github.com/DerHeimer/claude-auto-kit (see NOTICE.md)
