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

## How it works

Eight steps, each one a line of arithmetic. Nothing here is a black box.

### 1. Split the papers into scorable units

A *unit* is the smallest thing the marking scheme puts a number on: a sub-part
where the paper gives per-part marks, the whole problem where it does not. That
gives **800 units** across 402 problems, 2007–2025.

### 2. Make marks comparable across years

Raw marks cannot be compared: the 2007 median problem was worth 2 points, the
2008 median 20. So each unit's marks are normalised by its year's total,

> **w(u) = marks(u) / Σ marks over that year**

Every olympiad then contributes exactly 1, and the whole corpus sums to 19, one
per year. Two gaps are handled explicitly: 2012 and 2014 published no marks at
all and 2015 only three, so those problems take their year's median problem
value; problems with no per-part breakdown split their total evenly. Every unit
records which of these applied to it.

### 3. Place each unit on the syllabus

Each unit was read together with its official solution and tagged with the
concepts a solver must actually *use* — not every topic the question mentions.
Those concepts are then mapped onto the topics the official syllabus itself
lists. Writing **K(u)** for the set of syllabus nodes a unit touches at a given
level, note it is a *set*: a unit needing two concepts from one Content counts
once for that Content, not twice.

### 4. Node mass: how heavily something is examined

> **m(A) = Σ w(u) over every unit whose K(u) contains A**

A dot's area is proportional to m(A). The percentage shown is m(A) divided by
the total weight of the selection. **These shares do not sum to 100%** — they
sum to about 400%, because a unit requiring four topics counts toward all four.
Read it as coverage: *this fraction of the exam's marks sits in parts that
require A*, not as a slice of a pie.

### 5. Links: what gets examined together

For a pair, the joint mass is the weight of the units needing both:

> **n(A,B) = Σ w(u) over units whose K(u) contains both A and B**

The link strength is directional, and it is just a conditional probability:

> **p(B|A) = n(A,B) / m(A)**

*Of the marks that test A, this fraction also demand B.* Direction matters and
the atlas keeps both readings — 36% of the marks on orbital energy also need
Kepler's first law, while only 20% the other way. Layout uses the mean of the
two. Each pair also carries the hub-corrected

> **npmi(A,B) = log[ P(A,B) / P(A)P(B) ] / −log P(A,B)** ∈ [−1, 1]

which asks whether two topics co-occur more than their individual frequencies
would predict, so that a topic appearing everywhere cannot fake a strong link.

This is the exam analogue of the citation relevance used in the astro-ph
knowledge graph of Sun, Ting et al. (2024), where the question is what fraction
of the papers cited by work on A discuss B.

### 6. Decide which links survive

Keeping every pair would produce a hairball, and single observations would look
like structure. So:

1. A pair needs **at least two separate exam parts** behind it. One unusual
   question cannot invent a relationship.
2. Each node keeps its **6 strongest** outgoing links, plus any link above a
   floor of 0.05. The union of those is the edge set.
3. That leaves topics examined exactly once with no link at all. Rather than
   drop them — they include main-sequence stars and radioactive decay — each
   gets its strongest single-part links, drawn **dashed** and excluded from
   every statistic on the page.

### 7. Position

**ForceAtlas2** with logarithmic attraction: linked nodes pull together,
everything repels everything, and heavier nodes repel more. There are no axes
and no units — **only nearness means anything**. Communities come from the
**Leiden** algorithm on the symmetric weights. Syllabus topics nothing examines
have no links to place them, so they are parked beside their own Content group
and drawn as hollow rings.

### 8. Filter by round and period, live

Mass is additive over exam parts, so every quantity is stored per
(round × period) cell and summed over whichever cells you leave selected:

> **m(A) = Σ m<sub>cell</sub>(A)**, and then **p(B|A) = n(A,B) / m(A)** as before

Ratios are never summed — they are re-derived from the sums each time. That is
why theory alone, data analysis alone, or any mixture over any span of years all
give correct shares and link strengths rather than approximations.

### Does the exam follow its own syllabus?

The test is whether links stay inside a syllabus section more than chance
allows. Take the share of link weight whose two ends share a section, then
compare it against 200 rewirings of the graph that keep every node's degree and
reshuffle the weights, which destroys syllabus structure and nothing else.

| | |
|---|---|
| Observed, links inside one section | 40.8% |
| Rewired null | 11.4% ± 1.1% |
| **z** | **25.9** |

Counting the dashed links too gives 36.0% against the same null, so the answer
does not depend on that choice. Newman's assortativity on section labels agrees
at 0.27.

A caution on reading the map's communities: the Leiden partition agrees only
weakly with the syllabus sections. That is a limitation of partition-matching
scores on overlapping structure, not evidence against the result above — the
assortativity and null test are the ones to quote.

### What the method cannot tell you

- Tagging is a judgement call, made once per unit against a fixed vocabulary.
- "Untested" means no concept in this atlas maps onto that syllabus topic in
  the current selection. Sometimes that is a genuine gap, sometimes a
  granularity mismatch where one concept here covers several syllabus topics.
- The syllabus was revised during the period studied, so 2007 papers are being
  read against a document later than the one their authors used.
- Marks measure what examiners rewarded, which is not the same as difficulty.

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
