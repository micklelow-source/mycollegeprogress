# College Progress

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
https://micklelow-source.github.io/collegeprogress/
```

On your phone: open that, then Share → **Add to Home Screen** for an app-like icon.

**From your computer.** Download `index.html` and double-click it. It runs entirely
offline; no dependencies, no build step, no network requests.

## Public repo, private data

This repo is public so that Pages works on a free plan. That is safe here **because
the page contains no data** — everything you type is held in your browser's local
storage. Anyone who opens the URL sees an empty dashboard.

The one file that *is* your real record is a Backup JSON. `.gitignore` blocks it from
ever being committed. Keep backups somewhere private instead.

## How saving works

Everything you type is written to your browser's **local storage** the moment you save
an entry. It never leaves the device and nothing is uploaded anywhere.

That means the data is per-browser, so there are two buttons for moving it around:

| Button | What it does |
|---|---|
| **Backup** | Downloads `progress-YYYY-MM-DD.json` — your whole dashboard in one file |
| **Restore** | Replaces everything from a backup file you pick |

To move your record to another device: **Backup** on the old one, transfer the file
(email, iCloud, Drive), **Restore** on the new one.

Because storage is per-browser, back up every few weeks. Safari in particular clears
script-writable storage for sites you have not opened in about 7 days, so a long gap
between visits on an iPhone can wipe your entries. The backup file is the insurance.

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

- **Light and dark themes**, following your system by default; the `◐` button cycles
  auto → light → dark.
- **Load example data** (bottom of Goals & College) fills every chart with a fictional
  cadet's record so you can see how it looks. **Erase everything** clears it.
- Charts use a colourblind-safe palette, every chart has a table view or direct labels,
  and the whole thing respects `prefers-reduced-motion`.
- The dashboard is one file on purpose — easy to email to yourself, keep on a USB
  stick, or open on any machine without installing anything.
