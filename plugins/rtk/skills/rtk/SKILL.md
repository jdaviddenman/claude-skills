---
name: rtk
description: >
  RTK (Rust Token Killer) — token-optimized CLI proxy saving 60-90% on dev
  operations. A PreToolUse hook rewrites most Bash commands to `rtk <cmd>`
  automatically; this skill covers the meta commands that must be typed
  directly (`rtk gain`, `rtk discover`, `rtk proxy`) and how to verify the
  install. Use when the user says "rtk", "token savings", "token killer",
  asks how much RTK has saved, reports `rtk: command not found`, or when a
  command needs to bypass RTK filtering.
---

# RTK — Rust Token Killer

Token-optimized CLI proxy. Cuts 60-90% of tokens on dev operations by
filtering command output before it reaches the model.

## Hook-based usage (the normal path)

A `PreToolUse` hook on `Bash` rewrites commands automatically:
`git status` becomes `rtk git status`. This is transparent and costs no
tokens. Do not prefix commands with `rtk` by hand — the hook does it.

## Meta commands (always type `rtk` directly)

```bash
rtk gain              # Show token savings analytics
rtk gain --history    # Show command usage history with savings
rtk discover          # Analyze Claude Code history for missed opportunities
rtk proxy <cmd>       # Run a raw command with no filtering (for debugging)
```

Use `rtk proxy` when filtering hides output you need — a full diff, a
complete log, byte-exact text you are about to parse.

## Verifying the install

```bash
rtk --version         # Should print: rtk X.Y.Z
rtk gain              # Should work, not "command not found"
which rtk             # Confirm the right binary
```

**Name collision:** if `rtk gain` fails, the installed binary may be
reachingforthejack/rtk (Rust Type Kit), a different tool with the same name.
Check `which rtk` and `rtk --version` before assuming RTK is broken.

## Failure modes

- `rtk: command not found` — RTK is missing from `PATH`. Every hooked Bash
  call fails, not just one. Say so plainly; do not retry the same command.
- Output looks truncated or reformatted — that is the filter working. Rerun
  through `rtk proxy` if you need the raw bytes.
