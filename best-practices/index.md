---
title: Best practices
nav_order: 2
has_children: true
has_toc: false
---

# Best practices

Habits that make research software reliable, reproducible, and reusable.
You don't need to adopt them all at once. Start with the first few and add
more as your project grows.

## General principles

- Be clear and focused about what your product (research or software) does:
  what problem it solves for whom.
  Think about how to measure if it's doing its job and see if you can
  track those metrics as it evolves.
- Work in small steps, releasing as often as possible to gather feedback
  and learn if your solution works and if it needs to change.

## Code

- **Use version control for everything.** Track your code with Git and push
  it to a remote like GitHub, so you have history and a backup.
  See [Version control](version-control.md).
- **Write tests.** Start with the code your results depend on most.
  See [Testing](testing.md).
- **Run tests automatically.** Use continuous integration (e.g., GitHub
  Actions) to run tests on every change.
- **Use a formatter and linter.** Let tools like Ruff enforce a consistent
  style, so reviews can focus on what the code does.
- **Get your code reviewed.** A second pair of eyes catches bugs and
  spreads knowledge.
- **Review AI-generated code like any other code.** Read it, test it, and
  make sure you understand it before relying on it.
  See [Coding with AI agents](ai-agents.md).

## Reproducibility

- **Declare your dependencies.** Record every package your code needs, with
  versions, in a file checked into the repo.
  See [Environments and dependencies](environments.md).
- **Automate the path from raw data to results.** Generate figures,
  tables, numerical results, and finished documents (e.g., PDFs)
  with scripts or a pipeline, not by hand.
  Avoid manually transferring data between tools or platforms if possible.
- **Never edit results by hand.** If a number in a paper changes, it
  should be because the code that produced it changed.
- **Keep large data out of Git, but version control it nonetheless.**
  Use a tool built for data (e.g., DVC or
  Git LFS) or a data repository.

If you want a framework that has all of these baked in, check out
[Calkit](https://github.com/calkit/calkit),
built by one of our own Research Software Engineers.

## Sharing

- **Write a README.** Explain what the code does, how to install it, and
  how to run it.
- **Add a license.** Without one, others can't legally reuse your code.
- **Make it citable.** Add a `CITATION.cff` file and archive releases with
  a DOI (e.g., via Zenodo).
- **Keep secrets out of the repo.** Never commit passwords, tokens, or API
  keys.
