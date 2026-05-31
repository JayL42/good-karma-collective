---
title: CLAUDE.md — Good Karma Collective (project-local context gate)
created: 2026-04-24
author: Jay LaBelle
scope:
  project: good-karma-collective
  context_domain: personal
status: active
---

# CLAUDE.md — Good Karma Collective

Project-local instructions. When working *inside* this project folder, follow these rules. They override the workspace-level `CLAUDE.md` on context scope.

## Context Domain: personal

This is a personal project, not a Returnalyze project. Load:

- ✅ Workspace **filing discipline** from `~/Development/CLAUDE.md` — the "File Answers Back" pattern, frontmatter scope fields, `log.md` action vocabulary, HIL checkpoint rule, anti-drift discipline
- ✅ Workspace **skills that are domain-agnostic** — `skill-creator`, `docx`, `pptx`, `xlsx`, `pdf`, `rz-presentations` (template is Returnalyze-branded — skip for GKC), generic writing/design tooling
- ✅ This project's local `log.md`, `README.md`, `source-artifacts/`, `outputs/`

Do **not** load:

- ❌ `.shared-context/returnalyze/` — none of the Returnalyze shared context applies here
- ❌ TPx plans in `skills/product-management/context/plans/` — different business entirely
- ❌ `.work-in-progress.md` — that's the Returnalyze master plan
- ❌ `corrections.md` — Returnalyze-scoped corrections ledger
- ❌ Returnalyze-specific skills: `design` (Returnalyze UX context), `voc`, `cost-optimization`, `decision-scope-updates`, `qa-triage-concurrent-pass`
- ❌ Atlassian/Confluence/Jira MCP tools and any TPx registry lookups — irrelevant scope
- ❌ Returnalyze-specific skills loaded by default — if one gets invoked by accident, surface it and skip

If a task genuinely needs a Returnalyze-adjacent capability (e.g., the general-purpose `product-management` framework minus the Returnalyze specifics), lift the framework into this project's local docs rather than importing the full skill context.

## Filing Discipline — scoped to this project

Apply the workspace "File Answers Back" rules, but with these substitutions:

| Workspace concept         | GKC project equivalent                                    |
|---------------------------|-----------------------------------------------------------|
| `~/Development/log.md`    | `projects/good-karma-collective/log.md` (project-local)   |
| `.shared-context/returnalyze/index.md` | (not applicable — use README + source-artifacts/) |
| `.work-in-progress.md`    | (no equivalent yet — add if project complexity warrants)  |
| `corrections.md`          | (no equivalent yet — add if process gaps emerge)          |
| `outputs/analyses/`       | `projects/good-karma-collective/outputs/analyses/`        |
| `outputs/specs/`          | `projects/good-karma-collective/outputs/specs/`           |
| `outputs/design/`         | `projects/good-karma-collective/outputs/design/`          |

**Scope frontmatter** on any artifact filed into this project:

```yaml
scope:
  project: good-karma-collective
  context_domain: personal
```

**Workspace-level `log.md`**: still append a one-line entry for *material* GKC milestones (project creation, site launch, major scope shifts) so the workspace log remains the full index of activity. Routine intra-project updates live in the project-local `log.md`.

## Anticipated Tooling

- **GitHub** — no MCP connector available in Anthropic's registry (verified 2026-05-31), and none needed. We use `git` + `gh` CLI from Jay's terminal. Repo initialized locally 2026-05-31 with `main` as default branch, `.gitignore` in place. Remote creation + first push: pending Jay's terminal (see project log.md for the exact commands). Will be a **private** repo at `github.com/jayl42/good-karma-collective`; Netlify pulls from there.
- **Netlify** — no MCP connector anticipated; deploys via Git push + Netlify's build hooks.
- **MassageBook** — no connector needed. Integration approach **decided 2026-05-31**: hybrid — branded link-out "Book Now" buttons everywhere, full iframe embed on the Book Now page only. Full spec at `outputs/specs/2026-05-31-booking-integration.md` (widget URLs, snippets, mixed-content / mobile / theming gotchas). (Original handoff brief said Vagaro — corrected after Bethany confirmed MassageBook + Square reader.) MassageBook's *own* site builder doesn't allow custom code, which is exactly why we host the marketing site elsewhere (Netlify) and only consume MassageBook for booking + gift certs.

## Handoff Model

Bethany drives design/copy in a **separate Claude chat** seeded from `source-artifacts/brief.md`. That chat is a parallel track — Claude-in-Jay's-workspace (this context) and Claude-in-Bethany's-chat don't share memory.

Sync points between the two tracks:
- When Bethany finalizes brand/visual direction, capture a summary in `outputs/design/` so the code phase has it
- When Bethany finalizes copy blocks, save them to `outputs/design/copy-final.md` (or similar)
- Open HIL items (pricing, phone, Hot Stone cert) resolve through Bethany and get reflected here

## What Goes in This Project vs. Stays Out

**In scope**:
- Site code and infrastructure (hosting, domain, deploy)
- Technical specs (stack decisions, Vagaro embed approach, Netlify config)
- Design artifacts that Jay needs to implement (finalized color tokens, type scale, layout decisions)
- Meta about the project (status, roles, decisions, tracking)

**Out of scope**:
- Bethany's creative exploration — lives in her chat, not this workspace
- Vagaro account setup, licensing paperwork, bookkeeping — not a code/doc project
- Marketing/SEO strategy — separate concern from the site build

## Personal-Jumpstart (future)

A personal-jumpstart skill is anticipated but not yet built. When built, it should discover this project via `context_domain: personal` frontmatter and read this file + the local `log.md` + `README.md`. Keep those three files high-signal so the eventual skill has good inputs.
