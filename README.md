# IOAA Concept Atlas

**[Open the atlas →](https://seratsaad.github.io/ioaa-knowledge-graph/)**

An interactive map of what the International Olympiad on Astronomy and
Astrophysics actually tests. Every paper from 2007 to 2025 is split into its
smallest scorable pieces — 800 units across 402 problems — and each is placed
against the topics the official IOAA syllabus itself lists.

Two topics are linked when the same exam part requires both. The strength is
directional: of the marks that test A, what fraction also demand B.

## What you can do with it

- View at the syllabus's own three levels: **section**, **content**, **topic**.
- Filter to **theory**, **data analysis** or **observation**, in any
  combination, over any span of years. Every number is recomputed from the
  parts you keep.
- See which syllabus topics are **not tested** in a given selection, drawn as
  hollow rings, and which examined material sits **outside the syllabus**
  altogether.

## What it shows

| | |
|---|---|
| Link weight inside one syllabus section | 40.8% |
| Same, for a rewired graph with identical degrees | 11.4% ± 1.1% |
| z | 25.9 |
| Off-syllabus marks, 2007–2012 | 1.6% |
| Off-syllabus marks, 2019–2025 | 3.5% |

The exam follows its syllabus far more closely than chance. It departs from it
in one direction: relativity, compact objects and gravitational waves, none of
which the syllabus names, and whose share has doubled.

Between 2007–2012 and 2019–2025 the largest gains were reading values off a
plot and least-squares fitting; the largest losses were naked-eye observation
and visual magnitude estimation. IOAA has moved marks out of visual observation
and into quantitative data analysis.

One caveat the atlas states on its own page: the syllabus was revised during
this period. The current version adds a Mathematical Methods and Tools section
including basic calculus, where the earlier text ruled calculus out.

## Source material

Problems and solutions come from the [IOAA problem
book](https://github.com/ioanazelko/ioaa-problem-book), which is **all rights
reserved**. Nothing here reproduces them: this repository contains only the
rendered map and a data file of syllabus topic names, mark shares and layout
positions. The analysis code lives in a separate private repository.

Not affiliated with or endorsed by the IOAA.

## Credits

Serat Saad and Fahim Rajit Hossain. The relevance metric follows Sun, Ting et
al. (2024), as used in the astro-ph knowledge graph.
