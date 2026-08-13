# Corinne’s Progress Center

A single-file dashboard for tracking academics, fitness/PT, sports, service, awards and
personal goals — built around what college admissions and JROTC/ROTC scholarship boards
actually ask for. The page is public; everything you enter stays private in your own
browser.

```
index.html   the whole dashboard (open it, that's it)
.gitignore   keeps your progress backups out of this public repo
```

## Opening it

**From a URL.** GitHub Pages serves this repo at:

```
https://micklelow-source.github.io/mycollegeprogress/
```

On your phone: open that, then Share → **Add to Home Screen** for an app-like icon.

**From your computer.** Download `index.html` and double-click it — no dependencies and
no build step. Note that Google Drive sync only works over the hosted URL: OAuth cannot
authorise a `file://` origin, so the local copy is browser-storage only.

## Public repo, private data

This repo is public so that Pages works on a free plan. That is safe here **because
the page contains no data** — what you type lives in your browser, and in your own
Google Drive if you switch sync on. Neither is in this repo. Anyone who opens the URL
sees an empty dashboard.

The one file that *is* your real record is a Backup JSON. `.gitignore` blocks it from
ever being committed. Keep backups somewhere private instead.

## How saving works

There are two layers, and you can use either or both.

**1. This browser (always on).** Every entry is written to local storage the moment you
save it. Instant, private, works offline — but it is tied to one browser, and Safari
clears script-writable storage for sites you have not opened in about 7 days.

**2. Google Drive sync (optional).** Connect a Google account and your record is kept in
Drive's `appDataFolder` — a hidden folder only this app can see. That fixes both limits:
it survives a cleared browser, and signing in on your phone picks up what you entered on
your laptop. The `drive.appdata` scope grants **no access to the rest of your Drive**;
the app can only touch the one file it created.

Sync needs a free Google Cloud OAuth client ID, because the app runs entirely in your
browser with no server behind it. The **Set up Google sync** button walks through it —
roughly five minutes, one time:

1. Create a project at `console.cloud.google.com`
2. Enable the **Google Drive API**
3. OAuth consent screen → **External**, add your own address under **Test users**
4. Credentials → **OAuth client ID** → **Web application**
5. Authorised JavaScript origins: `https://micklelow-source.github.io`
6. Paste the client ID into the dashboard

Google will warn that the app is unverified — that is expected for a personal project.
Choose **Advanced → Go to app** to continue. Once connected, edits push to Drive
automatically a couple of seconds after you make them.

If both this device and Drive hold data when you first connect, the dashboard shows you
both timestamps and asks which to keep. It never silently discards either side.

**3. Backup / Restore (belt and braces).** **Backup** downloads a JSON file of
everything; **Restore** loads one back. Worth doing occasionally even with sync on. Keep
those files somewhere private and never commit one to this public repo.

## The tabs

**Overview** — the readiness score, a KPI row, GPA trend, upcoming deadlines and every
open goal.

**Academics** — term-by-term GPA (weighted and unweighted), courses with their rigor
level, and test scores. Best normalised score counts toward the score.

**Fitness & PT** — one panel per event with its trend and distance to goal. Ships with
the JROTC Cadet Challenge and Army ROTC staples (push-ups, curl-ups, pull-ups,
one-mile, two-mile, shuttle run); add or edit any of them. Timed events accept `m:ss`
(type `6:30`) and are scored so *lower is better*.

**Sports & Service** — seasons and levels, leadership billets, and a monthly service
hours chart.

**Awards** — a timeline of ribbons, medals, honour roll, promotions and certifications,
plus a breakdown by recognition level (school → national).

**Goals & College** — goals with a target number, a date and tickable milestones;
college/ROTC targets each with their own requirement checklist. New targets come
pre-filled with a standard ROTC scholarship checklist.

## The readiness score

One number out of 100, recomputed from your data on every change. It is a **personal
planning tool, not an admissions prediction** — no college or ROTC board uses it. Its
job is to show which pillar is lagging.

| Pillar | Points | Full marks at |
|---|---|---|
| Academics | 30 | 4.3 cumulative weighted GPA (16) · 8 rigor courses (7) · top test score (7) |
| Fitness & PT | 20 | every PT event at its goal |
| Leadership & service | 20 | 100 service hours (10) · 4 leadership roles (10) |
| Awards & athletics | 15 | 24 award "reach points" (10) · 4 varsity seasons (5) |
| Goal follow-through | 15 | average progress across your goals |

Award reach points: school 1, district 2, state 4, national 5.

Want a different weighting? Edit `PILLARS` and `scoreBreakdown()` in `index.html` —
they're near the top of the `<script>` block and deliberately kept in one place.

## Notes

- **Purple and white by default**; the `◐` button cycles light → dark → follow-system.
- **Each tab opens with its own illustrated banner** — a hawk over an academy facade for
  Academics, skiing/softball/soccer for Sports, a nursing motif for Goals, and so on. All
  original artwork drawn inline as SVG; nothing reproduces a real school's crest or logo.
- **Vector graphics throughout** — a single stroked icon set, a generated laurel wreath
  around the readiness ring, and a chevron rank motif behind the header. All inline SVG,
  so everything stays sharp at any zoom and recolours with the theme.
- **Load example data** (bottom of Goals & College) fills every chart with a fictional
  cadet's record so you can see how it looks. **Erase everything** clears it.
- Charts use a colourblind-safe palette, every chart has a table view or direct labels,
  and the whole thing respects `prefers-reduced-motion`.
- The dashboard is one file on purpose — easy to email to yourself, keep on a USB
  stick, or open on any machine without installing anything.
