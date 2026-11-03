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
