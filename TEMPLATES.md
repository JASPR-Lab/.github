# Choosing a repo-template variant

Every new lab repo starts from [`JASPR-Lab/repo-template`](https://github.com/JASPR-Lab/repo-template).
The template contains one shared core skeleton plus three variants. You pick a variant
once, right after creating the repo.

| You are building... | Variant | What you get on top of the core |
|---|---|---|
| Code for a specific paper (experiments, analysis, figures) | `paper` | Data-provenance section in the README, `docs/PREPUBLICATION_CHECKLIST.md`, `data/` folder that is git-ignored, restricted-data notes |
| Code reused across papers (a library, a tool, a harness) | `library` | Packaging metadata, `CHANGELOG.md`, 90% coverage gate in CI, build check |
| A demo or project page (static site) | `demo` | `pages/` folder, static-site build CI with opt-in deploy; no `src/` or `tests/` |

When unsure between `paper` and `library`: if a second paper would import it, it's a `library`.

## How to create a repo

Org owners create repos (members can't create repos in this org).

```sh
# 1. Create from the template (private by default for research code)
gh repo create JASPR-Lab/<repo-name> --template JASPR-Lab/repo-template --private
# Wait ~10 seconds for GitHub to copy the template, or the clone comes down empty
gh repo clone JASPR-Lab/<repo-name>
cd <repo-name>

# 2. Apply a variant and name the Python package
python3 scripts/init_variant.py paper --name <python_package_name>

# 3. Review, then commit
git add -A && git commit -m "Initialize from repo-template (paper variant)"
git push
```

Then:

1. Edit `.github/CODEOWNERS` and replace the placeholder usernames.
2. Fill in the `README.md` placeholders, `CITATION.cff` and the license year/holder, if needed.
3. Give the right team or outside collaborators access (see the
   [lab-handbook access conventions](https://github.com/JASPR-Lab/lab-handbook/blob/main/conventions/repositories.md)).

## Naming

- Paper repos: `paper-<short-slug>` (e.g. `paper-membership-inference`)
- Libraries/tools: descriptive kebab-case (e.g. `tool-eval-harness`)
- Demos: `demo-<short-slug>`
