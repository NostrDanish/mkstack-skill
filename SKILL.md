---
name: mkstack
description: "Scaffold a Nostr client from the MKStack template and build it with OpenCode or the template's own agent. Use when the user wants a new Nostr web app, a MKStack project, stacks mkstack, or a site based on gitlab.com/soapbox-pub/mkstack. The checkout's AGENTS.md wins over this file when they disagree."
---

# MKStack

MKStack is a Nostr client template (Vite, React, Tailwind, shadcn/ui, Nostrify). The template moves. Read the files you just created. Do not trust version numbers remembered from this skill.

## Create the project

Work in `<workspace>/projects/<project-name>` (lowercase, hyphens). Not the home directory.

Preferred, the template's own installer:

```bash
mkdir -p <workspace>/projects
cd <workspace>/projects
npm install -g @getstacks/stacks
stacks mkstack --help          # use only flags this prints
stacks mkstack
```

Fallback, a plain clone. Delete `.git` only. Keep `AGENTS.md`, `opencode.json`, `.agents/`, and `package.json`.

```bash
git clone https://gitlab.com/soapbox-pub/mkstack.git <project-name>
cd <project-name>
rm -rf .git
git init
git add .
git commit -m "Start from MKStack: https://gitlab.com/soapbox-pub/mkstack.git"
```

## Before writing any feature

1. Read `AGENTS.md` in the project. It is the agent's spec for this checkout (stack, hooks, security).
2. Read `package.json` for the real dependency versions.
3. Read `App.tsx` before editing it. Providers are already wired (`QueryClientProvider`, `NostrProvider`, `NostrLoginProvider`).
4. Hooks you will actually use live in `src/hooks/`: `useNostr`, `useCurrentUser`, `useAuthor`, `useNostrPublish`, `useUploadFile`. List the directory rather than guessing names.

Security rules from the template, which this skill repeats because they are easy to "clean up" by accident:

- Event content is untrusted. No `dangerouslySetInnerHTML`, no `innerHTML`, no `document.write` on it.
- Do not relax the CSP in `index.html` (`script-src 'self'`, no `unsafe-eval`, no `unsafe-inline` scripts).
- The template stores nsecs in `localStorage`. An XSS is a stolen identity. Treat that as the top bug class.
- Never use the TypeScript `any` type.
- Relays index single-letter tags only. Filter in the query, not after downloading everything.
- A new kind needs an `alt` tag, and `NIP.md` in the project must document it. Prefer an existing NIP. Check with the `nostr-nips` skill before inventing one.

## Build

From the project directory, with a PTY, follow the `opencode` skill. The prompt must tell OpenCode to follow `AGENTS.md` and not to replace the providers.

If the user asked for the template's own agent instead of OpenCode: `stacks agent`, then the same prompt.

On OpenClaw or Hermes you may run this in a subagent. The subagent has to read this skill and the opencode skill itself. `sessions_spawn` is that runtime's API, not a universal one.

## Check, then deploy

```bash
npm test
npm run dev
```

`npm run deploy` publishes to NostrDeploy. Run it only when the user asked to deploy.
