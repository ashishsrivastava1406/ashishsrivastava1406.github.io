---
layout: page
permalink: /recommendations/
published: false   # <-- change to true when this one is ready
title: "Recommendations — a ranked list is not a recommendation"
company: "Flutter Entertainment (Junglee Games)"
period: ""
role: "Senior Product Manager, Consumer Growth and Platform"
summary: "Building a recommendation engine across the conversion funnel. Double digit lift in checkout success, a step change in purchases per user, high single digit revenue per user at D7."
---

## The situation

The lobby rebuild fixed the order of a shared list. This was the next question:
what should we put in front of *this* player, right now, that is not simply the
best row in a list everyone sees.

<!-- TODO Ashish: where in the funnel did the engine actually sit? Your resume
says "across the conversion funnel", which is vague on purpose in a resume but
too vague here. Which surfaces got recommendations — lobby, post-game, entry
flow, all of them? -->

## The constraint

Recommendation quality depends on interaction history, and the players who
most need help choosing are the ones with the least history. Cold start is not
an edge case here — it is the segment where the recommendation matters most
and works worst.

<!-- TODO Ashish: was cold start actually the binding constraint, or was it
something else — inventory churn as tournaments start and end, latency budget
on the lobby, no offline evaluation set to test against? Replace this if I've
picked the wrong one. -->

## What I decided

<!-- TODO Ashish: state the call in one or two sentences before the reasoning.
What did the engine optimise for, and what did you consciously decide not to
optimise for? A recommender pointed at immediate conversion and one pointed at
retention produce different products, and the choice between them is the
decision worth writing about. -->

## What I rejected and why

<!-- TODO Ashish: candidates — popularity ranking as a baseline you had to beat
and why it was harder to beat than expected; personalising on affinity versus
on value; letting the engine control the whole surface versus reserving slots
for commercial pinning. -->

## How it played out

Checkout success rose by a double digit margin. Purchases per user showed a
step change. Revenue per user was up high single digits at D7.

The D7 framing matters and is worth saying explicitly: a recommender can lift
immediate conversion while shortening the relationship, so measuring at D7
rather than at the session was a deliberate choice about what counts as
success.

<!-- TODO Ashish: confirm that framing is true to how you actually set the
metric. If D7 was inherited rather than chosen, say so instead — inheriting a
metric and then arguing to change it is also a story. -->

## What I'd do differently

<!-- TODO Ashish: your call. -->

---

*Figures normalised — no absolute business metrics from a current or former
employer appear on this site.*
