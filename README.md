# Lien Deadlines — Free Mechanics Lien Deadline Reference & Open Dataset

A free, statute-cited reference and calculator for U.S. mechanics/construction lien
deadlines, plus an open dataset anyone can reuse.

**Informational only — not legal advice.** See the disclaimer below and on the site.

## Coverage (v0.1)

| State | Statute | Roles |
|-------|---------|-------|
| California | Civil Code §8000 et seq. | Direct contractor, Subcontractor/supplier |
| Texas | Property Code Ch. 53 (post-2022) | Original contractor, Subcontractor/supplier |
| Florida | Statutes Ch. 713 | Contractor (privity), Subcontractor/supplier |

Each deadline (preliminary/monthly notice, lien recording/affidavit, foreclosure suit)
is tied to the specific statute section that creates it.

## What's here

- **`index.html`** — single-file static site: state reference tables + a deadline
  calculator (calendar math on the standard statutory period). Zero dependencies.
- **`data/deadlines.json`** — canonical dataset, nested state → role → deadline.
- **`data/deadlines.csv`** — flat one-row-per-deadline export.

## Why this exists

Subcontractors lose lien rights by missing a date, not by losing an argument. The
deadlines are public law, but they're scattered across statutes and buried inside
$400/month compliance platforms. This puts the load-bearing dates — with citations —
in one free page, and the underlying data in the open.

## Data schema (`deadlines.json`)

```
states[].code / name / statute
states[].roles[].role / label
states[].roles[].deadlines[]:
  key         machine id (preliminary-notice, record-lien, foreclose, ...)
  name        human label
  period      human period ("90 days", "15th day of the 4th month")
  periodDays  integer days for simple calendar math, or null for month-15 rules
  trigger     event the clock runs from
  servedOn    (notices) who must be served
  statute     verbatim citation
  notes       exceptions / accelerations
```

## Local preview

```bash
python3 -m http.server 8080   # then open http://localhost:8080
```

(Must be served over HTTP, not `file://`, so the page can `fetch` the dataset.)

## Disclaimer

This project is for general informational purposes only and is **not legal advice**.
Lien deadlines depend on facts (project type, your tier, notices recorded by others,
weekends/holidays, contract terms, tolling) and statutes change. Many exceptions apply.
Always verify against the current statute and consult a licensed attorney in the
relevant state before relying on any date. No attorney-client relationship is created
by use of this project. The calculator performs plain calendar arithmetic on the
standard period and does not judge which rule applies to your situation.

## License

- **Data** (`data/`): CC BY 4.0 — attribution: "lien-deadlines open dataset".
- **Code**: MIT.

Corrections to citations are especially welcome — accuracy is the whole point.

_Last verified: 2026-06-10._
