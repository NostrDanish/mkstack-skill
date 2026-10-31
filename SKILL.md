---
name: mkstack
description: "Scaffold a Nostr web client from the MKStack template and build it with OpenCode. Use when the user wants a new MKStack app or a Nostr client website started from that template. Not for general Nostr protocol work (nostr skill) and not for an existing app that is not MKStack."
---

# MKStack

MKStack is Soapbox's Nostr client template: React, Vite, Tailwind, shadcn/ui, and Nostrify. Template: https://gitlab.com/soapbox-pub/mkstack.git

The template's `AGENTS.md` and `.agents/skills` are the project rules. Read them after scaffold and follow them. This skill only gets a real MKStack tree onto disk and then hands the build to OpenCode.

## Scaffold

Use a short lowercase hyphenated project name. Put it in the workspace's `projects/` directory, not in the home directory.

```bash
mkdir -p <workspace>/projects
git clone --depth 1 https://gitlab.com/soapbox-pub/mkstack.git <workspace>/projects/<project-name>
cd <workspace>/projects/<project-name>
rm -rf .git
git init
git add .
git commit -m "Start from MKStack: https://gitlab.com/soapbox-pub/mkstack.git"
```

Keep `AGENTS.md`, `.agents/`, `opencode.json`, and `package.json`. Do not delete them to "clean up" the template.

`npm install -g @getstacks/stacks` and `stacks mkstack` is the upstream shortcut for people. Use it only when it can finish without interactive prompts. If it prompts, clone instead. Either way, the result must be this template, and `AGENTS.md` still applies.

## Build

Read `AGENTS.md` before changing product code.

Then use the `opencode` skill to run OpenCode from the project directory. The prompt must say: follow `AGENTS.md` in this repo, and build <what the user asked for>. Do not hardcode a model id. The opencode skill chooses one with `opencode models` unless the user named one.

If the host agent can spawn a subagent, the clone and the OpenCode run can go there so the main chat stays short. The subagent has to read this skill and the opencode skill first. There is no required spawn API. A host that has no subagent runs the same commands itself.

## Done

Report the project path, the files OpenCode added or changed, and how to run the dev server (`npm install` then the script `package.json` actually contains — read it, do not guess the script name).
