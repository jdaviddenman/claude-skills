# claude-skills

Personal Claude Code skills, packaged as a plugin marketplace.

## orwell

Plain-English writing discipline. Applies the six rules from George Orwell's
*Politics and the English Language* (1946) to any prose Claude writes — docs,
commit messages, comments, PR bodies, replies:

1. Never use a metaphor, simile, or other figure of speech which you are used to seeing in print.
2. Never use a long word where a short one will do.
3. If it is possible to cut a word out, always cut it out.
4. Never use the passive where you can use the active.
5. Never use a foreign phrase, a scientific word, or a jargon word if you can think of an everyday English equivalent.
6. Break any of these rules sooner than say anything outright barbarous.

Code, identifiers, paths, commands, quoted errors, and log output are left alone.

## rtk

How to work with RTK (Rust Token Killer), a proxy that filters CLI output
before it reaches the model. A `PreToolUse` hook
rewrites `git status` to `rtk git status` on its own, so the skill covers the
parts the hook cannot do for you:

- the meta commands you must type directly — `rtk gain`, `rtk gain --history`,
  `rtk discover`, `rtk proxy <cmd>`
- when to reach for `rtk proxy`: you need the raw bytes, not the summary
- how to check the install, and the name collision with Rust Type Kit, a
  different tool that also answers to `rtk`
- what `rtk: command not found` means — every hooked Bash call is failing, so
  say so instead of retrying

## Install

```
/plugin marketplace add jdaviddenman/claude-skills
/plugin install orwell@claude-skills
/plugin install rtk@claude-skills
```

Install either one on its own; they share nothing.

For orwell, say `orwell`, `plain English`, or `tighten this` — or run
`/orwell`. Turn it off with `stop orwell`. For rtk, say `rtk` or ask about
token savings — or run `/rtk`.

## Run one in every session

A skill loads when something in your prompt matches its description. To load
one every time instead, add a `SessionStart` hook to `~/.claude/settings.json`
— its stdout goes into the session context before you type anything:

```json
{
  "hooks": {
    "SessionStart": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "cat ~/.claude/plugins/cache/claude-skills/rtk/*/skills/rtk/SKILL.md"
          }
        ]
      }
    ]
  }
}
```

The `*` is the installed version. Point the path at `orwell/*/skills/orwell`
for the other skill, or at `~/.claude/skills/<name>/SKILL.md` if you keep a
personal copy outside the plugin.

Loading a skill on every session spends its tokens on every session. Worth it
for rules that should never lapse; wasteful for anything you need now and then.

## License

MIT
