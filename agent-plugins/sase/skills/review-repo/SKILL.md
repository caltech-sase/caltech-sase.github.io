---
name: review-repo
description: Review a research software repository against Caltech SASE best practices (version control, tests, CI, dependencies, reproducible results, README, license, citation, secrets) and report what's missing, ordered by impact. Use when the user asks to review, audit, or check a research code repo, or asks how to make their project more reproducible or ready to share.
---

# Review a research software repository

Check the current repository against the
[Caltech SASE best practices](https://caltech-sase.github.io/best-practices/)
and give the user a short, prioritized list of what to improve.
Research codebases vary a lot, from a single analysis notebook to a
packaged library, so judge each item against what this project is for.

## Steps

1. Figure out what the project is: a library, an analysis or paper
   repo, a simulation code, a set of notebooks, etc.
   Read the README (if any), the top-level layout, and recent Git history.
2. Check each item in the checklist below.
   Look for evidence in the repo rather than assuming.
3. Report the results (see [Report](#report)).
4. Offer to fix the items that can be fixed in the repo,
   starting with the highest-impact one.
   Don't change anything until the user says which ones to do.

## Checklist

### Code

- **Version control:** The project is a Git repo with a remote
  (`git remote -v`), and work is committed rather than sitting
  uncommitted for long periods.
- **Tests:** There are automated tests, ideally covering the code
  the results depend on most.
- **Continuous integration:** Tests run automatically on each change,
  e.g., a GitHub Actions workflow in `.github/workflows/`.
- **Formatter and linter:** A tool like Ruff (Python) is configured,
  e.g., in `pyproject.toml` or a pre-commit config.

### Reproducibility

- **Dependencies declared:** Every package the code needs is recorded,
  with versions, in a checked-in file such as `pyproject.toml` with a
  lock file, `environment.yml`, `requirements.txt`, `Project.toml`
  (Julia), `renv.lock` (R), or a `Dockerfile`.
  Flag imports that aren't declared anywhere.
- **Automated path from raw data to results:** Figures, tables,
  numbers, and documents are produced by scripts or a pipeline
  (e.g., a Makefile, Snakemake, DVC, or Calkit), not by hand.
  Flag steps that are only described in prose, or that depend on
  notebooks being run in a particular order.
- **No hand-edited results:** Numbers in papers or reports come from
  code, not typed in.
- **Large data handled properly:** Large data files aren't committed
  directly to Git, but are still versioned, e.g., with DVC, Git LFS,
  or a data repository.
  Check for large tracked files with
  `git ls-files -z | xargs -0 du -h 2>/dev/null | sort -rh | head`.

### Sharing

- **README:** Explains what the code does, how to install it, and how
  to run it.
- **License:** A `LICENSE` file is present.
- **Citation:** A `CITATION.cff` file is present, and releases are
  archived with a DOI (e.g., via Zenodo) if the project is published.
- **No secrets:** No passwords, tokens, API keys, or private keys are
  committed. Check the current files and `.gitignore`, and look for
  obvious patterns (e.g., `.env` files, `AKIA`, `sk-`, `BEGIN PRIVATE KEY`).
  If a secret was ever committed, tell the user it must be rotated,
  since removing it from the latest commit doesn't remove it from history.

## Report

Start with a one-sentence summary of the project's overall state.
Then list the gaps, most important first, each with:

- What's missing and the evidence (file paths or commands).
- Why it matters for this project in particular.
- The smallest concrete step to fix it.

Treat committed secrets and results that can't be regenerated as the
most urgent. Briefly list what's already in good shape at the end,
so the user knows what not to worry about.
Keep the report short; don't pad it with items that don't apply.
