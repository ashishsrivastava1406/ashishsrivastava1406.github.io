# ashishsrivastava1406.github.io

Product case studies. Decisions and trade-offs, not project summaries.

Live at **https://ashishsrivastava1406.github.io**

## How this repo is laid out

Everything sits at the root — no folders. That is deliberate: GitHub's web
uploader cannot select folders from the macOS file picker, so a flat repo means
you can always select all and drag without anything being silently left behind.

- `index.md` — the landing page
- `tournament-lobby-revamp.md` — the one published case study
- `f2p-revamp.md`, `recommendations.md`, `tournament-ingress.md`,
  `zombie-perception.md` — drafts, each marked `published: false` so they do not
  appear on the site yet
- `case-study-template.md` — the shape every case study follows
- `*.png` — redacted screenshots
- `_config.yml` — site settings
- `DISCLOSURE.md` — the rules every file here follows

## Publishing a draft

Open the file, change `published: false` to `published: true`, commit. That is
the whole process.

## Disclosure rules

See `DISCLOSURE.md`. Relative movement is safe, absolute business volume is not.
Naming Flutter and Junglee Games is fine as long as it is never paired with an
absolute figure. No absolute figures are recorded anywhere in this repository,
including in a resume — those go to recruiters directly, not here.
