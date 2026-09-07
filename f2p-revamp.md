---
layout: page
published: false   # change to true when this one is ready
permalink: /f2p-revamp/
title: "F2P Revamp"
company: "Flutter Entertainment (Junglee Games)"
role: "Senior Product Manager, Consumer Growth and Platform"
period: ""
summary: "Selecting and sequencing four monetisation models under a regulatory constraint, after a national ban removed the existing revenue."
---


## The situation

Junglee Games ran on real money gaming. Players deposited, played, withdrew,
and the business took a rake. Every product surface I owned — the lobby,
the tournament catalog, pricing, promotions — existed to serve that model.

Then India banned it. The revenue model did not shrink. It became illegal.

<!-- TODO Ashish: one line on the timeline. How long between the ban taking
effect and the first replacement model shipping? The compression is the story. -->

## The constraint

Three things were true at once, and they pulled against each other.

The first was legal. Anything we shipped had to be defensibly outside the
definition of the thing that had just been banned, and that definition was
being interpreted in real time. Legal and policy were not a review gate at the
end. They were in the room for the design decisions.

The second was that we still had the users. People kept opening the app. The
audience had not gone anywhere — only the way we earned from them had. That
made this a monetisation problem rather than a survival problem, which sounds
easier and is actually harder, because it removes the excuse for shipping
something bad quickly.

The third was that the players' relationship with the product had been
financial. Stake, risk, reward. Any replacement had to give people a reason to
come back that was not the reason they used to come back.

## What I decided

Ship four monetisation models rather than one, and sequence them so that the
cheapest to build ran first and funded the patience for the one that mattered
most.

The four: virtual currency, rewarded advertising, in app purchases, and the
platform's first subscription.

## What I rejected and why

**Betting everything on advertising.** It was the fastest path to non-zero
revenue and the least legally exposed. It was also a ceiling. Ad revenue per
user in this category would not have replaced what we lost, and building the
org around it would have made the harder work politically impossible later.
Rewarded ads stayed, but as one model of four rather than the model.

<!-- TODO Ashish: was there internal pressure to do exactly this? If someone
senior argued for the ads-only path and you argued them out of it, say so.
That is the single most valuable paragraph you could add to this site. -->

**Launching the subscription first.** Subscription was the model I believed in
most, because it converts a transactional relationship into a recurring one,
which was precisely the relationship we had just lost. It was also the one
most likely to fail if we launched it into an audience that had no habit yet.
Selling a recurring commitment to users who were still deciding whether to open
the app at all is a bad trade. It went last, deliberately.

**Rebuilding the same loops with virtual currency alone.** The tempting move
was a near-identical product with a non-cash currency swapped in. It would have
preserved the existing design, the existing funnels, the existing everything.
We used virtual currency, but not as a cash substitute in the old loops,
because the old loops were built on financial stakes and the new currency
carried none. Reusing the mechanics without the stake produces a product that
looks like the old one and feels hollow.

<!-- TODO Ashish: check this last one. If the actual reasoning was different,
replace it — I inferred it from how you described the rebuild. -->

## How it played out

The share of people opening the app who became active users went from under
half to roughly three quarters.

That is the number I care about from this project, and it is worth being clear
about why, because it is not a revenue number. Revenue after a ban is a
function of how much of the audience you keep. Activation was the leading
indicator, and it moved before the monetisation did.

<!-- TODO Ashish: what went wrong? Which of the four underperformed, or shipped
late, or needed rebuilding? A case study with no failure in it reads as
marketing. -->

## What I'd do differently

<!-- TODO Ashish: your call, not mine. One candidate, if it's true: sequencing
by build cost was the right instinct under time pressure, but it meant the
subscription — the model most likely to change the business — got the least
runway and the least learning time. Would you sequence by strategic weight
instead, and eat the slower start? -->

---

*Figures normalised — no absolute business metrics from a current or former
employer appear on this site.*
