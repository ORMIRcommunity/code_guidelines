# Code review

## What is code review?
Code review is the practice of having someone other than the author read through a piece of code before it is merged or used to produce published results. The goal is to catch bugs, improve clarity, share knowledge across a group, and end up with code that another person in the lab can run six months from now.
For research software, this is one of the cheapest and highest-value reproducibility practices available. JOSS treats it as a publication requirement, and the major ORMIR projects (ORMIR-XCT, ORMIR-MIDS) already use pull-request review as the standard mechanism for accepting changes.

---

## Why bother in a small lab?
A common objection is that code review is overhead a research group cannot afford. In practice, even a single 10-minute review catches a large fraction of obvious bugs and forces the author to write code that another human can follow. Three concrete benefits:
- Correctness. Bugs in analysis pipelines invalidate results. A second pair of eyes is the simplest defence.
- Continuity. When a student leaves, reviewed code is far more likely to remain usable by the next person.
- Training. Reviewing other people's code is one of the fastest ways for junior members to learn idiomatic Python and a project's conventions.

---

## What should I check before opening a review?
Most of the value of code review comes from forcing the author to read their own work as if a stranger wrote it. Before requesting a review, run the checklist above on your own diff: skim every changed line, read your own docstrings, and confirm the code still runs from a clean clone. This removes the bulk of obvious issues and lets the human reviewer focus on what only a second person can catch.

---

## What should reviewers watch for in imaging or numerical code?
Generic linters do not catch the bugs most likely to bite scientific image-processing code. When reviewing pipelines that touch microCT volumes, segmentation masks, or other imaging data, watch specifically for:

- Silent type coercion (e.g. int to float, float32 to float64) that changes results without warning.
- Off-by-one errors in voxel indexing, especially around region masks and boundary slices.
- Confusion between voxel coordinates, physical coordinates (mm), and world coordinates. Function signatures should make this explicit.
- Hard-coded image dimensions, isotropic-voxel assumptions, or orientation conventions (LPS vs RAS).
- Reproducibility under different numpy, scipy, or SimpleITK versions. Pinning matters more here than in most domains.

---

## What about Jupyter notebooks?
Notebooks are harder to review than scripts because the diff includes execution outputs, cell metadata, and sometimes binary blobs. A few practical recommendations:

- Strip outputs before commit, either manually or with nbstripout as a pre-commit hook. The repo should store the code, not the runs.
- Use jupytext to pair each .ipynb with a .py mirror that is the actual reviewable artifact.
- For visual diffs of the notebook itself, nbdime is much more useful than the default GitHub view.
- Run linters and tests on notebooks with nbqa (e.g. nbqa ruff, nbqa pytest).
- Once notebook logic stabilizes, move it into a regular module that the notebook imports. Treat heavy analysis notebooks as drafts.

---

## What if I'm the only person on the project?
A strict "wait for a reviewer" policy is unrealistic for a solo project. Two practical substitutes: open a pull request anyway and self-review it after a 24-hour gap (you will read your own code differently the next day), and run an AI review tool as a non-blocking second pass. Neither replaces a human reviewer for code that supports a publication, but both are far better than merging straight to main.

---

## Where do AI tools fit?
AI-assisted review (GitHub Copilot review, CodeRabbit, Cursor) is useful as a first pass for style issues, obvious bugs, and missing edge cases. It does not replace a human reviewer who understands the scientific intent of the code. Suggested workflow: run an AI pass before opening a review request, resolve those comments yourself, then let the human reviewer focus on substance.

---

## Recommended Python tooling
Pull-request workflow on GitHub or GitLab, with at least one required approval before merge.
Formatters (ruff, black) run before review so the diff is not full of style noise.
Static checks (ruff, mypy) wired into CI so the reviewer is not the linter.
Tests with pytest, executed automatically on each PR via GitHub Actions.
pre-commit (pre-commit.com) to tie the above together at commit time.
Notebook tooling: nbstripout, jupytext, nbdime, nbqa.

---

## Further reading
- JOSS review checklist: https://joss.readthedocs.io/en/latest/review_checklist.html
- Google, How to do a code review: https://google.github.io/eng-practices/review/
- The Turing Way, Code Reviewing: https://book.the-turing-way.org/reproducible-research/reviewing
- MIT 6.102, Code Review (current semester): https://web.mit.edu/6.102/www/sp26/classes/03-code-review/
- Wilson et al., Good Enough Practices in Scientific Computing, PLOS Comp Bio 2017: https://doi.org/10.1371/journal.pcbi.1005510
- Software Sustainability Institute, code review guide: https://www.software.ac.uk/guides/recommended-practice-code-review

