# mkstack-skill

Agent skill for starting a Nostr web client from the [MKStack template](https://gitlab.com/soapbox-pub/mkstack.git) and building it with [OpenCode](https://github.com/NostrDanish/opencode-skill).

The template's own `AGENTS.md` is the source of project rules. This skill's job is the non-interactive scaffold (git clone, fresh git history) and the handoff to OpenCode. It does not depend on a particular agent's subagent API.

## Install

Copy `SKILL.md` into the agent's skills directory. The opencode skill must be available too.
