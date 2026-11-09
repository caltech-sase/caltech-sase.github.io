---
title: Tools
nav_order: 5
---

# Tools

Software we've built to support research software development.

## Agent plugins and skills

The `research-software` plugin gives AI coding agents
[skills](https://agentskills.io) based on our
[best practices](best-practices/index.md).
It works with [Claude Code](https://code.claude.com),
[Codex](https://developers.openai.com/codex), and
[OpenCode](https://opencode.ai).

### Skills

| Skill         | What it does                                                                                                                                                                                                      |
| ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `review-repo` | Reviews a repository against our best practices (version control, tests, CI, dependencies, reproducible results, README, license, citation, and secrets) and lists what to improve, most important first. |

### Install

#### Claude Code

In a Claude Code session, run:

```text
/plugin marketplace add caltech-sase/caltech-sase.github.io
/plugin install research-software@caltech-sase
```

Or, from a terminal:

```sh
claude plugin marketplace add caltech-sase/caltech-sase.github.io
claude plugin install research-software@caltech-sase
```

#### Codex

From a terminal, run:

```sh
codex plugin marketplace add caltech-sase/caltech-sase.github.io
codex plugin add research-software@caltech-sase
```

You can also run `/plugins` in Codex and install it from the
Caltech SASE tab.
Start a new session afterward.

#### OpenCode

You'll need OpenCode 2 or newer. From a terminal, run:

```sh
opencode plugin add 'git+https://github.com/caltech-sase/caltech-sase.github.io.git#main::path:agent-plugins/research-software'
```

This adds the plugin to your global OpenCode config
(`~/.config/opencode/opencode.json`).

### Keep it up to date

#### Claude Code

Claude Code only updates plugins automatically for marketplaces that
have auto-update turned on, and it's off by default for ours.
To turn it on:

1. Run `/plugin` in a Claude Code session.
2. Go to the **Marketplaces** tab.
3. Select `caltech-sase`.
4. Select **Enable auto-update**.

Or add this to your `~/.claude/settings.json`:

```json
{
  "extraKnownMarketplaces": {
    "caltech-sase": {
      "source": {
        "source": "github",
        "repo": "caltech-sase/caltech-sase.github.io"
      },
      "autoUpdate": true
    }
  }
}
```

With auto-update on, Claude Code checks for updates shortly after you
start a session.
Run `/reload-plugins` to use the new version right away,
or it'll load the next time you start Claude Code.

To update by hand instead, run:

```sh
claude plugin marketplace update caltech-sase
claude plugin update research-software@caltech-sase
```

{: .note }
If you've set `DISABLE_AUTOUPDATER=1` to stop Claude Code from updating
itself, plugin auto-update is off too.
Also set `FORCE_AUTOUPDATE_PLUGINS=1` to keep plugins updating.

#### Codex

Codex checks for updates every time it starts and installs
them automatically, so there's nothing to set up.
To update by hand, run:

```sh
codex plugin marketplace upgrade caltech-sase
```

#### OpenCode

OpenCode checks for plugin updates when it starts, but it doesn't
install them on its own.
To update, run:

```sh
opencode plugin update
```

### Use

The agent picks up skills automatically when your request matches what
a skill is for, so you can just ask, e.g.:

> Review this repo against research software best practices.

> How can I make this project more reproducible?

To run a skill explicitly:

- **Claude Code:** `/research-software:review-repo`
- **Codex:** type `$` and pick `review-repo`, or browse with `/skills`
- **OpenCode:** ask it to use the `review-repo` skill

Skills only give the agent instructions.
Like any AI output, check what it tells you and review any changes it
makes before you commit them.

### Contribute

The plugin lives in the
[`agent-plugins/research-software`](https://github.com/caltech-sase/caltech-sase.github.io/tree/main/agent-plugins/research-software)
folder of this site's repository.
Suggestions and new skills are welcome: open an issue or pull request.
