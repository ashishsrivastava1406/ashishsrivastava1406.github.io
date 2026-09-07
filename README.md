# ashishsrivastava1406.github.io

Product case studies. Decisions, alternatives considered, and what the
measurement showed.

Live at **https://ashishsrivastava1406.github.io**

## What this is for

Evidence of product judgement, aimed at hiring managers. Each case study leads
with the decisions taken and treats the measurement as the check on them, rather
than working backwards from data to a narrative.

## Files

Everything sits at the root except `_layouts`. GitHub's web uploader cannot
select folders from the macOS file picker, so upload by dragging from Finder,
not by using "choose your files".

- `index.html` — homepage. The headline and standfirst live in its front matter.
- `tournament-lobby-revamp.md` — the published case study.
- `f2p-revamp.md`, `recommendations.md`, `tournament-ingress.md`,
  `zombie-perception.md` — drafts, each `published: false`.
- `case-study-template.md` — the shape every case study follows.
- `_layouts/` — `default.html` holds all the styling; `home.html` and
  `page.html` build the dark header band.
- `*.png` — redacted screenshots.
- `_config.yml`, `404.md`, `DISCLOSURE.md`.

## Publishing a draft

Open the file, change `published: false` to `published: true`, commit. Then add
a matching entry on the homepage and remove the `draft` class from its row.

## Writing a new one

Copy `case-study-template.md`. The first section is the decisions. If a line
does not name something chosen over something else, it is a task rather than a
call, and it does not belong there.

## Disclosure

See `DISCLOSURE.md`. Relative movement is safe, absolute business volume is not.
No absolute figures appear anywhere in this repository, including in a resume —
those go to recruiters directly.
