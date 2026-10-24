# claude-auto-kit

**Save it, forget it — Claude installs it.** A template for your own self-updating Claude Code plugin: you save AI tips (Instagram reels, TikToks, posts, screenshots) into [mymind](https://mymind.com) while scrolling, and once a week Claude goes through them, turns the useful ones into skills, pushes them to *your* copy of this repo, and wires them into a `project-pipeline` skill that runs at the start of every project.

No more "saved 40 reels about Claude skills, installed none of them".

> **This repo is a template, not a plugin to install.** It only works with your own mymind space and your own copy of the repo. Fork it (or use it as a template), connect your mymind, and the weekly check fills *your* plugin with *your* finds. Installing someone else's copy just gives you their taste, changing every week.

```mermaid
flowchart LR
    A["📱 Save a reel / post / screenshot<br/>to your mymind space"] --> B["🗓️ Weekly Claude task<br/>reads new items"]
    B --> C{"What is it?"}
    C -->|"Skill (open license)"| D["Copied into your repo"]
    C -->|"Checklist / prompt"| E["Rewritten as a skill"]
    C -->|"Plugin / MCP / CLI"| F["Install command<br/>in the weekly report"]
    C -->|"Irrelevant / duplicate"| G["Skipped, noted"]
    D --> H["project-pipeline updated"]
    E --> H
    H --> I["💻 Claude Code auto-updates<br/>the plugin on your PC"]
```

## What you need

- [Claude Code](https://code.claude.com) with the `claude` CLI, and [git](https://git-scm.com) (Claude Code uses it to fetch your plugin)
- A [mymind](https://mymind.com) account. There's a free plan with a card limit (100 cards at the time of writing — check [mymind's pricing](https://mymind.com/pricing)); paid plans remove the limit.
- A Claude plan with scheduled tasks and connectors, and the **mymind connector** enabled in Claude (Settings → Connectors)
- A GitHub account, with Claude's GitHub access granted to your copy of this repo (push access)

## Set up your own

### 1. Make your copy

On GitHub, click **Use this template → Create a new repository** (or **Fork**). Pick any name, e.g. `claude-auto-kit`. A template copy can be private; if it is, git on your PC needs to be signed in to GitHub so Claude Code can fetch it.

The project is licensed [CC BY-NC-SA 4.0](LICENSE): free for your own non-commercial use, with credit. Keep [`NOTICE.md`](NOTICE.md) and put this line at the top of your copy's README:

```markdown
> Based on [claude-auto-kit](https://github.com/DerHeimer/claude-auto-kit) by DerHeimer, licensed under [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/).
```

### 2. Point it at your account

Edit two files in your copy and replace the owner with your GitHub username:

- [`.claude-plugin/marketplace.json`](.claude-plugin/marketplace.json) → `owner.name`
- [`plugins/auto-kit/.claude-plugin/plugin.json`](plugins/auto-kit/.claude-plugin/plugin.json) → `author.name` and `repository`

Don't add a `version` field to either file — without it, Claude Code updates the plugin on every new commit.

### 3. Decide what to start with

Your copy starts with the skills that are in this repo right now (see [the bottom of this page](#the-skills-already-in-this-repo)). Keep them, or delete the folders under `plugins/auto-kit/skills/` you don't want and remove their rows from `project-pipeline`. Keep `project-pipeline` itself — it's the part the weekly check builds on. If you delete everything else, the weekly check simply fills it up from your own finds.

### 4. Create a mymind space

Make a space for your finds (e.g. "AI") and share reels, posts and screenshots into it. Connect mymind to Claude if you haven't.

### 5. Schedule the weekly check

Take the prompt from [`docs/weekly-check-prompt.md`](docs/weekly-check-prompt.md), fill in the placeholders (your repo, your space, the skills and plugins you already have), and schedule it in Claude. The task needs push access to your repo. If a fresh scheduled session can't get it, run the check as a weekly reminder in a chat that has the repo attached — the prompt schedules its own next run.

### 6. Install your copy

Replace `<your-username>/<your-repo>` with your copy:

```powershell
claude plugin marketplace add <your-username>/<your-repo>
claude plugin install auto-kit@auto-kit
```

Turn on auto-update so new skills arrive by themselves — add this to `~/.claude/settings.json` (Windows: `C:\Users\<you>\.claude\settings.json`):

```json
"extraKnownMarketplaces": {
  "auto-kit": {
    "source": { "source": "github", "repo": "<your-username>/<your-repo>" },
    "autoUpdate": true
  }
}
```

Make Claude run the pipeline automatically — add this line to your `CLAUDE.md`:

```text
For every new project (website, web app, dashboard, 3D scene, motion video), start by loading the auto-kit:project-pipeline skill and follow its phases.
```

## How it works

1. **Capture.** Whenever you see something useful — a reel about a design skill, a security checklist, a GitHub repo — share it to your mymind space. mymind stores the link and writes an AI summary of the content.
2. **Weekly check.** A scheduled Claude task reads every item in that space that isn't tagged `claude-checked` yet. It works from mymind's summary, the tags and screenshots, plus web search and GitHub, to find out which tool or skill the post is about. It does not scrape Instagram or TikTok.
3. **Sort and act.**
   - Skills with an open license (MIT, Apache-2.0 …) are copied into `plugins/auto-kit/skills/` — Markdown only, no scripts.
   - Checklists and prompts from posts are rewritten as skills in Claude's own words.
   - Plugins, MCP servers and CLI tools are never added automatically, because they run code on your machine. They show up as ready-to-paste commands in the weekly report.
4. **Wire it up.** Every new skill is added to [`project-pipeline`](plugins/auto-kit/skills/project-pipeline/SKILL.md) — as a row in its "Skill bundles" table (phase, project types, the only valid skip reason) and in the text of its phase.
5. **Ship it.** The task validates the plugin, commits to `main`, tags each mymind item `claude-checked` plus one status tag and a few topic tags (see below) with a short note, and sends you a report: what was added, what was skipped and why, and what's left for you to do.
6. **Clean up.** Only items whose content is 100 % installed (`claude-installed`) are listed in the next report as ready to delete; reply "delete" and Claude removes them from mymind (they stay in mymind's trash for 30 days). "Checked" is never enough on its own. Items waiting for you (`claude-todo`, `claude-unclear`) are listed again every week until you say they're installed. Everything else stays.
7. **Use it.** Claude Code auto-updates the plugin. Start any project and `project-pipeline` classifies it and runs every skill in the matching bundle — a website gets every web skill, but no 3D or video skills.

### Tags

Every checked item gets `claude-checked`, exactly one status tag and one or more topic tags.

| Status | Meaning | What happens |
|---|---|---|
| `claude-installed` | 100 % installed: every tool, skill or checklist the item shows is verifiably on your machine — in the auto-kit repo (auto-updated), or in your list of installed plugins and skills. If even one part is missing or couldn't be identified, the item does **not** get this tag | Offered for deletion in the next run — the only status that is |
| `claude-todo` | Needs you: a plugin, MCP server, CLI tool or connector to install | Listed under "For you to do" every week until you report it installed (then it becomes `claude-installed`) |
| `claude-unclear` | The tool couldn't be identified | Listed every week until you say what was meant |
| `claude-keep` | Worth keeping, nothing to install: general knowledge, inspiration, non-Claude tools | Stays, no reminders |

Topic tags: `knowledge` (general AI know-how), `design`, `video`, `security`, `coding`, `ai-tool` (a non-Claude AI app or service), `offtopic`.

## What `project-pipeline` does

A fixed sequence of phases for web, UI, 3D, video and plain code projects. Claude classifies the project, then uses **every** skill in the bundle for that type (WEB, 3D, VIDEO, CODE) — nothing from a bundle is dropped on a whim, and nothing from an unrelated bundle is pulled in. Phases: classify → style → design system file → build → motion → test → polish, plus 3D-asset and video phases. A skill ledger in the plan and in the final report shows where each skill was used; the only allowed skip reasons are listed next to the skill. If a skill isn't installed, Claude says so and carries on.

## Safety model

- Only Markdown skills land in the repo automatically. Hooks, MCP servers, `bin/` executables and scripts never do — those come as commands you decide to run.
- Every candidate is checked for maintainer, activity, license, and for instructions that would push Claude to leak data, ignore rules or run code unasked.
- Offensive security tools are noted, never added.
- The weekly task never executes anything from a third-party repository.
- Social media pages are not scraped; the content comes from mymind's own summary and public sources.

## Limitations

- If a post doesn't name the tool and mymind's summary doesn't either, the item is tagged `claude-unclear` and the report asks you which tool was meant.
- Skills without a license that allows redistribution are not copied; you get the install command instead.
- Some skills are designed to run only when you invoke them, e.g. `/auto-kit:review-animations`.

## License

claude-auto-kit was created by **DerHeimer**. Everything written for this repo is licensed [CC BY-NC-SA 4.0](LICENSE): copy and adapt it for non-commercial use, credit the original as described in [NOTICE.md](NOTICE.md), and share changes under the same license. No commercial use.

Copied skills keep their original licenses, listed with full text in [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md). [NOTICE.md](NOTICE.md) says which part is under which license.

---

## The skills already in this repo

This copy is the author's own, filled by the weekly check from their saves. It's here as an example of what the template produces — your copy will drift in its own direction.

| Skill | What it's for | Source |
|---|---|---|
| `project-pipeline` | The orchestrator above | this repo |
| `web-security-checklist` | Pre-launch security review for AI-built web apps | this repo |
| `hallmark` | Anti-"AI slop" page structure, themes and audits | [nutlope/hallmark](https://github.com/nutlope/hallmark) |
| `humanizer` | Removes AI writing patterns from text | [blader/humanizer](https://github.com/blader/humanizer) |
| `web-design-guidelines` | UI review against Vercel's Web Interface Guidelines | [vercel-labs/agent-skills](https://github.com/vercel-labs/agent-skills) |
| `apple-design` | Apple-style fluid, physical motion for the web | [emilkowalski/skill](https://github.com/emilkowalski/skill) |
| `emil-design-eng` | UI polish and component details | [emilkowalski/skill](https://github.com/emilkowalski/skill) |
| `animate` | Building a single animation the right way | [emilkowalski/skill](https://github.com/emilkowalski/skill) |
| `animation-performance` | Keeping animations inside the frame budget | [emilkowalski/skill](https://github.com/emilkowalski/skill) |
| `find-animation-opportunities` | Where motion is missing — and where it isn't | [emilkowalski/skill](https://github.com/emilkowalski/skill) |
| `improve-animations` | Audit and plan for existing motion code | [emilkowalski/skill](https://github.com/emilkowalski/skill) |
| `review-animations` | Strict motion review (run it yourself) | [emilkowalski/skill](https://github.com/emilkowalski/skill) |
| `break-ui` | Stress-test UI with worst-case data | [emilkowalski/skill](https://github.com/emilkowalski/skill) |
| `pick-ui-library` | Picks a library for a frontend task (run it yourself) | [emilkowalski/skill](https://github.com/emilkowalski/skill) |

Alongside these, the author's `project-pipeline` calls a few separately installed plugins and skills: the plugins `superpowers`, `ui-ux-pro-max` and `diagram-design`, and the skills `design-taste-frontend`, `impeccable`, `playwright-cli`, `img2threejs`, `remotion-best-practices` and a motion graphics skill. Swap them for whatever you use.
