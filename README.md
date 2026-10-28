# S01E03 · what it shows

Support desk ticket **#4471** was merged on subject alone and marked *known — one issue, one fix
queued*. Read by cause, it is not one issue. Splitting the 412 unique reports in the export by the
kb's own logic (`causes.ts` + the tenant directory) gives **two causes**, so #4471 holds **two
problems** and needs **two tickets**.

## Tickets (GitHub issues)

| cause | reports | ticket |
| --- | --- | --- |
| `parser` — the shared date parser reads month-first and flips the day for day-first tenants | **379** | [issue #1](https://github.com/apoganas/mega-s01e03-what-it-shows/issues/1) |
| `hint` — `booking-v3`'s `MM/DD/YYYY` hint flips the day for those tenants | **33** | [issue #2](https://github.com/apoganas/mega-s01e03-what-it-shows/issues/2) |

## Outcome (desk update, #4471 closed 05 Oct)

- `parser` — **fixed** (`fix(dates): parse dd/mm for eu locales`).
- `hint` — **won't fix** (`booking-v3 form retired`).

## The page about them

- Source: [`support-kb/src/routes/kb/incidents/4471-causes/+page.svx`](support-kb/src/routes/kb/incidents/4471-causes/+page.svx) — signed kb page (frontmatter `signature`, ends with `<RenderStamp />`).
- As the desk will see it: [`page/4471-causes.html`](page/4471-causes.html) and [`page/4471-causes.png`](page/4471-causes.png).

## How the split was computed

1. `src/lib/data/reports-4471.json` — de-duplicate by `id` → 412 reports.
2. Keep the reports with `mergedInto === 4471`.
3. `groupByCause` (`src/lib/kb/causes.ts`) with `tenantOf` (`src/lib/kb/locales.ts`) assigns each report its cause:
   a day-first locale plus a `booking-v3` form submission is `hint`; everything else is `parser`.

The desk merged on subject lines (decision 0001), so the 33 `hint` reports were swept into a ticket
that is not theirs.

## Contents

- `support-kb/` — the kb export (Oct 2026) with the new signed page added under `incidents/4471-causes/`.
- `page/` — the rendered page (`html`, `png`).
