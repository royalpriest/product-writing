# Proposal: Friend Mode, Recommending Movies Two People Will Both Accept

**Product:** SaintFlick, an AI-assisted movie discovery app ([saintflick.com](https://saintflick.com))
**Type:** Feature proposal
**Status:** Shipped, then refined through follow-up passes (see "What happened next")

> Adapted from SaintFlick's internal design docs for public reading. How the system works under the hood has been left out; this covers the problem, the product rules and how success was judged.

## Problem

Choosing a movie with someone else is a negotiation. One person wants science fiction, the other wants something warm and funny, and one of them has a firm rule like "no horror."

A naive approach fails in predictable ways. It either:

- alternates between "your pick" and "my pick" instead of finding overlap
- averages away one person's explicit "no," so one person's enthusiasm outvotes the other's veto
- treats one person's preference as mandatory, creating impossible requests (one asks for horror, the other says no horror)
- favours a lopsided pick (great for one person, mediocre for the other) over a balanced pick both people like, because the average looks higher

## Goal

Recommend movies that **both** people can reasonably accept, without ever overriding anyone's "no."

## Product rules

**1. A "no" from either person is a "no" for both.**

```text
Person 1: no horror
Person 2: tense mystery
→ no horror in the shared results
```

**2. Preferences shape the results but never block them.** What each person *wants* is weighed, but no single preference becomes a requirement. That avoids deadlocks:

```text
Person 1: horror
Person 2: no horror
→ Person 2's "no" holds; Person 1's interest only counts where it's compatible
```

**3. Vetoes are never relaxed to fill the list.** Fewer good results beat more results that break someone's rule.

**4. Balanced beats lopsided.** Results favour movies that work well for *both* people, judged by how well the less-satisfied person is served, not by the average.

```text
Balanced:  both people like it a lot           → shown first
Lopsided:  one loves it, the other is lukewarm → shown later, even if the average is higher
```

**5. Stay fast and affordable.** Response time and running cost are tracked as product requirements, not afterthoughts.

## How success is measured

A dedicated test set of two-person scenarios covers complementary tastes, explicit vetoes, genre conflicts, pacing conflicts, difficult mixed requests and unusual combinations (dark-but-funny, gentle sci-fi, weird-but-romantic).

Each run checks:

- how well the results suit each person, and how balanced they are
- whether any veto slipped through
- how often a request returns no results
- how many good recommendations come back
- response time and running cost
- a human review of whether the picks genuinely suit both people

## What happened next

The first version worked, but follow-up passes refined it, each written up the same way:

- **A rejected experiment.** The first test run showed one pair getting almost nothing back: "dark but not depressing" plus "romantic and warm, not cheesy" left a single movie. My first fix was to give the AI much more detailed instructions. Measured against the same tests, it didn't solve that case and made responses slower and costlier, so I replaced it. The write-up was kept rather than deleted, so the reasoning stays visible.
- **The fix that worked: treat "not too…" differently from "no."** "Not depressing" is a matter of degree, not a hard ban like "no horror." Distinguishing the two fixed the over-filtering.
- **An efficiency pass.** Response time and cost were cut further, with a firm rule: if a speed or cost gain made recommendations worse, quality won.
