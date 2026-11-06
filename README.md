# Power BI Portfolio · Megan Small

**Business analytics on real operating data.** Four Power BI reports built from a cleaning company I run, the software I build, and my degree progress. Each one starts with a business question, uses a star-schema model with documented DAX measures, and ships as a text-based Power BI Project, so every table, measure and visual can be reviewed right here on GitHub.

`Power BI Desktop` · `DAX` · `Power Query (M)` · `Star-schema modeling` · `Time intelligence` · `PBIP / TMDL` · `Python data prep` · `Data anonymization` · `Git`

---

## The reports

| | Report | Business question | Data |
|---|---|---|---|
| 🧽 | **[Maine Cleaning Co Operations](Maine-Cleaning-Co-Operations/)** | Where does revenue come from, which clients stay, and how seasonal is rental work? | 3,113 invoices · 188 clients · Mar 2023 – Oct 2026 |
| 💻 | **[GitHub Dev Portfolio](GitHub-Dev-Portfolio/)** | What have I built, with what tech, and how does the work break down? | 2,412 commits · 1,274 pull requests · 13 repos |
| 🧰 | **[Software Stack](Software-Stack/)** | Which tools did the business outgrow, and what replaced them? | 31 tools · dependency files from 9 code projects |
| 🎓 | **[USM Academic Progress](USM-Academic-Progress/)** | How far along is the degree, and how heavy is this term? | Course history · 73 Fall 2026 deadlines |

## Highlights

**Maine Cleaning Co Operations**
- Commercial clients brought in **41% of revenue from 5% of clients**. Their average invoice runs **2.7× a residential clean**.
- The **top 10 clients account for 51% of revenue**, a concentration risk the report makes visible.
- **63% of clients booked more than once.** Cohort tracking shows how many clients from each starting year are still booking.
- Rental turnovers peak hard: **July and August hold 34% of the year's turnovers**, versus about 7% for January and February combined.

**GitHub Dev Portfolio**
- **1,274 pull requests across 160 active days** in eight months. Nearly two-thirds of all commits went into BrightBase, the operations platform that replaced the company's field-service, scheduling and CRM tools.
- The work is mostly building, not patching: **feature commits outnumber fixes about 1.7 to 1**.
- Full-stack spread: JavaScript 34%, Python 28%, TypeScript 26% of files changed.

**Software Stack**
- Four tools replaced so far. **Three of them (Jobber, Connecteam and a custom Twenty CRM build) were consolidated into BrightBase**, a platform I built.

## How the reports are built

```
Extract           Transform (Python)            Model (Power BI)              Validate
───────           ──────────────────            ────────────────              ────────
Jobber invoices   dedupe, classify segments,    star schema + Date table,     Microsoft JSON schemas,
git history   ─►  anonymize clients, derive ─►  DAX measures, descriptions ─► TOM model load, field
calendar feeds    cadence, parse commit types   on every table and measure    and layout checks
```

- **Modeling:** fact tables (Invoices, Commits, Deadlines) join many-to-one to dimensions (Clients, Repositories, Courses) and to a marked Date table. Auto date/time is off.
- **DAX highlights:** like-for-like year-over-year growth that only compares dates with data in both years, client retention via `INTERSECT` of this year's and last year's client sets, `RANKX`-driven top-N visuals, and a what-if parameter.
- **Accuracy over flattery:** an independent review caught year-over-year cards comparing partial years. Those measures were rewritten to compare matching date ranges only.

## Data & privacy

- **Cleaning company:** client names are replaced with keys like `RES-042` and `STR-007`. **Dollar amounts are multiplied by one constant factor**, so growth rates, shares, rankings, seasonality and retention are exact, but the totals are not the real figures.
- **GitHub:** commit metadata only (date, repo, file types, PR number). No source code or commit messages.
- **School:** grades appear for completed courses only.

## Open a report

1. Click **Code → Download ZIP** and **extract** it. Don't open files from inside the zip.
2. Open any `.pbip` file in a current version of **Power BI Desktop**. Keep it next to its `.Report` and `.SemanticModel` folders.
3. Click **Refresh**. The data is embedded, so there's nothing to connect and no login.

## Repository layout

```
<Report>/
├── <Report>.pbip                 open this in Power BI Desktop
├── <Report>.SemanticModel/       the data model, in TMDL (plain text)
│   └── definition/tables/*.tmdl  one file per table: columns, DAX measures, descriptions
└── <Report>.Report/              pages and visuals, in PBIR (JSON)
```

Start with any `tables/*.tmdl` file to read the model and measures without opening Power BI.

---

**Megan Small** · Business analytics & systems · B.S. Business Analytics & AI (CS minor), University of Southern Maine, in progress · [mlinx.studio](https://mlinx.studio)
