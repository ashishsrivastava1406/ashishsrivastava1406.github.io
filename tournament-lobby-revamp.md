---
layout: page
permalink: /tournament-lobby-revamp/
title: "Tournament Lobby Revamp"
company: "Flutter Entertainment (Junglee Games)"
role: "Senior Product Manager, Consumer Growth and Platform"
period: "2024 to 2025"
summary: "Rebuilding the tournament lobby on cohort-aware ranking and configurable merchandising, and designing the test that separated what the personalisation actually contributed from what the redesign contributed on its own."
---

## The calls

Six decisions carried this project. The measurement afterwards told me which
of them were right.

- **Instrument the funnel before changing anything visual.** The complaint was
  that the lobby felt dated. The loss was in the sort and category tab logic.
- **Rank by cohort, not by individual.** Less sophisticated than per-player
  ranking, and legible to the operations team who had to configure it under
  time pressure.
- **Put the merchandising logic in operations tooling rather than in the
  client.** Tournament inventory turns over constantly and campaign calendars
  move faster than release trains.
- **Keep featured placements under human control.** A guaranteed-prize series
  launch is a commercial event with a date; no ranking model was going to infer
  that it mattered this Thursday.
- **Restructure the join flow conditional** so the cash path shows when a player
  has no valid ticket and the ticket path shows only when they do.
- **Test it three ways, not two** — full build, redesign only, control — which
  meant the experiment could show the expensive half of my own work was
  unnecessary.

**Scope.** I owned the specification, the segmentation model, the experiment
design and the metric set, and ran the analysis with the product analyst on my
team. Design and engineering were partner teams.

<!-- TODO Ashish: add engineering team size and the design partner's function.
Being precise about what you did not do is what makes the rest credible. -->

**Reading the numbers.** ARPU is average revenue per user. NGR-T is net gaming
revenue from tournaments, negative across every path because guaranteed prize
pools exceed rake. The first experiment read at D21, the second at D7 on a
D4-matured cohort. The first ran on the lowest-value player segment only, and
the second had a treatment group roughly a tenth the size of control. Both are
real limits on how far these results generalise.

## The situation

Every session that ends with a player at a table starts with someone looking at
the lobby. That list was identical for everyone: registered tournaments first,
then highlighted ones, then open-for-registration by start time, then closed,
completed, cancelled. Chronological and sensible, and the same for a regular who
plays the same three tournaments every evening as for someone who has never
entered one.

Writing the specification, we separated players four ways: deep tournament
history and clear preferences; thin history and visible confusion about entry
fees, prize structures and the jargon; entirely new to the platform; and a large
group of committed cash-game players with almost no tournament affinity.

One order, four different jobs to be done.

![Lobby wireframes showing four different segment layouts side by side]({{ site.baseurl }}/segment-wireframes.png)

*The same surface specified four ways. A new player gets a learn-how-to-play
prompt where a series player gets a leaderboard opt-in. The structure holds;
the ordering and the prompts change.*

## The constraint

A lobby is a ranking surface wearing the costume of a landing page, and it can
only be in one order at a time.

Three things made it harder than ranking usually is. Inventory is perishable, so
a recommendation that was right ten minutes ago points at something the player
can no longer join. The economics differ by tournament, so promoting what
players most want is not the same as filling what the business most needs
filled. And tournaments compete with ring games inside the same app, which means
every player moved into one may be a player moved out of something else.

## Building the merchandising into operations tooling

This was the structural decision and the one I would defend hardest.

A bundle became a first-class entity in the admin: featured bundles pinned to the
top of the lobby, tab bundles in a horizontal strip below. Tournament templates
map to bundles. A rules engine decides, per segment and inside a time window,
which bundles appear and in what order, with real-time segments fed from the
audience platform. No rule for a template and it falls back to the default sort.

The alternative was building the ranking into the client. That would have been
faster to ship once and slower every time afterwards. Operations needed to change
the lobby on the day of a series launch, not in the next release.

## What I turned down

**Per-player personalisation.** The more sophisticated answer, and I did not
build it. Cohorts were legible to the people configuring them, degraded
gracefully for players with no history, and fit the release window.

**A visual redesign on its own.** Faster to ship, easier to sell internally, and
it would have left the sort order untouched. What the test later found does not
change that reasoning, though it does complicate it.

**Letting the rules engine own the whole surface.** Featured placements stayed
manual for commercial reasons.

<!-- TODO Ashish: was there a fourth? The spec raised the custom tab cap from 10
to 20 to cover more segments. If there was an argument about how many segments
operations could realistically maintain, that is the governance question every
rules engine eventually meets, and worth a paragraph. -->

## Designing the test so it could fail

We ran three paths rather than two.

- **Path 1** — the full build: revamped lobby, featured cards, bundles, segment
  rules
- **Path 2** — the same card redesign and join flow, featured cards removed
- **Control** — the existing lobby

Path 2 exists because someone asked what the featured card was worth on its own.
Adding it meant the experiment could return a result that made half my build
redundant. It did.

![Control, Path 1 and Path 2 side by side on device]({{ site.baseurl }}/ab-variants.png)

*Left to right: control, Path 1 with featured cards, Path 2 with the card
redesign only. Player identifiers and balances redacted.*

## What the first test showed

Three weeks of exposure, read at D21.

**Both paths lifted ARPU by about seven percent, and were indistinguishable from
each other.** The bundles, the rules engine and the segment configuration added
nothing to the primary business metric that the card redesign had not already
delivered.

Underneath, the two behaved differently. Path 1 pushed tournament wager per user
up sharply and cut browsing hard, with clicks into tabs and filters falling by
over five points against control versus one point for Path 2. The featured card
did what it was designed to do: players stopped hunting.

But Path 1's ring-game rake per user fell while Path 2's rose, average cash games
played fell in Path 1 and rose in Path 2, and tournament NGR per user improved
far more in Path 2. My reading is that the featured card moved players into
tournaments partly by moving them out of ring games and into the more subsidised
product — the same ARPU, a worse mix. That reading is mine, not something the
analysis stated, and the next experiment pushed the opposite way, so I hold it
loosely.

**Volume fell while value rose.** Average tournaments played dropped in both
paths, most in Path 1, while wager per tournament rose. Personalisation did not
make people more active. It improved the match between player and tournament.

**The smallest change was among the largest wins.** The join flow conditional
lifted ticket purchase success by seventeen points and cash join-click-to-success
by over three. No personalisation involved.

**What went wrong.** Withdraw success fell materially in both paths and free
withdraw attempts rose. Players were trying to back out more often and succeeding
less. Registration is a commitment with money attached, and if the exit gets
harder while the entry gets easier, part of the gain is friction rather than
preference. Fewer people clicked into the lobby at all in either path — we
improved the room without improving the door.

<!-- TODO Ashish: was the withdraw regression diagnosed afterwards? If Phase 2
fixed it, say so. Closing that loop is worth more than the metric that opened
it. -->

## Isolating the bundles

The first test never measured the bundles on their own, so we ran them
separately: three bundles above the tournament list — Quick Start for low entry
fees and short formats, Highrollers, and Win 10X.

![The shipped bundle strip: Quick Start, Highrollers and Win 10X]({{ site.baseurl }}/bundles-live.png)

*The shipped bundle strip. Quick Start drew the least attention of the three and
produced the most completed registrations.*

**The bundle players clicked most produced the least play.** Win 10X pulled the
most traffic and converted around one registration for every twenty clicks.
Quick Start pulled less traffic and converted more than half its clicks.
Highrollers was worst on both counts, and of the players who clicked join inside
it, roughly one in ten completed.

Aspiration wins the click. Accessibility wins the play. Highrollers shows where
the gap becomes a wall: a player who clicks join and cannot register has not
failed to discover the tournament, they have failed to afford it. No amount of
better ordering fixes that.

**The headline and the mechanism did not match.** ARPU rose about two and a half
percent, but only around one percent of registrations came through the bundle
tab, and ring-game rake rose more than tournament rake. With a treatment group a
tenth the size of control, some of that is noise. A two and a half percent result
that cannot explain its own mechanism is weaker than it looks, and I would rather
say so than quote the number on its own.

**One merchandising decision was made by omission.** Cash tournament join clicks
rose by about three quarters of a point and free tournament join clicks fell by
almost the same amount, because no free tournaments had been mapped into any
bundle. Nobody decided to push the audience toward paid play. It followed from
what got mapped, and mapping was an operational task rather than a reviewed one.

That is the cost of the structural decision I made earlier. Configuration is
faster than a release, and it is also easier to do without anyone reviewing the
strategy behind it.

**The guardrail.** Platform retention dipped a little over a point at D3 and D4
in the matured cohort. Not statistically significant, but the same direction two
days running. The recommendation was to scale up while monitoring it, which I
think was right — though a retention dip you have decided to watch is an accepted
risk, not an absent one, and should be recorded that way.

<!-- TODO Ashish: what happened after scale-up? Whether the D4 dip resolved, and
whether free tournaments were later mapped into bundles, is the ending this case
study needs. -->

## What I would do differently

**Test the expensive component earlier.** Path 2 was the right idea at the wrong
time. Shipping the card redesign and join flow as their own release first would
have established the baseline before engineering committed to a rules engine, and
the decision about bundles would have been made knowing what they had to beat.

**Instrument the substitution, not just the surface.** Every success metric in
the specification pointed at tournaments. None pointed at what a player stopped
doing in order to play one. The cannibalisation was only visible because ring
rake happened to sit on the guardrail list. Inside an app with competing
products, cross-product substitution belongs in the primary metric set.

**Rank on what a player can complete.** The bundle results are the clearest
lesson here. A surface optimised for clicks and one optimised for completed
actions are different surfaces, and where entry costs money the difference is
affordability. I would build the eligibility signal into the ranking rather than
leaving the join flow to reject people at the end.

**Make mapping a reviewed decision.** Tooling that lets operations change
merchandising without a release also lets them change it without a discussion.

---

<!-- TODO Ashish, before publishing:
1. Check whether the Path 1 variant actually shipped. Showing the live app is one
   thing; publishing an unshipped variant is a different disclosure.
2. Never paste reviewer names, the Jira epic ID, or Figma and Drive links into
   any file in this repository. -->

*Figures normalised. No absolute business metrics from a current or former
employer appear on this site.*
