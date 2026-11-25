# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

An AI product-management portfolio, published publicly at https://github.com/elanlux1/ai-pm-portfolio. It holds Markdown documents rather than application code, so there is no build, lint or test tooling. The work is writing PRDs, prompts, eval definitions and workflow specs.

## Layout

- `AI-PM-portfolio/Notes/`: weekly learning notes (`week01.md`, …). Each concept is written up with a "PM angle" or "PM decisions" note underneath it.
- `prd-saas/B2B`: the master PRD template for AI products. The file has no extension but is Markdown. New project PRDs should follow its structure: exec summary → market → strategy → personas/use cases → messaging → competitive → scope matrix (V1/V2/non-goals) → **AI-specific requirements** (data supply chain and tenant isolation, structured-output contract, quality/latency/cost thresholds, agent autonomy and tool-permissions matrix, golden-dataset eval gate, fallback UX) → GTM rollout (shadow mode → design-partner beta → GA) → open questions and sign-off.
- `cafe-sol/`, `siteline/`, `sre-agent/`: one folder per portfolio project. Each has the same four subfolders:
  - `docs/`: PRDs and specs built from the template above
  - `prompts/`: system prompts and prompt templates
  - `evals/`: golden datasets, metrics and pass thresholds (the notes describe the PM as the person who defines "good" and sets the pass mark)
  - `workflows/`: agent and automation workflow definitions

  The `.gitkeep` files exist only so the empty folders are tracked. Delete one once its folder has real content.

## Project-specific context

- **SiteLine**: an agent where every ticket action needs human approval. Design its tool permissions to match the PRD's autonomy matrix (read-only actions run autonomously, internal writes are suggest-only, external or irreversible actions are escalated for human approval).
- The PRD template's example personas are support/CX leads, multi-location SMB operators and on-call SREs. These appear to line up with SiteLine, cafe-sol and sre-agent, but confirm with the user before treating that as settled.

## Repo hygiene

- There is a local `.env` at the root with no `.gitignore` covering it, and the repo is public. Never stage it. Use `git add <paths>`, not `git add -A` or `git add .`.
- Commits go straight to `main` and are pushed to `origin`.
