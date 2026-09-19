# IOAA Knowledge Graph

**[Open the map](https://seratsaad.github.io/ioaa-knowledge-graph/)**

Hi everyone. We went through every problem the International Olympiad on
Astronomy and Astrophysics has set between 2007 and 2025, worked out what each
one asks you to know, and drew the result as a map.

We split the papers into 800 scored parts across 402 problems, read each part
next to its official solution, and matched what it needs to the 175 topics the
official syllabus lists. We link two topics when the same exam part needs both.

## What you can do with it

- Look at the map at any of the three levels the syllabus itself uses, which
  are section, content and topic, or at the problem book's own 14 chapters.
- Keep theory, data analysis or observation, in any mix, over any stretch of
  years. We recompute every number from the parts you keep.
- Find the syllabus topics nothing tests in your selection, which we draw as
  hollow rings, and the material the exam tests that the syllabus never names.

## How we built it

Eight steps, each one a line of arithmetic. We hide nothing.

### 1. We split the papers into scored parts

We take the smallest piece the marking scheme puts a number on. Sometimes that
means a sub-part and sometimes a whole problem. We end up with **800 parts**
across 402 problems.

### 2. We make marks comparable across years

Marks do not mean the same thing from one year to the next. The median 2007
problem carried 2 points and the median 2008 problem carried 20. So we divide
each part's marks by the total for its year.

> **w(u) = marks(u) / total marks that year**

Pooling a year's marks in one lump still gets the balance wrong, because it
lets whichever round we happen to hold more parts for take over. IOAA scores
theory, data analysis and observation 2 to 1 to 1, so we normalise each round
inside itself and then hand it its official share of the year. Pooling gave
theory 59 per cent of the weight. It now gets the 50 per cent the statutes give
it.

Three gaps are handled openly. The 2012 and 2014 papers never published marks
and 2015 published only three, so those problems take their year's median
problem value. Where a problem shows no per-part marks we split its total
evenly. The book carries no observation round for 2010, 2013 and 2020, so in
those years we spread the observation share across the rounds we do hold and the
year still counts once. We record all of it per part, so you can check us.

### 3. We place each part on the syllabus

We read each part next to its official solution and write down the concepts you
actually need to *use*, not every topic the question mentions. Then we match
those concepts to the topics the official syllabus lists. Writing **K(u)** for
the topics a part needs, note that it is a set. A part needing two concepts from
one Content counts once for that Content, not twice.

### 4. We measure how heavily a topic is examined

> **m(A) = sum of w(u) over every part that needs A**

A dot's area follows m(A). The percentage we show divides that by the total
weight of your selection. **These percentages do not add up to 100.** They add
up to roughly 400, because a part needing four topics counts toward all four.
Read a number as coverage. It tells you what share of the marks sit in parts
that need A, not what slice of a pie A owns.

### 5. We link topics that get examined together

> **n(A,B) = sum of w(u) over parts that need both**
>
> **p(B|A) = n(A,B) / m(A)**

Read that as the share of marks testing A that also demand B. Direction matters,
so we keep both readings. Of the marks on orbital energy, 39 per cent also need
Kepler's first law, while only 21 per cent run the other way. For the layout we
average the two.

We also work out normalised pointwise mutual information for every pair, which
asks whether two topics turn up together more often than their separate rates
predict. That stops a topic appearing everywhere from faking a strong link.

We took this measure from Sun, Ting et al. (2024), who built the astro-ph
knowledge graph by asking what share of the papers cited by work on A discuss B.
We ask the exam version of the same question.

### 6. We decide which links to keep

Keeping every pair would give us a hairball, and single observations would look
like structure. So we apply three rules.

1. A pair needs **at least two separate exam parts** behind it. One unusual
   question should not invent a relationship.
2. Each topic keeps its **six strongest** links, plus any above a floor of 0.05.
   We take the union of those.
3. That leaves topics examined only once with no link at all. We did not want to
   drop them, because they include main-sequence stars and radioactive decay. So
   we draw their strongest single-part links **dashed** and keep those out of
   every number we quote.

### 7. We place the topics

We lay the map out with **ForceAtlas2** using logarithmic attraction. Linked
topics pull together, everything pushes everything else apart, and heavier
topics push harder. There are no axes and no units. **Only nearness means
anything.** We group topics with the **Leiden** algorithm. Syllabus topics that
nothing tests have no links to place them, so we park each one next to its own
Content group and draw it as a hollow ring.

### 8. A fourth cut, the book's own chapters

The IOAA problem book sorts the same problems into 14 chapters of its own, which
is an editor's reading of the material rather than the syllabus's. Every exam
part sits in exactly one chapter, so chapters never share a part and a
part-based graph of them would have no links at all. What they do share is
concepts, 204 of our 337 turn up in more than one chapter. So at this level the
concept does the linking, and a link reads as the share of one chapter's concept
mass that another chapter also examines.

We colour each chapter by the syllabus section it draws on most. That is where
Compact Objects and Gravitational Waves show up as sitting outside the syllabus
altogether.

### 9. We let you filter live

Mark weight adds up across exam parts, so we store every quantity per round and
period cell, then add up whichever cells you leave selected.

> **m(A) = sum of the selected cells**, then **p(B|A) = n(A,B) / m(A)** as before

We never add ratios. We work them out again from those sums each time. That is
why theory on its own, data analysis on its own, or any mixture over any stretch
of years gives you exact numbers rather than an approximation.

## Does the exam follow its own syllabus?

We wanted to know whether links stay inside a syllabus section more often than
chance allows. So we measured the share of link weight whose two ends sit in the
same section, then compared it against 200 rewirings that keep every topic's
degree and shuffle the weights. Rewiring breaks the syllabus structure and
leaves everything else alone.

| | |
|---|---|
| What we measured, links inside one section | 40.4% |
| What rewiring gives | 11.5% ± 1.2% |
| **z** | **24.5** |

If we count the dashed links too we get 35.9% against the same rewired
baseline, so the answer does not hinge on that choice. Newman's assortativity on
section labels agrees at 0.27.

Our Leiden groups agree only weakly with the syllabus sections. That tells you
more about how partition-matching scores behave on overlapping structure than
about the result above, so quote the assortativity and the rewiring test.

## What we found

The exam follows its syllabus much more closely than chance. It strays in one
direction, into relativity, compact objects and gravitational waves, none of
which the syllabus names. Those topics carried 1.4% of marks between 2007 and
2012 and 3.5% between 2019 and 2025.

Reading down the topics that gained and up the ones that lost tells us the same
thing twice. Reading values off a plot gained most, then least-squares fitting.
Naked-eye observation lost most, then visual magnitude estimation. IOAA has
moved marks out of visual observation and into quantitative data analysis.

One caveat sits under all of this. The syllabus changed while we were studying
it. The current version adds a Mathematical Methods and Tools section that
includes basic calculus, where the older text ruled calculus out, so we read
early papers against a document written later.

## What we cannot tell you

- We tagged each part once, by judgement, against a fixed vocabulary.
- When we say untested we mean that no concept in our map points at that
  syllabus topic in your selection. Sometimes that marks a real gap. Sometimes
  it just means one of our concepts covers several syllabus topics at once.
- Marks tell you what examiners rewarded. They do not tell you what students
  found hard.

## Source material

We took the problems and solutions from the [IOAA problem
book](https://github.com/ioanazelko/ioaa-problem-book), which is all rights
reserved. We reproduce none of them here. This repository holds the rendered map
and a data file of syllabus topic names, mark shares and layout positions. We
keep the analysis code in a separate private repository.

We are not affiliated with the IOAA and they have not endorsed this work.
