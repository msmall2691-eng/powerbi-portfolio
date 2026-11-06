# Software Stack · Build vs. Buy

> **Business question:** Which tools did the business run on, which did it outgrow, and what replaced them?

An inventory of 31 tools used across The Maine Cleaning Co, my software studio and school, joined to the technologies declared in my code projects.

## What it shows

1. Four tools replaced so far. Three of them (Jobber, Connecteam and a custom Twenty CRM build) were consolidated into BrightBase.
2. React appears in 9 projects, Tailwind CSS in 8 and TypeScript in 7.

## Pages

| Page | What's on it |
|---|---|
| **Stack Overview** | Tools by area and status, status mix, full inventory. |
| **Build vs Buy** | Migration map of retired tools and their replacements, plus the reasoning behind building BrightBase. |
| **Tech in Code** | Frameworks and services declared in each project's dependency files. |

## Data model

| Table | Role | Rows describe |
|---|---|---|
| `Code Libraries` | Dimension | Technologies declared in each project's package.json / requirements.txt. |
| `Tools` | Dimension | Software used across The Maine Cleaning Co, M Studio and school. |

## Key DAX measures

**Tools In Use**

```dax
CALCULATE([Tool Count], Tools[Status] IN {"In use", "Setting up", "Being replaced"})
```

**Replaced by BrightBase** · Off-the-shelf tools retired or being retired in favor of the in-house platform.

```dax
CALCULATE([Tool Count], Tools[Replaced by Own Build] = "Yes")
```

**Projects Using**

```dax
DISTINCTCOUNT('Code Libraries'[Project])
```

<details><summary>All 8 measures</summary>

| Measure | Table | Definition |
|---|---|---|
| Projects Using | Code Libraries | `DISTINCTCOUNT('Code Libraries'[Project])` |
| Technologies | Code Libraries | `DISTINCTCOUNT('Code Libraries'[Technology])` |
| Tool Count | Tools | `COUNTROWS(Tools)` |
| Tools In Use | Tools | `CALCULATE([Tool Count], Tools[Status] IN {"In use", "Setting up", "Being replaced"})` |
| Tools Retired | Tools | `CALCULATE([Tool Count], Tools[Status] IN {"Retired", "Previously used"})` |
| Replaced by BrightBase | Tools | `CALCULATE([Tool Count], Tools[Replaced by Own Build] = "Yes")` |
| Category Groups | Tools | `DISTINCTCOUNT(Tools[Category Group])` |
| Planned Tools | Tools | `CALCULATE([Tool Count], Tools[Status] = "Planned")` |

</details>

## Data preparation

- Tool list maintained by hand from what I've used; dates are included only where known.
- Technology list parsed from each project's package.json and requirements.txt.

## Open it

Open the `.pbip` file in this folder with Power BI Desktop and click **Refresh**. The data is embedded in the model, so there's nothing to connect.

[← Back to all reports](../README.md)
