---
name: oss-contributor
description: Analyze any open-source GitHub repository and prepare a contribution: survey architecture, pick a suitable issue, locate the root cause, and produce a fix plan with tests. Use when the user wants to contribute to an OSS project, pick a first issue, understand a repository's structure, or draft a pull request.
---

# OSS Contributor Skill

## Overview

This skill turns "I want to contribute to repo X" into a concrete, verifiable
contribution plan: repo survey → issue selection → code localization → fix
design → PR checklist. Use it **before writing any code** against an unfamiliar
repository, so a contribution lands with a reproducer, an anchored root cause,
and a regression test — not a guess.

## When to Use This Skill

- User names a GitHub repository and asks how to contribute, what to fix, or what to build first
- User wants a "good first issue" or an issue matched to their skill level
- User asks to analyze a repository's architecture before making changes
- User wants a fix plan for a specific issue (root cause + test strategy + PR outline)
- User wants to review an existing local checkout and turn it into a PR-ready change

## When NOT to Use This Skill

- Pure Q&A about a project's README facts with no contribution intent
- Writing code inside a codebase the user already knows well (no survey needed)
- General web research unrelated to a specific repository contribution

## Core Principle

**Never propose a change without three anchors:** a reproducer (or an issue
that ships one), the exact `file:line` of the root cause, and a regression test
plan. Unanchored suggestions are noise — they waste both the contributor's and
the maintainer's review cycle.

## Workflow

### Phase 1: Repo Survey (read-only, one pass)

1. Read README (and its primary translation if the user's language differs),
   CONTRIBUTING.md, AGENTS.md / CLAUDE.md, and the top of CHANGELOG.md.
2. Record the contribution contract: language, build/test/lint commands, CI
   checks, commit-message convention, AI-assistance disclosure rules.
3. Map the top-level layout (backend / frontend / skills / docs) and identify
   the module that will own the change.

### Phase 2: Issue Selection

1. List open issues; prefer: labeled bug/help-wanted, recently active,
   reproducible, small blast radius.
2. Score candidates on four axes:
   - (a) reproducer exists in the issue body,
   - (b) root cause locatable in the codebase in under ~30 minutes,
   - (c) a test file/area already exists for the module,
   - (d) no open PR or "I'll take this" claim on the issue.
3. Recommend **one** issue. State competition risk (e.g. the reporter offered
   to fix it) and the claiming etiquette: comment "I'd like to work on this"
   before starting.

### Phase 3: Fix Plan

1. Locate the root cause: cite `file:line`, quote the failing code.
2. Write the minimal patch — prefer defensive guards symmetric to sibling code
   in the same file.
3. Write the regression test, mirroring the existing test style in the same
   test file (parametrize where the failure shapes are enumerable).
4. Run: the module's test file → formatter (ruff / prettier) → the relevant
   full suite.
5. Produce the PR: feature-branch name, conventional-commit message, and the
   AI-assistance disclosure section filled in truthfully.

## Output Format

Deliver as a structured markdown plan:

- **Recommended issue** — `#num`, why it fits, competition risk
- **Root cause** — `file:line` + quoted failing snippet
- **Patch** — code block of the minimal change
- **Test** — code block + the exact command that runs it
- **PR checklist** — branch name, commit message, format / test / disclosure

## References

- `skills/public/deep-research/SKILL.md` — multi-angle research methodology for the survey phase
- `skills/public/skill-reviewer/SKILL.md` — self-review a skill before publishing
- `backend/AGENTS.md` and `frontend/AGENTS.md` — module depth for DeerFlow contributions
