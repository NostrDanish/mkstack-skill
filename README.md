# mkstack-skill

Agent skill for starting a Nostr client from the [MKStack](https://gitlab.com/soapbox-pub/mkstack.git) template and building it with [OpenCode](https://github.com/NostrDanish/opencode-skill) or `stacks agent`.

The template's `AGENTS.md` is the source of truth for versions and hooks. This skill tells the agent to read that file instead of repeating a stack that has already changed once (the template now uses Nostrify, and its own docs disagree about React 18 vs 19).

## Install

Copy or symlink the directory that contains `SKILL.md` into the agent's skills path. Install OpenCode separately if that is the builder you want.
