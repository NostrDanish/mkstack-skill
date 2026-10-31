# Host profiles for MKStack + OpenCode

## Cursor / generic shell

Parent: spawn a subagent (or a tmux session) whose only job is this workflow.
Worker: read mkstack + opencode, then run the clone and `opencode run` via
the host shell with a PTY and a ~10 minute block.

There is no `sessions_spawn` API here. Do not emit that block as if it were
a tool call.

## OpenClaw

```
sessions_spawn:
  task: "CRITICAL: Read mkstack SKILL.md and opencode SKILL.md first. Then create an MKStack project: <description>. Project path: <workspace>/projects/<project-name>. Ask for / use model <model>. Do not skip OpenCode."
  label: "mkstack-<project-name>"
  runTimeoutSeconds: 660
```

OpenCode exec still needs `pty: true` and a yield/timeout that covers the run.
See the opencode skill `references/host-spawn.md`.
