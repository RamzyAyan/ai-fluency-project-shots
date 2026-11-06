# My course project

This repository holds your project for **00560413 AI Fluency and Agentic Methods for
Engineers** (Technion). You will build it over the semester, one milestone at a time. It
starts with your project proposal from Week 1; later weeks add your ground, your agent
and their tests.

Course website: <https://technionaifluency.github.io/www/>
(the [project page](https://technionaifluency.github.io/www/project/) describes the
milestones; the [exercises page](https://technionaifluency.github.io/www/exercises/)
has each week's handout).

## The one rule: `main` only changes through a pull request

Never commit straight to `main`. For every change:

1. make a branch;
2. commit your change on it, and push the branch;
3. open a pull request (PR) into `main`;
4. read the diff and the checks, get a review, then merge;
5. `git switch main` and `git pull`, so your laptop has what GitHub has.

Why: a pull request shows exactly what changes before it lands, runs the checks on a
clean machine, and leaves a record of who reviewed what. When an agent writes code for
you later in the course, this is where you read its work before you accept it.

## What lives where

| Path | What it is |
| --- | --- |
| `docs/project-proposal.md` | Your project proposal. It starts as the blank Week 1 template; replace it with your own. Keep the four section headings and the file name. |
| `docs/disclosure.md` | Your AI-usage log: one line at the end of every exercise session. |
| `tests/test_proposal.py` | Checks on the proposal (see "The checks" below). Your own tests go in `tests/` too. |
| `.github/workflows/ci.yml` | Tells GitHub to run the checks on every pull request and on `main`. |
| `pyproject.toml`, `uv.lock` | The Python project and its exact package versions, for `uv`. Commit both. |
| `.gitignore` | Files Git must never record, `.env` (your secrets) first. |

## How to start

You need a terminal (Ubuntu in WSL2 on Windows, or the macOS Terminal), `git`, `uv`,
and `gh` signed in to your GitHub account (`gh auth status` says "Logged in"). The Week 2
handout walks through every step.

1. **Make your own copy.** On this repository's GitHub page, click **Use this template**,
   then **Create a new repository**. Owner: your own account. Name:
   `ai-fluency-project`, exactly (staff find your repository by this name). Visibility: **Public**.
2. **Clone it into your Linux home folder.** On Windows, work inside Ubuntu (WSL), never
   under `/mnt/c`:

   ```bash
   cd ~
   git clone https://github.com/<you>/ai-fluency-project.git
   cd ai-fluency-project
   ```

   Put your own GitHub username in place of `<you>`, without the `< >`.

3. **Install and run the checks.**

   ```bash
   uv sync
   uv run pytest
   ```

   On the blank template, four "is written" checks fail, one per proposal section. That
   is expected: they pass once each section has your own answer.
4. **Bring your Week 1 proposal, on a branch.**

   ```bash
   git switch -c add-proposal
   cp ~/my-project/docs/project-proposal.md docs/project-proposal.md
   uv run pytest
   git add docs/project-proposal.md
   git commit -m "Add my project proposal"
   git push -u origin add-proposal
   ```

   Then open the pull request in the browser: on your repository's page, **Compare &
   pull request**, then **Create pull request** (or, in the terminal,
   `gh pr create --base main --fill`). Read the PR, wait for the checks, get a review,
   and merge it (the rule above).

## The checks

| Check | When it runs | What it asks |
| --- | --- | --- |
| **Proposal structure** | every pull request, and every change on `main` | The proposal exists at `docs/project-proposal.md`, keeps its four section headings, and has no merge-conflict markers (`<<<<<<<`, `>>>>>>>`, or a line of exactly seven `=`, `=======`). |
| **Proposal complete** | every pull request | No section still has a `<!-- ... -->` placeholder. |

A red check is information, not a punishment. Click **Details** next to it, scroll to
the summary at the end of the log, and read the `FAILED` line: it names the section and
the line to fix. On your laptop, `uv run pytest` runs both checks before you push.

"Proposal complete" does not run on `main` itself, so a new repository made from this
template starts green; your pull requests are where it counts.
