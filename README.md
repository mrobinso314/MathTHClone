# Math Trailhead

A self-paced precalculus and college algebra review built in
[PreTeXt](https://pretextbook.org), with most exercises presented as live
[WeBWorK](https://webwork.maa.org) problem.

**Live site:** https://kyleormsby.github.io/math-th/

## Status

Working prototype. Hundreds of WeBWorK exercises across the core review
chapters, plus curated Math 111, Stat 141, and Econ 201 course-readiness diagnostics,
imported from the
[Moodle course](https://moodle.reed.edu/course/view.php?id=6466).

Known gaps, carried over from the import:

- Roughly two dozen problems threw errors (most often a missing `statement`
  tag) and are commented out in place.
- Some problems have rendering issues that were fixed on Reed's WeBWorK but
  not in the Open Problem Library version referenced here, e.g. using `x`
  rather than `['x']` for LaTeX. Inline comments mark the cases that were
  noticed; there are probably more.
- The syllabus page is still template boilerplate.

Both classes of problem are the motivation for eventually hosting corrected
copies of the problems ourselves rather than referencing the OPL. See
`docs/webwork-server-setup.md`.

## How it is organized

The main book has two parts: **Part I: Problems**, containing diagnostics and
practice worksheets, and **Part II: Lessons**, with each lesson as a chapter
and each topic as a section on its own page. The sidebar lists all three
levels (part, chapter, and section).

Chapter introductions and the overall book structure live in
[`source/main.ptx`](source/main.ptx). Front-matter pages live in
[`source/frontmatter.ptx`](source/frontmatter.ptx), while individual content
pages are grouped by chapter under [`source/activities`](source/activities).
The Math 111, Stat 141, and Econ 201 diagnostic sections are in
[`source/activities/diagnostics`](source/activities/diagnostics).

In Part II, the
[`Trigonometry`](source/activities/reed-algebra-lessons/trigonometry.ptx)
chapter has an overview and a separate page for each topic. It connects
the unit circle to right triangles, derives the Pythagorean identity, develops
the family `A cos(wx + T) + C`, including vertical displacement, and introduces tangent, cotangent, secant, and
cosecant. Existing WeBWorK exercises accompany written checkpoints. Its illustrations live in
[`assets/reed-algebra-lessons`](assets/reed-algebra-lessons).

The [Quadratic Formula](source/activities/reed-algebra-lessons/quadratic-formula.ptx)
chapter contains three separate topic pages: functions and zeros, solving with
the formula (including practice with expandable solutions), and a visual
completing-the-square derivation. Its source pages are in
[`quadratics`](source/activities/reed-algebra-lessons/quadratics). Standard
section-level HTML chunking supplies the topic pages. Existing chapter and
page IDs are retained so previously published links continue to work.
The quadratic lessons mix three visible worked examples with four optional
example dropdowns. They also reuse three Part I WeBWorK problems for
instant-feedback practice, alongside the written checkpoints. An additional
randomized problem, authored directly in PreTeXt, checks the discriminant
and both branches of the quadratic formula. Quadratic examples and
checkpoints use numbered headings without descriptive titles.

The separate blank lesson book is in [`lessons`](lessons). Its first section,
[`Function Review`](lessons/sections/function-review.ptx), is intentionally
empty and is published beneath the main site at `/lessons/`.

Most interactive exercises use `<webwork source="Contrib/CCCS/..."/>` references
into the Open Problem Library; the quadratic-formula problem is authored inline
in PreTeXt. No `.pg` files live in this repository; the problems are rendered at read time by whichever WeBWorK server is named in
[`publication/publication.ptx`](publication/publication.ptx).

## Building locally

```bash
pretext build course   # build the HTML
pretext build lessons  # build the separate lesson book
pretext view course    # serve it and open a browser
```

The build needs network access to the WeBWorK server to generate problem
representations, and to Runestone's CDN for interactive components.

## Deploying

Pushing to `main` triggers `.github/workflows/pretext-cli.yml`, which builds
the book and publishes it to GitHub Pages. Nothing else is required; the
built HTML is deliberately not committed to the repository.

To publish without pushing a content change, run the **PreTeXt-CLI Actions**
workflow manually from the Actions tab.

See [`docs/deploying.md`](docs/deploying.md) for the one-time setup and for
notes on moving to Reed-hosted infrastructure.
