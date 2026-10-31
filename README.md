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
3. Prefer `npm create mkstack@latest`; clone only if the generator is missing (keep the upstream README / SHA)
4. Run OpenCode with `--auto` and a model from `opencode models` — do not hardcode model ids
5. Report what was created

Requires the [opencode skill](https://github.com/NostrDanish/opencode-skill). OpenClaw `sessions_spawn` / `pty` blocks in SKILL.md map to a long-running terminal on Cursor and similar hosts.

## Install

Upload `SKILL.md` as a `.skill` package to your agent's skill library, or clone this repo into your skills directory.

## Source

Extracted from the openclaw-skills collection.
