# caltech-sase.github.io

Source for <https://caltech-sase.github.io>, built with
[Jekyll](https://jekyllrb.com) and the
[Just the Docs](https://just-the-docs.github.io/just-the-docs/) theme.
A GitHub Actions workflow (`.github/workflows/pages.yml`) builds the site
and deploys it on every push to `main`.

## Adding content

Pages are plain Markdown files with a small front matter block:

```markdown
---
title: My new page
parent: Best practices   # Omit for a top-level page
nav_order: 5             # Position in the sidebar
---

# My new page

Content goes here.
```

Sections live in folders (e.g., `best-practices/`, `tutorials/`), each with
an `index.md`. Link to other pages with relative paths to the `.md` file,
e.g., `[Testing](testing.md)`.

Try to stick to standard Markdown, so the content is easy to move to
another tool (e.g., Quarto) later.

## Agent plugin

This repo is also a `caltech-sase` plugin marketplace for Claude Code and
Codex, and hosts an OpenCode plugin.
User-facing install and usage docs are on the [Tools](tools.md) page.
For Claude Code, users can install it with:

```text
/plugin install sase --marketplace caltech-sase/caltech-sase.github.io
```

All three tools share one set of skills in
`agent-plugins/sase/skills/`:

```text
.claude-plugin/marketplace.json     # Claude Code marketplace
.agents/plugins/marketplace.json    # Codex marketplace
agent-plugins/sase/
├── .claude-plugin/plugin.json      # Claude Code manifest
├── .codex-plugin/plugin.json       # Codex manifest
├── package.json, index.js          # OpenCode plugin (registers the skills)
└── skills/<skill-name>/SKILL.md
```

To add a skill, create `skills/<skill-name>/SKILL.md` with `name` (matching
the folder name, lowercase with hyphens) and `description` frontmatter on
single lines.
Then add it to the skills table on the Tools page.

The manifests intentionally have no `version`, so every commit that changes
the plugin counts as a new version and reaches users who have auto-update
on.

To test locally:

```sh
claude plugin validate .
claude --plugin-dir ./agent-plugins/sase
```

The `agent-plugins` folder is excluded from the Jekyll build in
`_config.yml`.

## Under construction notice

While the site isn't ready for use, every page shows a banner. To remove it,
delete the "Under construction" block and the breadcrumb fix in
`_sass/custom/custom.scss`.

## Previewing locally

You'll need Ruby (e.g., `brew install ruby`; the macOS system Ruby is too
old). Then run:

```sh
bundle install
bundle exec jekyll serve
```

and open <http://localhost:4000>.
