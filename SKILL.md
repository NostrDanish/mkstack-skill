---
name: mkstack
description: Create Nostr client websites from the MKStack template (React + Vite + Tailwind + shadcn/ui) and build them with OpenCode. Use when starting a new Nostr-powered web app or MKStack project.
---

# MKStack

MKStack is a template for building Nostr clients with compatible coding agents (OpenCode, Shakespeare, Cursor). This skill is the **scaffold + OpenCode** workflow only. OpenCode CLI details live in the `opencode` skill — read both before running.

## Host portability

The original spawn/exec blocks below are **OpenClaw-shaped**. On other hosts, keep the same *steps* and drop the YAML:

| OpenClaw | Cursor / generic agent |
|---|---|
| `sessions_spawn` + `runTimeoutSeconds: 660` | Spawn a subagent / Task with a 10-minute budget |
| `exec` + `pty: true` + `yieldMs` / `timeout` | Run OpenCode in an interactive terminal; do not background it |
| `workdir:` | `cd` or `opencode run --dir <path>` |

Do **not** hardcode a model id. Use the model the user named, or the one selected in the `opencode` skill (`opencode models`).

## Workflow: spawn a subagent

Keep the long OpenCode run out of the main chat.

**Parent agent:**
1. Project path: `<workspace>/projects/<project-name>` (lowercase, hyphens).
2. Resolve the full paths of the `mkstack` and `opencode` SKILL.md files.
3. Spawn a subagent whose first instruction is: read both skills, then create the project. Do not improvise or skip OpenCode.

```
sessions_spawn:
  task: "CRITICAL: You MUST read the mkstack skill (<skills>/mkstack/SKILL.md) first, then read the opencode skill (<skills>/opencode/SKILL.md). Do NOT proceed until you have read both skills. After reading them, create a new MKStack project for [describe the project]. Follow the mkstack workflow exactly - do NOT improvise or skip the OpenCode step. Project path: <workspace>/projects/<project-name>"
  label: "mkstack-<project-name>"
  runTimeoutSeconds: 660
```

## For the subagent

### Step 1: Scaffold

Prefer the official generator when it is available (pins a release and keeps attribution):

```bash
mkdir -p <workspace>/projects
cd <workspace>/projects
npm create mkstack@latest <project-name>
cd <project-name>
git rev-parse HEAD   # record the template SHA in the first commit message if a git history exists
```

If `npm create mkstack` is missing or the user asked to clone:

```bash
mkdir -p <workspace>/projects
cd <workspace>/projects
git clone https://gitlab.com/soapbox-pub/mkstack.git <project-name>
cd <project-name>
TEMPLATE_SHA=$(git rev-parse HEAD)
# Keep upstream README as attribution — do not delete it.
git checkout --orphan tmp-init
git add .
git commit -m "Project created with MKStack ${TEMPLATE_SHA}: https://gitlab.com/soapbox-pub/mkstack.git"
```

Always create projects under `<workspace>/projects/`, never `$HOME`.

### Step 2: Run OpenCode

You MUST have read the `opencode` skill. Typical command (model comes from the user / `opencode models`, not from this file):

```bash
cd <workspace>/projects/<project-name> && opencode run --auto --dir . --model <provider>/<model> "[detailed project description]"
```

OpenClaw exec extras (ignore on Cursor): `pty: true`, `workdir: <project>`, `yieldMs: 600000`, `timeout: 600`.

Without a PTY you will see no streaming output and the run looks hung.

### Step 3: Report

Say what was created, the project path, and the template SHA if you cloned.

## What MKStack includes

Confirm against the template README after scaffolding (the list drifts):

- Nostr integration (provider, hooks, utilities)
- React + Vite + TypeScript
- Tailwind CSS + shadcn/ui
- Pre-built Nostr modules (comments, DMs, infinite scroll, AI chat — optional in current templates)
- Often: Stacks packaging / Nostrbook MCP — use them if the scaffold installed them; do not invent a stack that is not in the repo

## Notes

- One project per directory.
- Pair with `opencode`. Do not re-document OpenCode install here.
- Deploy/hosting is out of scope for this skill.
