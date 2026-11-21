# CHECK.md — "One Day, Everywhere" (news-image-20261121)

What was actually run against this entry, and what each run said. All of it
was run in this session, against the committed repo, not assumed from the
build: the numbers below are the ones the runs printed.

## The repo and the kit

- Repo `cashbags/makefun-news-image-20261121`, public, created
  2026-11-21T05:12:50Z — after the competition opened (2026-11-21T00:00:00Z).
  License MIT, SPDX-License-Identifier line on top (same LICENSE file that
  passed license_osi for the news-image-20261120 entry). README carries the
  three make.fun badges and the referral `qrg7fvky` (the account's own code
  is `6sknhk5z`, verified live via /api/me/referrals, used ONLY for
  bring-the-humans surfaces, never here — user decision stands). About +
  topics set (editorial, makefun, news, news-image) — topics via the
  dedicated set-topics endpoint, since PATCH alone leaves them empty;
  homepage https://make.fun/bounty/news-image-20261121.
- Kit downloaded fresh from the live API and unpacked at
  `../kit/news-image-20261121-kit` (bundle sha256 `35b3239e…` per kit.json);
  the starter's `main.ts` was read, not copied — this entry's `main.ts` is
  written fresh in this session with its own structure (PNG signature check
  plus 1 MiB cap plus byte-length proof, wrapped in a handOverImage helper
  with a named abort path).
- Competition verified live before building: $100, entryFeeUsd null (free),
  acceptingSubmissions true, 3,122 submissions at check time, deadline
  2026-11-23T00:00:00Z (07:00 WIB Mon 23 Nov), published
  2026-11-21T00:00:00Z. No escrow field in the API response
  (escrow: null) — the submit step decides whether a signed entry is needed;
  the keypair is on hand if so.
- Local HEAD `a138e83ebb2a717922f67f65cc4471a7a89e2639` (1 commit, 7 files);
  GitHub HEAD `8f4f1e50906247a2fe330b0fcda7f5d4eef2a9e0` (confirmed by
  get-ref). The local commit is NOT in the repo — files went up via the
  Contents API, one commit per file — but the trees are identical: all 7
  files byte-identical, verified by downloading each file from
  raw.githubusercontent.com and comparing sha256 with local (all MATCH).
  SUBMIT THE GITHUB HEAD, not the local commit.
- CHECK.md itself was added after the kit check below, as an 8th file; it
  changes nothing about the entry (documentation only). A second kit-check
  run on the 8-file tree is recorded at the end of this file.

## The image: real browser capture, verified from disk

- `node scripts/capture.mjs` (playwright-core, headless Chromium, resolved
  from `~/workspace/makefun/bounties/node_modules`) — the first capture
  failed loudly on purpose: the page overflowed the 1024 px sheet by 580 px
  (capture.mjs measures scrollHeight and refuses an overflowing page).
  Three rounds of trimming followed (shorter decks and briefs, one-line
  headlines, smaller Peru map): 580 → 279 → 163 → 102 → 50 → 7 → 3 → 0 px.
  Two visual defects found by viewing the capture (JUNÍN label touching the
  epicentre rings; world-map dots 5/8 and 3/4 touching) and fixed in
  design.html; re-captured.
- Final `entry.png`: 1024×1024, 332,236 bytes, under the 1 MiB cap, sha256
  `f62bddd83073d0ce0e42001984595c1b45dd723b33acb4da92ce2eb007d67560`.
  Viewed at full size (masthead, date, lead headline, all six story
  headlines, map, briefs, clock and strip read; both SVG defects gone) and
  at 300 px across (masthead, date band, lead headline and story headlines
  still read).
- `main.ts` run twice into two directories: byte-identical output, same
  sha256 `f62bddd8…` as entry.png itself.

## Kit check (no transcripts — this session, 2026-11-21 ~05:14 WIB)

- Command: `node cli/makefun.mjs check --kit <kit> --repo <entry>`
  (no --transcripts: no bundle could be written from this session, see
  Transcripts below).
- Result: **4 passed, 1 failed, 14 skipped, 5 at submission** —
  `not ready: fix transcripts_present, then check again`.
- Passes: competition_open (now between opening 2026-11-21T00:00:00Z and
  deadline 2026-11-23T00:00:00Z), snapshot (7 files, 373,424 bytes, within
  the intake's caps), license_osi (SPDX-License-Identifier: MIT,
  OSI-approved), entrypoint (main.ts, node22).
- The one failure, transcripts_present, is structural to this subagent run
  and expected: no bundle can be sealed from this session (see Transcripts).
  Nothing needs rebuilding.
- NOTE on the "Entry tree ≤8192 bytes" line: that cap does not apply to this
  competition. The kit's own check reports the snapshot "within the intake's
  caps" (each file at most 100 MiB, repository at most 512 MiB), the
  competition RULES state no 8,192-byte tree cap (that cap belonged to
  tiny-chess), and the news-17/18/19/20 entries passed the same check at
  ~275–373 KB. The tree was NOT shrunk to 8,192 bytes: doing so would mean
  dropping entry.png, which is the entry itself.
- At-submission checks (site-side, not yet run): repo_public (repo IS
  public), repo_owner (owner cashbags is the account's GitHub login),
  repo_created_after_open (created 2026-11-21T05:12:50Z, after opening),
  commit_in_repo (submit the GITHUB HEAD 8f4f1e50…, NOT the local commit
  a138e83…, which is not in the repo), duplicate_snapshot (all files are
  this session's own work).

## Transcripts — NOT sealed, parent must re-bundle in a live session

- No bundle was attempted in this session, per the build spec: sealing is
  impossible from this cron-originated run (same root cause as
  news-image-20261120 — the parent chain terminates at a scheduler.cron
  root session that never heard the person type the prompt; see that
  entry's CHECK.md for the full verification). The entry is NOT sealed.
- Prompt file `prompt-user.txt` holds ONLY the user's verbatim words:
  "Makefun kompetisi baru langsung join". No prompt file with words the
  user did not say was written.
- Fix (parent, after this run): run bundle from the top-level agent in a
  live session once this run completes, with `--session <builder file>
  --no-family --no-discover --muse-usage
  ~/.makefun/muse-usage-news-image-20261121.jsonl` and the same
  harness/prompt/system-prompt flags as the 20261120 seal (system prompt =
  `~/workspace/system/system_prompt.md`, NOT the withheld stub), after
  SELECTing usage rows from muse.db for this builder session and appending
  them to `~/.makefun/muse-usage-news-image-20261121.jsonl`. Then re-run
  the kit check with --transcripts. NOTHING needs rebuilding; the entry,
  repo and image are final.

## News sourcing

Six lead stories plus 24 briefs plus 3 strip items = 33 stories, each
checked against the day's reporting before it was drawn (see DESIGN.md for
the per-story sourcing and the date check): Peru M6.8 quake, Junín, 19:09
local Friday = 00:09 UTC Saturday, felt in Lima, no casualties; Kh-101
crashes near Nowy Lipowiec ~06:30 local, Tusk "deliberate provocation",
Rutte due in Warsaw Saturday; Wall Street Friday close S&P −3.70%,
Nasdaq −5.28%, Dow −1.93%, Nvidia −13.8% on the SEC report, Anthropic
−9.1% day two; COP31 Friday deadline missed, draft drops fossil fuels,
third draft promised Saturday morning; 14+ Iranian tankers at Kharg,
Araghchi "the blockade must be broken", Senate 51–48 war-powers rejection;
three Houthi missiles intercepted over Riyadh early Saturday. Cut: the
US–Venezuela deal, the Van Gogh sale, the Shenzhen trilateral itself,
Cyclone Akvan's landfall and the Han Duck-soo acquittal — the 19 and 20
November entries' stories, not repeated except where Saturday brings the
follow-up.

## Kit check, second run (8-file tree, after CHECK.md was added)

- Command: same as above, run 2026-11-21 ~05:14 WIB.
- Result: **4 passed, 1 failed, 14 skipped, 5 checked at submission** —
  identical to the first run. Snapshot: 8 files, 381,210 bytes, at local
  commit `c4ae77303b4fd76591e5706ce5f255b14cd9bf06` (the commit that added
  CHECK.md). The only failure is again transcripts_present (see Transcripts
  above); nothing else moved.
- This section was filled in after the second run, so the CHECK.md now on
  GitHub differs from the one the second run saw only in this section's
  text. Final GitHub HEAD after pushing the filled-in CHECK.md is recorded
  in the build report, not here (writing it here would change the file
  again).
