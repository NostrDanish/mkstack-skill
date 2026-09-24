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

1. Spawn a subagent (keeps main chat clean)
2. Subagent reads **both** the mkstack and opencode skills
3. Clone template → fresh git init → run OpenCode with the project description
4. Report what was created

Requires the [opencode skill](https://github.com/NostrDanish/opencode-skill).

## Install

Upload `SKILL.md` as a `.skill` package to your agent's skill library, or clone this repo into your skills directory.

## Source

Extracted from the openclaw-skills collection.
