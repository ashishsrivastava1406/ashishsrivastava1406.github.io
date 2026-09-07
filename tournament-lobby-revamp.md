---
layout: page
permalink: /tournament-lobby-revamp/
title: "Tournament Lobby Revamp — the expensive half didn't earn its place"
company: "Flutter Entertainment (Junglee Games)"
period: "2024–2025"
role: "Senior Product Manager, Consumer Growth and Platform"
summary: "We built cohort personalisation into the tournament lobby, then ran two experiments to find out which parts of it were actually doing the work. The answers were not the ones I expected, and the most useful one came from a bundle that everybody clicked and nobody played."
---

## In one minute

- The tournament lobby showed every player the same list in the same order. We
  rebuilt it on cohort-aware ranking, configurable bundles and a redesigned
  card, with the merchandising logic in operations tooling rather than in the
  client.
- I ran it as a **three-path test** — full build, card redesign only, control —
  which meant the experiment could show the expensive half of my own build was
  unnecessary. It did: both paths lifted ARPU by about seven percent, and were
  indistinguishable from each other.
- A second experiment isolated the bundles. The bundle that drew the most
  attention converted worst; the one built around low entry fees and short
  formats converted more than half its clicks. **Attention and completion point
  in opposite directions when entry costs money.**
- Both experiments moved players between products inside the app. Neither had
  that movement as a primary metric. That is the mistake I'd fix first.

**Scope.** I owned the spec, the segmentation model, the experiment design and
the metric set, and I ran the analysis with the product analyst on my team.
Design and engineering were partner teams.
<!-- TODO Ashish: add engineering team size and the design partner's function
(not their name). Precision about what you did *not* do is what makes the rest
credible. -->

**Reading the numbers.** ARPU is average revenue per user. NGR-T is net gaming
revenue from tournaments, negative across all paths because guaranteed prize
pools exceed rake. Phase 1 read at D21, Phase 2 at D7 on a D4-matured cohort.
Phase 1 ran on the lowest-value player segment only, and Phase 2's treatment
group was roughly a tenth the size of control — both are real limits on how far
these results generalise.

---

## The situation

The tournament lobby is the front door. Every session that ends with a player
sitting at a table starts with someone looking at a list.

That list was the same for everyone. Tournaments within a tab appeared in one
fixed order — registered first, then highlighted, then open-for-registration by
start time, then closed, completed, cancelled. Sensible, chronological, and
identical whether you were a regular who plays the same three tournaments every
evening or someone who had never entered one.

The players were not identical. Writing the spec, we separated them four ways:
players with deep tournament history who knew exactly what they wanted; players
with thin history who found the format confusing — entry fees, prize pool
structures, the jargon; players entirely new to the platform; and a large group
of committed cash-game players with almost no tournament affinity at all.

One order, four very different jobs to be done.

![Lobby wireframes showing four different segment layouts side by side]({{ site.baseurl }}/segment-wireframes.png)

*The same surface, specified four ways. A new player gets a learn-how-to-play
prompt where a series player gets a leaderboard opt-in. The structure is
identical; only the ordering and the prompts change.*

## The constraint

A lobby is a ranking surface wearing the costume of a landing page, and it can
only be in one order at a time.

Three things made this harder than a ranking problem usually is.

The inventory is perishable. Tournaments start, fill, close and end. A
recommendation that was right ten minutes ago points at something the player
can no longer join. Whatever we built had to reason about time, not just fit.

The economics differ by tournament. Guaranteed prize pools mean some
tournaments run at a loss to the business — across every path in the eventual
test, tournament NGR per user was negative. Promoting the tournaments players
most want is not automatically the same as promoting the tournaments the
business most needs filled, and any ranking system has to hold both.

And tournaments compete with ring games inside the same app. Every player moved
into a tournament is a player possibly moved out of something else. This one
turned out to matter more than I expected, and I will come back to it.

## What I decided

Build the personalisation into configurable operations tooling rather than into
the client.

Concretely: a bundle became a first-class entity in the admin. Two kinds —
featured bundles pinned to the top of the lobby, and tab bundles in a
horizontal strip below them. Tournament templates map to bundles. A rules
engine then decides, per segment and within a time window, which bundles appear
and in what order, with real-time segments fed in from the audience platform.
No rule for a template, and it falls back to the default sort.

The reason for putting the intelligence in admin rather than in code is that
tournament inventory turns over constantly and marketing calendars move faster
than release trains. A merchandising decision that requires an app release is a
merchandising decision that arrives late. Operations needed to change the lobby
on the day of a series launch, not in the next sprint.

Alongside it: a full tournament card redesign, a filter and sort system across
entry fee, format, prize pool, status, start time and duration, and one small
change to the join flow — show the cash path when the player has no valid
ticket, show the ticket path only when they have a ticket or a ticket sale is
running.

## What I rejected and why

**Per-player personalisation instead of cohort rules.** True per-player ranking
was the more sophisticated answer and I did not build it. Cohorts were legible
to the operations team who had to configure and debug them, they degraded
gracefully for players with no history — exactly the segment we most needed to
help — and they could ship inside the release window. Cohort ranking is the
version an operator can reason about at four in the afternoon before a big
series.

**A visual redesign alone.** The presenting complaint was that the lobby felt
dated. Instrumenting the funnel first put the loss in the sort and category tab
logic, not in how the rows looked. Redesigning would have shipped faster and
left the actual problem untouched.

The irony of what the test later found is not lost on me. More below.

**Letting the rules engine own the whole surface.** Featured slots stayed under
human control, because a guaranteed-prize series launch is a commercial event
with a date, and no ranking model was going to infer that it mattered this
Thursday.

<!-- TODO Ashish: was there a fourth? The PRD raised the custom-tab cap from 10
to 20 to cover more segments. If there was an argument about segment
proliferation — how many segments operations could actually maintain before the
config became unmanageable — that is worth a paragraph. It is the governance
question every rules engine eventually runs into. -->

## How it played out

We ran it three ways rather than two, which turned out to be the most
consequential decision in the project.

- **Path 1** — the full build: revamped lobby with featured cards, bundles and
  segment rules
- **Path 2** — the same card redesign and join flow, featured cards removed
- **Control** — the existing lobby

![Control, Path 1 and Path 2 side by side on device]({{ site.baseurl }}/ab-variants.png)

*Left to right: control, Path 1 with featured cards, Path 2 with the card
redesign only. Player identifiers and balances redacted.*

Three weeks of exposure, read at D21.

**The headline: both paths lifted ARPU by roughly seven percent, and they were
indistinguishable from each other.** The expensive half of the build — bundles,
the rules engine, the segment configuration — added nothing to the primary
business metric that the card redesign alone had not already delivered.

That is not the result I expected, and it is the most useful thing the test
produced.

**Underneath, the two paths behaved very differently.** Path 1 pushed tournament
wager per user up sharply, well ahead of Path 2, and tournament rake per user
rose more. It also cut browsing hard: clicks into tabs and filters fell by over
five points against control, versus one point for Path 2. The featured card did
precisely what it was designed to do — players stopped hunting, because what
they wanted was already in front of them.

But Path 1's ring-game rake per user went *down* while Path 2's went up, and
average cash games played fell in Path 1 and rose in Path 2. Tournament NGR per
user, negative everywhere because of guaranteed prize pools, improved far more
in Path 2 than in Path 1.

Put together, the reading I came to is that **the featured card moved players
into tournaments substantially by moving them out of ring games, and into the
more heavily subsidised product.** Same ARPU, worse mix. It moved money around
rather than creating it.

That effect belongs to the featured card specifically, not to personalisation
in general. The next experiment showed the opposite sign, which is why I am
careful about the claim.

<!-- TODO Ashish: this is my reading of the NGR-T and ring rake numbers, not
something the analysis states outright. Confirm or correct it. -->

**Volume fell while value rose.** Average tournaments played dropped in both
paths, most in Path 1, while wager per tournament rose. Players played fewer,
larger tournaments. Personalisation did not make people more active. It made
the match between player and tournament better.

**The smallest change was among the largest wins.** The join-flow logic — cash
when there is no valid ticket, ticket only when there is one — lifted ticket
purchase success by seventeen points and cash join-click-to-success by over
three. A conditional in an entry flow, no personalisation involved.

**What went wrong.** Withdraw success fell materially in both paths, and free
withdraw *attempts* rose. Players were trying to back out of tournaments more
often and succeeding less. Registration is a commitment with money attached,
and if the exit gets harder while the entry gets easier, some of the gain is not
a gain — it is friction the player did not choose.

Fewer people clicked into the tournament lobby at all in either path. We
improved the room without improving the door.

<!-- TODO Ashish: was the withdraw regression diagnosed afterwards? A design
issue in the new card, or a real flow break? If Phase 2 fixed it, say so —
closing that loop is worth more than the metric that opened it. -->

## Then we isolated the bundles

Phase 1 told us the featured card did not beat the card redesign on ARPU. It
did not tell us what the bundles were worth, because they had never been tested
on their own. So we ran them separately: three bundles in a strip above the
tournament list — Quick Start, for low entry fees and short formats;
Highrollers; and Win 10X.

![The shipped bundle strip: Quick Start, Highrollers and Win 10X]({{ site.baseurl }}/bundles-live.png)

*The shipped bundle strip. Quick Start drew the fewest of the three on
attention and the most on completed registrations; Win 10X the reverse.*

Read at D7.

**The finding I did not expect was that the bundle players clicked most was the
bundle that produced the least play.** Win 10X pulled the most traffic of the
three and converted worst — around one registration for every twenty clicks.
Quick Start pulled less traffic and converted more than half of its clicks into
registrations. Highrollers was worst on both counts: it drew the fewest clicks,
and of the people who clicked join inside it, only about one in ten completed.

Aspiration wins the click. Accessibility wins the play. And Highrollers shows
where the gap becomes a wall — a player who clicks join and then cannot register
has not failed to discover the tournament, they have failed to afford it. That
is not a ranking problem and no amount of better ordering fixes it.

**The headline number and the mechanism did not match.** ARPU rose about two and
a half percent. But only around one percent of all registrations came through
the bundle tab at all, and ring-game rake rose more than tournament rake did. In
an experiment on a tournament surface, most of the ARPU movement was sitting
somewhere the feature does not touch. With a treatment group roughly a tenth the
size of control, some of that is noise. Some of it may be a real indirect
effect. I do not think the data settles which, and a two-and-a-half percent
headline that cannot explain itself is a weaker result than it looks.

**One merchandising decision was made by omission.** Cash tournament join clicks
rose by about three quarters of a point and free tournament join clicks fell by
almost exactly the same amount. The reason was simple: no free tournaments had
been mapped into any bundle. Nobody decided to push the audience toward paid
play. It happened because of what got mapped, and the mapping was an
operational task rather than a strategic one.

That is the risk of putting merchandising into configurable tooling, and it is
the flip side of the argument I made for building it that way. Configuration is
faster than a release, and it is also easier to do without anyone reviewing the
strategy behind it.

**The Phase 1 pattern repeated.** Average tournaments played per user fell
slightly again while value per user rose. Join-click-to-success fell again,
cash more than free — the same signature as Phase 1, intent up and completion
down, consistent with pushing players toward tournaments they cannot finish
entering.

**And the guardrail.** Platform retention dipped by a little over a point at
D3 and D4 in the matured cohort. Not statistically significant, but pointed the
same direction two days running. The recommendation was to scale up while
continuing to watch it, which I think was right — but a retention dip you have
decided to monitor is a decision to accept risk, not an absence of one, and it
should be written down as such.

<!-- TODO Ashish: what happened after scale-up? If the D4 dip resolved, or
didn't, that is the ending this case study needs. If free tournaments were
mapped into bundles afterwards and the mix shift reversed, say so. -->

## What I'd do differently

**Test the expensive component against nothing much earlier.** Path 2 existed
because someone asked what the featured card was actually worth. That question
arrived after the build, not before it. Had we shipped the card redesign and
join flow as their own release first, we would have known the baseline lift
before committing engineering to a rules engine — and we would have decided on
bundles knowing what they had to beat.

**Instrument the substitution, not just the surface.** Every success metric in
the spec — join rate, conversion, ARPU — pointed at tournaments. None pointed at
what a player stopped doing in order to play one. The cannibalisation was only
visible because ring rake happened to sit on the guardrail list. Inside an app
with competing products, cross-product substitution belongs in the primary
metric set, not the guardrails.

**Treat the exit as part of the flow.** The join path got attention at the level
of individual conditionals. The withdraw path got none, and it regressed.

**Rank by what a player can complete, not by what they will look at.** The
bundle results are the cleanest lesson in the project. A surface optimised for
clicks and a surface optimised for completed actions are different surfaces, and
on a product where entry costs money, the difference is affordability. I would
now build the eligibility signal — can this player actually enter this
tournament right now — into the ranking itself rather than leaving it to the
join flow to reject them.

**Make mapping a reviewed decision.** The free-versus-cash mix shifted because
of what was mapped into bundles, and nobody signed off on that as strategy.
Tooling that lets operations change merchandising without a release also lets
it change merchandising without a discussion. Both experiments moved the mix
between products, and neither had the mix as a primary metric.

---

<!-- TODO Ashish, before publishing:
1. Check whether the Path 1 variant actually shipped. Showing the live app is
   one thing; publishing an unshipped variant is a different disclosure.
2. Never paste reviewer names, the Jira epic ID, or Figma and Drive links into
   any file in this repo. -->

*Figures normalised — no absolute business metrics from a current or former
employer appear on this site.*
