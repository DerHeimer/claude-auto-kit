---
name: project-pipeline
description: Step-by-step build pipeline for any new project. Use at the start of every new project, when the user says "new project", "start project", "/project-pipeline", or asks to build a website, landing page, dashboard, web app, game page, 3D scene, motion video, script, bot or tool from scratch. Classifies the project as WEB, 3D, VIDEO and/or CODE, always runs the quality, test and process skills for that type, and offers the look-defining design skills as distinct style directions for the user to pick — so no single skill makes every project look the same. Orchestrates superpowers, ui-ux-pro-max, diagram-design, design-taste-frontend, impeccable, hallmark, DESIGN.md, GSAP, Emil Kowalski's motion skills, apple-design, playwright-cli, break-ui, web-design-guidelines, web-security-checklist, humanizer, img2threejs, the motion graphics skill and Remotion.
---

# Project Pipeline

You run new projects through fixed phases. The project type decides which skills are relevant (see "Skill bundles" below). Skills from bundles that don't match are not used: a website gets web skills, but no 3D model and no video.

Inside a matching bundle there are three modes:

- **always** — quality, testing and process skills. They catch problems but don't decide what the result looks like, so they run on every matching project.
- **choose** — look-defining skills (layout catalogs, themes, brand systems, signature aesthetics). Used every time, they would make every project look alike. So they are never applied by default: you offer them inside distinct style directions in Phase 1 and the user picks. Only the picked direction shapes the design.
- **if** — only when the condition in the table is true.

## Phase 0 — Classify (always)

Read the user's request and any existing files. Classify the project as one or more of:

- **WEB** — website, landing page, dashboard, web app, browser game UI, any page with a UI
- **3D** — needs a 3D object or scene in the browser (always also WEB)
- **VIDEO** — motion graphic, TikTok/Reel, animated explainer, data video
- **CODE** — script, CLI, bot, backend/API without own UI, game logic outside the browser (e.g. Roblox/Luau)

A project can have several types (e.g. WEB + CODE for a web app with a separate API). The bundle is then the union.

For anything bigger than a single static page with a complete brief: before posting the plan, run superpowers `brainstorming` (keep it short — a few targeted questions, not an interview).

Then post the plan in this shape and wait for "ok" (or changes) before building:

```
Type: WEB
Phases: 1 Style → 2 DESIGN.md → 3 Build → 4 Motion → 5 Test → 6 Polish
Always: brainstorming · writing-plans · ui-ux-pro-max · design-taste-frontend · impeccable ·
        emil-design-eng · humanizer · animate · animation-performance · playwright-cli ·
        break-ui · web-design-guidelines · web-security-checklist · hallmark audit ·
        requesting-code-review · verification-before-completion
If: test-driven-development (has app logic) · diagram-design (no — one component) · GSAP (rich motion picked)
Choose in Phase 1: see the style directions below
Not in this project's bundles: img2threejs, motion graphics skill, Remotion
Tell user: /auto-kit:pick-ui-library, /auto-kit:review-animations

Style directions — pick one (or mix):
A) <named style> · layout: <hallmark macrostructure or own> · fonts · palette · motion: none/subtle/rich · look skills: <e.g. hallmark editorial genre>
B) <clearly different style> · … · look skills: <e.g. apple-design aesthetic>
C) <clearly different again> · … · look skills: <e.g. none — own direction from ui-ux-pro-max>
Model note: <say if this project would benefit from switching to Opus / high effort>
```

Build the "Always" and "If" lines by going through the "Skill bundles" table row by row. If the build has several steps or views, `writing-plans` writes the plan and `executing-plans` runs it.

If the user said not to ask, or is clearly away, pick the direction that fits the brief best, state it at the top, and continue.

## Phase 1 — Style (WEB, VIDEO)

Propose **three style directions** in the Phase 0 plan. They must differ in all of: named style (e.g. neo-brutalism, swiss, editorial, glassmorphism, bento grid, synthwave, claymorphism, wabi-sabi, Y2K, cyberpunk), page structure, font pairing, palette and motion level. Rules for variety:

- Build the options fresh for each brief from `ui-ux-pro-max` (styles, palettes, font pairings for the product type) and, for WEB, `hallmark`'s macrostructures and genres. Don't reach for the same favourite every time.
- Look at DESIGN.md files of sibling projects (`../*/DESIGN.md`) if they exist. No option may reuse the style, font pairing or palette of one of them unless the user asks for consistency.
- At most one option may be built around a single look-defining skill's signature aesthetic (hallmark theme, apple-design look, a getdesign brand). At least one option is your own direction.
- Never default to purple gradients or centered-hero + three-card grids.

Each option names which "choose" skills it would use. After the user picks, define for the chosen direction: one font pairing, background color, one accent color, corner radius, shadow style, motion level. The look skills of the unpicked options are not applied. They may still be used as reviewers for objective problems (spacing, contrast, hierarchy), never to push their own aesthetic.

## Phase 2 — DESIGN.md (WEB)

If the project root has no DESIGN.md:
- If the picked direction is a real brand look (Linear, Stripe, Vercel, Notion, …), download it from `https://getdesign.md/<brand>/design-md` (fallback: GitHub VoltAgent/awesome-design-md).
- Otherwise write a short DESIGN.md yourself from the Phase 1 decisions (colors, type scale, spacing scale, radius, shadows, motion level, component rules, do's and don'ts).

All later UI work must follow DESIGN.md. DESIGN.md wins over any skill's default style.

## Phase 3 — Build (WEB, CODE)

WEB: Follow `design-taste-frontend` and `impeccable` for craft — hierarchy, spacing, typography quality, avoiding generic AI output — inside the picked direction and DESIGN.md, not instead of them. Use realistic copy, never lorem ipsum. Default stack: single index.html with vanilla JS for small things; Vite + React only when the project needs state across many views or the user asks for it. Charts: BKlit UI if it fits, Recharts as fallback.

Also load `emil-design-eng` for component-level polish (states, details, feel). When a library choice comes up (toasts, OTP, command menu, drag and drop, virtualization …), suggest the user runs `/auto-kit:pick-ui-library` (it only starts on explicit invocation). Run every piece of visible copy through `humanizer` before it ships.

WEB and CODE: for app logic (state, data handling, calculations, game rules — not pure layout), follow superpowers `test-driven-development`. On any bug, test failure or unexpected behavior, switch to `systematic-debugging` before proposing a fix. If the project has more than one component (frontend + API, bot + database …), draw the architecture with `diagram-design` before building and keep it in the README.

## Phase 4 — Motion (WEB)

Follow the motion level picked in Phase 1. "None" still covers basic feedback (hover, press, focus, loading, success/error). "Subtle" adds entrances and state changes. "Rich" adds scroll reveals and scroll-linked effects with GSAP + ScrollTrigger from cdnjs. Always respect `prefers-reduced-motion`. For each animation, follow `animate` (decides whether it should animate at all, curve, duration, interruption) and check it against `animation-performance`. For drag, swipe, sheets, springs and other gesture-driven UI, use `apple-design`'s motion physics — its visual aesthetic only if that direction was picked.

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

WEB: Run impeccable's audit/polish pass and `hallmark audit` (its anti-pattern check, not its themes) over the finished UI and fix what they find — as long as the fix stays inside DESIGN.md. Run `find-animation-opportunities` and apply only clear wins that match the motion level. `review-animations` can only be started by the user — tell them to run `/auto-kit:review-animations` for a strict motion review.

WEB and CODE: get a structured review with superpowers `requesting-code-review` and fix what it finds. Then report a short before/after list.

## Phase 7 — 3D asset (3D)

If a reference image exists in the project, use `/img2threejs` to rebuild it as a procedural Three.js model. Works well for hard-surface objects, poorly for faces and characters — say so if the image is organic. Embed it with orbit controls and soft lighting, then run Phase 5 on the page.

## Phase 8 — Video (VIDEO)

- Direction for every video — script, storyboard, timing, sound design → the motion graphics skill (Miftahul).
- Rendering in Remotion (default for data-driven or template videos: charts, bar races, swappable JSON data) → Remotion best practices skill.

Always: 9:16 1080x1920 unless told otherwise. Offer the Phase 1 style directions for the video's look too. Show a storyboard with second-by-second timings first and wait for OK before rendering. Only generated or royalty-free audio. Render to `./out/`. Run the script, on-screen text and caption through `humanizer` before rendering.

## Skill bundles

One row per skill. "Bundles" = project types the skill is relevant for. "Mode": **always** = run it on every matching project; **choose** = only via a style direction the user picked in Phase 1; **if** = only when the condition is true.

| Skill | Phase | Bundles | Mode |
|---|---|---|---|
| brainstorming (superpowers) | 0 | WEB, 3D, VIDEO, CODE | always, except a single static page or small script with a complete brief |
| writing-plans + executing-plans (superpowers) | 0 → 3 | WEB, 3D, VIDEO, CODE | if the build has several steps or views |
| ui-ux-pro-max | 1 | WEB, 3D, VIDEO | always (source for the style directions) |
| hallmark — themes, genres, macrostructures | 1 | WEB, 3D | choose |
| hallmark audit | 6 | WEB, 3D | always |
| DESIGN.md — getdesign brand file | 2 | WEB, 3D | choose (own DESIGN.md is always written) |
| design-taste-frontend | 3 | WEB, 3D | always, inside DESIGN.md |
| impeccable | 3, 6 | WEB, 3D | always, inside DESIGN.md |
| emil-design-eng | 3 | WEB, 3D | always |
| pick-ui-library | 3 | WEB, 3D | if a library choice comes up — tell the user (manual only) |
| test-driven-development (superpowers) | 3 | WEB, 3D, CODE | if there is app logic |
| systematic-debugging (superpowers) | any | WEB, 3D, VIDEO, CODE | if a bug occurs |
| diagram-design | 3 / docs | WEB, 3D, CODE | if more than one component, or a diagram is wanted on the page or in the README |
| humanizer | 3, 8, docs | WEB, 3D, VIDEO, CODE | always when text gets published |
| GSAP | 4 | WEB, 3D | if motion level "rich" or anything beyond CSS transitions |
| animate | 4 | WEB, 3D | always |
| apple-design — motion physics | 4 | WEB, 3D | if gesture-driven UI (drag, swipe, sheets, springs) |
| apple-design — visual aesthetic | 1, 6 | WEB, 3D | choose |
| animation-performance | 4 | WEB, 3D | always |
| playwright-cli | 5 | WEB, 3D | always |
| break-ui | 5 | WEB, 3D | always |
| web-design-guidelines | 5 | WEB, 3D | always |
| web-security-checklist | 5 | WEB, 3D; CODE with network, API keys, user data or hosting | always |
| find-animation-opportunities | 6 | WEB, 3D | always, within the picked motion level |
| review-animations | 6 | WEB, 3D | tell the user to run `/auto-kit:review-animations` (manual only) |
| improve-animations | 6 | WEB, 3D | if it's an existing project with a lot of motion code |
| requesting-code-review (superpowers) | 6 | WEB, 3D, CODE | always |
| verification-before-completion (superpowers) | end | WEB, 3D, VIDEO, CODE | always |
| img2threejs | 7 | 3D | if a reference image exists |
| motion graphics skill (Miftahul) | 8 | VIDEO | always |
| Remotion best practices | 8 | VIDEO | if the video is rendered with Remotion |

<!-- Maintained by the weekly automated task. Every new skill gets a row here (phase, bundles, mode) and is wired into that phase's text. A skill that imposes its own look (themes, brand styles, signature aesthetics) gets mode "choose"; quality, test and process skills get "always" or "if". -->

## Rules

- Checkpoint after Phase 0 always (that's where the user picks the style direction); after Phase 3 show the result (screenshot) before Motion/Test unless the user said to run straight through.
- Before saying anything is done, fixed or working: run superpowers `verification-before-completion` and check that every "always" skill and every true "if" skill was actually used.
- If a skill or tool is missing, say which one and continue with the best fallback — never stall.
- Skip superpowers' git skills (`using-git-worktrees`, `finishing-a-development-branch`) unless the project already uses git.
- superpowers, ui-ux-pro-max and diagram-design come from separate plugins installed on this machine; if one is missing, say so and continue.
- Keep narration minimal. At the end: what was built, where the files are, which style direction and look skills were used, and which skills ran.

License: CC-BY-NC-SA-4.0 — © DerHeimer, https://github.com/DerHeimer/claude-auto-kit (see NOTICE.md)
