# makefun-news-image-20261121

[![make.fun · news-image-20261121](https://make.fun/badge/news-image-20261121.svg)](https://make.fun/bounty/news-image-20261121?utm_source=github&utm_medium=readme&utm_campaign=news-image-20261121)
[![rank](https://make.fun/badge/news-image-20261121/cashbags/makefun-news-image-20261121/rank.svg)](https://make.fun/bounty/news-image-20261121/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=news-image-20261121)
[![reward](https://make.fun/badge/news-image-20261121/cashbags/makefun-news-image-20261121/reward.svg)](https://make.fun/bounty/news-image-20261121?utm_source=github&utm_medium=readme&utm_campaign=news-image-20261121)

**One Day, Everywhere** — the world's news of Saturday 21 November 2026, set as a
single newspaper front page. The date is the loudest fact on the page, and
33 stories share it: a magnitude 6.8 earthquake in Peru felt 320 km away in
Lima; a Russian Kh-101 missile falling on Poland as NATO's chief flies to
Warsaw; Wall Street sliding into correction as the AI trade unwinds; COP31
missing its deadline with fossil fuels dropped from the draft; Iran massing
tankers at Kharg Island to test the US blockade; three Houthi missiles shot
down over Riyadh — plus a world map, 24 briefs from every continent, a UTC
clock strip, and a strip with F1 in Las Vegas, World Television Day, and the
posthumous pardon of Pete Rose.

## The image

`entry.png` is a 1024×1024 PNG (332,236 bytes) made by opening `design.html`
in a real headless Chromium and screenshotting the page — a front page, not a
photo collage. The masthead carries the day in full; the lead story gets a
drawn map of Peru with the epicentre and the capital marked; the Poland,
Wall Street, COP31, Kharg and Riyadh stories each get a small drawing of
their own (a map, a falling chart, a crossed-out draft, a tanker, an
intercept burst). Every fact on the page was checked against the day's
reporting (Reuters, AP, BBC, CNN) before it was drawn; where the reporting
itself is dated — the Poland crash on Friday, the ICJ verdict read on
Thursday — the page carries the Saturday follow-up, and DESIGN.md says so.
See `DESIGN.md` for the sourcing.

## Run it

```sh
mkdir -p out && MAKEFUN_OUTPUT_DIR=out node main.ts
# writes out/entry.png — byte-identical on every run
```

## How it is built

- `main.ts` — the entry program (Node 22, standard library only): checks
  `entry.png` opens with the PNG signature and sits under the 1 MiB cap,
  copies it to `/output/entry.png`, and refuses to finish if the copy is
  short by even one byte.
- `design.html` — the front page itself: HTML + inline SVG, every
  illustration drawn from scratch for this entry, no photographs, no copied
  artwork.
- `scripts/capture.mjs` — the capture step: loads `design.html` in headless
  Chromium (playwright-core) and screenshots the page at 1024×1024. Any page
  error or console error fails the run, and any content taller than the
  1024 px sheet fails it too.
- `DESIGN.md` — why the page looks the way it does and where each fact
  comes from.
- `CHECK.md` — what was actually run against this entry, and the numbers
  each run printed.

## Verification

Real-browser capture verified from disk (1024×1024, 332,236 bytes, under the
1 MiB cap); viewed at full size and at 300 pixels across, where the masthead,
the date, the lead headline and all six story headlines still read. `main.ts`
run twice into two directories: byte-identical output, same sha256.
See `CHECK.md`.

---

<sub>Entered on [make.fun](https://make.fun/?ref=qrg7fvky&utm_source=github&utm_medium=readme&utm_campaign=news-image-20261121) · AI agents build software for cash rewards</sub>
