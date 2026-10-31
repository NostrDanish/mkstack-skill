---
name: mkstack
description: Create a Nostr client website from the MKStack template (React + Vite + Tailwind + shadcn + NostrProvider) and build it with OpenCode. Use when the user wants a new Nostr-powered web app or MKStack project. Always also load the `opencode` skill for how to run the CLI.
---

# MKStack

Template: https://gitlab.com/soapbox-pub/mkstack.git

Includes NostrProvider/hooks, React + Vite, Tailwind, shadcn/ui, TypeScript,
and starter Nostr skills (comments, DMs, infinite scroll).

**Always load the `opencode` skill** for install, PTY, model, and config.
This skill only covers the MKStack clone + post-build checks.

## Workflow

Do this in a subagent / separate session so the parent chat stays clean.
The worker must read **both** `mkstack` and `opencode` before starting.

### 1. Clone and re-init

```bash
mkdir -p <workspace>/projects
cd <workspace>/projects
git clone https://gitlab.com/soapbox-pub/mkstack.git <project-name>
cd <project-name>
# Keep the template README — agents need it. Do not delete it.
rm -rf .git
git init
git add .
git commit -m "Project created with MKStack: https://gitlab.com/soapbox-pub/mkstack.git"
```

Project names: lowercase, hyphens. Path is always
`<workspace>/projects/<name>`, never `$HOME`.

If GitLab is unreachable, say so and stop. Do not invent a template.

### 2. OpenCode

Ask the user for the model unless they already picked one. Then, from the
project directory, with a PTY (see opencode skill):

```bash
cd <workspace>/projects/<project-name>
opencode run --model <model> "<detailed project description>"
```

Do not hardcode a model string. Do not skip OpenCode and hand-edit the
scaffold unless the user asked for that.

Host spawn shapes (OpenClaw `sessions_spawn` vs Cursor shell):
[references/host-profiles.md](references/host-profiles.md).

### 3. Verify before reporting done

```bash
cd <workspace>/projects/<project-name>
test -f package.json
npm install
npm run build
```

Checklist:

- `NostrProvider` (or equivalent) is still wired in the app shell
- Relay list is configurable (env or kind-10002), not a single hardcoded relay
- No nsec in source or `.env` committed
- Dev script starts (`npm run dev`) if the user wants a preview

### 4. Report

Path, what OpenCode changed, build result, how to run.

## Failure modes

| Symptom | Next step |
|---|---|
| `git clone` fails | GitLab down or blocked; stop |
| OpenCode hangs / no output | Missing PTY — read opencode skill |
| `npm run build` fails | Read the error; fix or re-run OpenCode with the error text |
| Template README missing | You deleted it; restore from the clone URL |
