# mkstack-skill

Kimi/Claude-style agent skill: create and build Nostr client websites using the [MKStack template](https://gitlab.com/soapbox-pub/mkstack.git) with OpenCode.

## What MKStack Includes

- **Nostr integration** — NostrProvider, hooks, utilities
- **React + Vite** — modern frontend stack
- **Tailwind CSS** — utility-first styling
- **shadcn/ui** — pre-built components
- **TypeScript** — type safety
- **Pre-built Nostr features** — comments, DMs, infinite scroll, AI chat

## Workflow

1. Scaffold with `stacks mkstack` (package `@getstacks/stacks`), or clone https://gitlab.com/soapbox-pub/mkstack.git when the CLI is not installed.
2. Read the new project's `AGENTS.md` before editing.
3. Build with Stacks' `stacks agent`, with OpenCode (`opencode` skill — do not hard-code a model id), or by editing the project directly.
4. Do not add NIP-28 chat, NIP-15 stalls, NIP-04 DMs, or NIP-96 uploads. The template's older examples mention some of those.

Requires the [opencode skill](https://github.com/NostrDanish/opencode-skill) only when OpenCode is the coder. Deploy with `npm run deploy` only when the user asked to publish.

## Install

Upload `SKILL.md` as a `.skill` package to your agent's skill library, or clone this repo into your skills directory.

## Source

Extracted from the openclaw-skills collection.
