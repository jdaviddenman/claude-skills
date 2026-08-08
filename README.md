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

## Install

```
/plugin marketplace add jdaviddenman/claude-skills
/plugin install orwell@claude-skills
```

Then say `orwell`, `plain English`, or `tighten this` — or run `/orwell`.
Turn it off with `stop orwell`.

## Run it in every session

Add a `SessionStart` hook to `~/.claude/settings.json` so the rules load
before you type anything:

```json
{
  "hooks": {
    "SessionStart": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "cat ~/.claude/skills/orwell/SKILL.md"
          }
        ]
      }
    ]
  }
}
```

A `SessionStart` hook's stdout is added to the session context.

## License

MIT
