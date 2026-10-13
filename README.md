<!-- solve-problem:7d4ef174-25cf-498a-a281-7a2fd7de4615 -->
# Generalized star height greater than one

A [Tangle Solve problem](https://solve.tangle.tools/problems/7d4ef174-25cf-498a-a281-7a2fd7de4615).

## What is the problem?

The **generalized star height** of a regular language L is the minimum nesting depth of Kleene stars required to express L by a **generalized regular expression** — one built from letters, ∪ (union), · (concatenation), and **complement** (over some universe), with no other operators. Crucially, when complement is available, union and concatenation can themselves be simulated (e.g., K ∪ L = ¬(¬K · ¬L) up to ε handling), so the measure is usually formalized as the star-nesting depth in expressions over {·, ∪, ¬, *}. Languages of generalized star height 0 are exactly the **star-free languages** (equivalently, those definable in FO[<] over words, by McNaughton–Papert/Schützenberger's aperiodicity theorem).

The open problem: **Does there exist a regular language of generalized star height ≥ 2?** Either exhibit one, or prove every regular language has generalized star height ≤ 1. Every regular language trivially has finite generalized star height ≤ its ordinary star height. The subtlety is that complement can drastically reduce needed star nesting — e.g., (ab)* has ordinary star height 1 but is not star-free... while ¬((a+b)*...) manipulations can sometimes eliminate stars entirely (as in the classic ¬∅ = Σ* trick, showing Σ* is star-free despite needing a star without complement).

## Why does it matter?

This is one of the oldest open problems in automata theory (open since the early 1960s, Brzozowski-era). It measures the true descriptive complexity of regular languages when negation is free — directly relevant to succinctness of logic/regex formalisms used in verification and query languages. A separation would establish an infinite (or at least nontrivial) hierarchy, giving lower-bound machinery for regular-expression and temporal-logic description sizes; a collapse-to-one theorem would be equally striking, implying complement is an almost-universal star-eliminator.

## What's already known?

- **Star-free = aperiodic = FO[<]** (Schützenberger 1965; McNaughton–Papert 1971): generalized star height 0 is decidable and well understood.
- The analogous problem *without* complement — ordinary star height — was **solved**: Eggan (1963) defined it, and Hashiguchi (1988) proved star height is decidable via his decidability of the finite-substitution/`-limitedness problem for distance automata; De Schutter and later Lenčo/Shallit simplified parts.
- **Level 1 = star-free** and the problem reduces essentially to separating "height exactly 1" from "height ≥ 2" — but no candidate separating the levels is known.
- **Pin (1992)** surveys the problem: the generalized star height hierarchy is known only at level 0; there is no known regular language provably of height > 1, and no proof of collapse. Pin–Weil-style work on the dot-depth hierarchy (the analogous hierarchy measuring alternation of · and ¬) is related but does not resolve star nesting.
- A notable result often cited: every regular language can be written with **one** star if complement is allowed in certain restricted positions? — no; in fact the strongest known statement is that the problem is open even for a single candidate language. Some progress exists for languages over **one-letter alphabets** (star height collapses there (verify)).

## What would count as solving it?

1. **Separation:** A specific regular language L (given, e.g., by a DFA or ordinary expression) plus a proof that L cannot be expressed by any generalized regular expression of star-nesting depth ≤ 1. A referee would want a rigorous invariance argument (e.g., an algebraic characterization of height-≤-1 languages refuted by L).
2. **Collapse:** A proof that every regular language has generalized star height ≤ 1, i.e., an effective rewriting of arbitrary regular expressions into depth-1 generalized expressions.
3. **Weaker but valuable:** decidability of generalized star height 1, or an algebraic characterization (in terms of finite monoids/syntactic morphisms) of the height-≤-1 class.

## How to start

1. Read Pin (1992) first — it is the survey of record and frames all known partial results and the algebraic viewpoint.
2. Study why ordinary star height succumbed: Hashiguchi's reduction to distance-automata limitedness (via Leiss's or Simjonowitsch's expositions, or Sakarovitch's framework of "ratios of transductions"). Ask: where does the technique break when complement enters?
3. Try the algebraic route: star-free ↔ aperiodic monoids. Seek a monoid-theoretic invariant preserved by depth-1 generalized expressions, and hunt for a syntactic monoid violating it — natural candidates are languages whose ordinary star height is high and whose aperiodic "closures" behave badly.
4. Main obstacle: complement makes expression-to-automata translations wildly non-well-founded — no known normal form bounds the search space; unlike ordinary star height, there is no known decidability even for the level-1 question.

## Key references

- J.-É. Pin, *Some results on the generalized star-height problem*, 1992. HAL: hal-00019978. Survey defining the problem and collecting all partial results known as of the early 90s.
- M. P. Schützenberger, "On finite monoids having only trivial subgroups" (1965): aperiodicity characterizes star-free languages — the level-0 base case.
- K. Hashiguchi, "Algorithms for determining relative star height and star height" (1988): decides ordinary star height via limitedness — the model of a successful attack to compare against.
- L. Eggan (1963), "Transition graphs and the star height of regular events": defines star height and initiates the hierarchy program.
- J. Sakarovitch, *Elements of Automata Theory* (2009), chapters on star height and limitedness: modern unified treatment of the non-complement case.

## Warnings

- Do not confuse generalized star height with **dot-depth**; they are different hierarchies, and results on one don't transfer.
- Complement changes the game entirely: naive tricks like "push stars through negation" fail; e.g., ¬L* is not of the form (something)*.
- The empty/universal-language edge cases (Σ* is star-free via double negation of ∅) trip up informal arguments — fix a precise syntax and universe first.
- Beware of folklore claims that the problem was solved; no accepted solution exists — verify any claimed breakthrough against Pin's survey and the current literature.

---
*`ALGO-000176` · unverified*

## Acceptance guidance

1. **Separation:** A specific regular language L (given, e.g., by a DFA or ordinary expression) plus a proof that L cannot be expressed by any generalized regular expression of star-nesting depth ≤ 1. A referee would want a rigorous invariance argument (e.g., an algebraic characterization of height-≤-1 languages refuted by L).
2. **Collapse:** A proof that every regular language has generalized star height ≤ 1, i.e., an effective rewriting of arbitrary regular expressions into depth-1 generalized expressions.
3. **Weaker but valuable:** decidability of generalized star height 1, or an algebraic characterization (in terms of finite monoids/syntactic morphisms) of the height-≤-1 class.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/7d4ef174-25cf-498a-a281-7a2fd7de4615?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000176.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000176)
