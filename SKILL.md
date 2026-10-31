---
name: mkstack
description: "Create a Nostr client website from the MKStack template (gitlab.com/soapbox-pub/mkstack, stack: React, Vite, Tailwind, shadcn/ui, Nostrify). Use when the user wants a new Nostr web app, a MKStack project, or to extend one. Triggers on MKStack, stacks mkstack, Nostrify client."
---

# MKStack

MKStack is Soapbox's Nostr client template. The project you create should be the user's app, built on that template, not a copy of the MKStack marketing site.

Official template: https://gitlab.com/soapbox-pub/mkstack (public domain). Docs: https://mkstack.xyz

## Create the project

Work in `<workspace>/projects/<project-name>` (lowercase, hyphens). Do not put it in the home directory.

Prefer the official scaffolder:

```bash
npm install -g @getstacks/stacks
cd <workspace>/projects
stacks mkstack
```

If `stacks` is not available, clone the template and make it a new repository:

```bash
mkdir -p <workspace>/projects
git clone https://gitlab.com/soapbox-pub/mkstack.git <workspace>/projects/<project-name>
cd <workspace>/projects/<project-name>
rm -rf .git
git init
```

Then read, in this order, before editing anything:

1. `AGENTS.md` in the new project
2. `.agents/skills/` in the new project
3. This skill, and the `opencode` skill if you are about to call OpenCode

Replace the template README with a README for the new app. The template is public domain; keep that notice if you redistribute the template code.

## Build it

Use whichever coder the user asked for.

**Dork (built into Stacks).** From the project directory:

```bash
stacks configure    # only if no provider is set; do not invent an API key
stacks agent
```

Providers Stacks documents: OpenRouter, Routstr, PayPerQ. The user supplies the credential. Never write it into the repo.

**OpenCode.** Read the `opencode` skill and run it from the project directory. Do not hard-code a model id. `opencode models` prints the ids that exist in this install. From an agent with no terminal prompts, pass `--auto` or the process stops on the first permission check.

**This agent.** Edit the project yourself when the user asked you to, using the same rules below. You do not have to spawn another agent.

Deploy with `npm run deploy` (NostrDeploy) only when the user asked to publish.

## What you must not build, even if an old README mentions it

- New NIP-28 public chat. It is unrecommended. Groups are NIP-29.
- New NIP-15 marketplace stalls. Classifieds are NIP-99.
- New NIP-04 DMs. Private messages are NIP-17.
- NIP-96 uploads. Media is Blossom (`useUploadFile` in the template; the `blossom` skill has the protocol).
- A flow that asks the user to paste an nsec. Web signers are NIP-07. Remote signers are NIP-46.

## Stack you can rely on

React, Vite, Tailwind, shadcn/ui, TypeScript, TanStack Query, React Router, Nostrify. Hooks already in the template include `useNostr`, `useAuthor`, `useCurrentUser`, `useNostrPublish`, `useUploadFile`, and `useZaps`. Re-read the project after scaffolding; versions move, and the files in the checkout win over this paragraph.

## Rules while editing

- Signer interface only. Keys stay in the extension or bunker.
- Validate events you depend on (id and signature) before acting on them.
- Publish to the user's write relays and read from their read relays (NIP-65), not one hard-coded relay. The template's `AGENTS.md` has replaced `relay.damus.io` with `nos.lol` in defaults; follow the file you just read.
- Escape untrusted note content. Do not render it as HTML.
- Run the project's test script (`npm test` or the script `package.json` actually has) before you say the app works.
