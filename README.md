# Power BI Portfolio: Megan Small

These are four Power BI reports built on real data from my businesses, my code and my degree. Each one is a **Power BI Project (.pbip)**: a text-based format with a TMDL semantic model and a PBIR report. That means the whole model, every DAX measure and every visual can be read and diffed in Git.

| Report | What it answers | Data | Pages |
|---|---|---|---|
| **Maine Cleaning Co Operations** | How did revenue, clients and short-term-rental turnovers change from 2023 to 2026? | 3,113 Jobber invoices, 188 clients (anonymized), Mar 2023–Oct 2026 | Overview · Clients & Retention · STR Turnovers · Segments |
| **GitHub Dev Portfolio** | What have I built, how much of it, and with what tech? | 2,412 commits, 13 repos, 1,274 PRs (full git history), Mar–Nov 2026 | Overview · Projects · Work Patterns · Tech Stack |
| **USM Academic Progress** | Where am I on the degree, and how heavy is this term? | Course history plus 73 Fall 2026 deadlines from my school calendar | Degree Progress · Fall 2026 Workload · Path to Graduation |
| **Software Stack** | Which tools did I buy, outgrow and replace with my own build? | 31 tools + dependency files from 10 code projects | Stack Overview · Build vs Buy · Tech in Code |

## How to open

1. Clone or download this repo (Code → Download ZIP), then **extract it**. Don't open files from inside the zip. Keep each `.pbip` next to its `.Report` and `.SemanticModel` folders.
2. In **Power BI Desktop** (a current version), open the `.pbip` file inside a report folder.
   * If Desktop says the report format needs a preview feature, turn on **File → Options → Preview features → "Store reports using enhanced metadata format (PBIR)"** and **"Power BI Project (.pbip) save option"**, then restart Desktop.
3. Click **Refresh** once. The data is embedded in each query, so there are no files to locate and no credentials to enter.
4. To share a report as a single file, use **File → Save as → .pbix**. To publish it, use **Publish → My workspace**.

## Modeling notes (good to mention in interviews)

* **Star schemas.** The fact tables (Invoices, Commits, Deadlines) relate many-to-one to dimensions (Clients, Repositories, Courses) and to a marked Date table. Auto date/time is turned off.
* **Time intelligence.** Revenue PY, YoY %, YTD, rolling 3-month and year-over-year client retention (`INTERSECT` of this period's and last year's client lists).
* **Ranking and concentration.** Top-15 client bars use `RANKX` over `ALLSELECTED`. Top-10 revenue share uses `TOPN`.
* **What-if parameter.** The *Path to Graduation* page recalculates the terms remaining for any credit load.
* **Documented model.** Every table and most measures carry descriptions, which show as tooltips in the field list.
* **Theme.** One custom dark theme is shared by all four reports. Its categorical palette was checked for colorblind separation and contrast.

## Data handling

* **Cleaning company:** Dollar amounts are multiplied by one constant factor for privacy. Growth rates, shares, rankings, seasonality and retention are exact; totals are not the real figures. Client names were replaced with keys such as `RES-042`, `STR-007` and `COM-003`. Each key is the segment plus the order of the client's first invoice. No names, addresses or invoice subjects are included. Segment comes from the client name and the invoice subjects. Service cadence comes from the median gap between a client's invoices.
* **GitHub:** Only commit metadata is used (date, repo, file types, commit type parsed from the message, PR number). Bot and merge commits are excluded. No code or commit messages are included.
* **School:** Grades are shown for completed USM courses only. Deadlines come from the Brightspace calendar feeds plus dates I entered by hand.
* **Tools:** This one is hand-maintained. Dates are filled in only where known. To add costs or dates, use **Transform data → Tools → Source**, or ask me to regenerate it.

Snapshot taken November 2, 2026.
