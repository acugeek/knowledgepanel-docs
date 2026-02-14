---
author: "Dr. Jordan Barber"
website: "https://drjordanbarber.com"
license: "Documentation only"
status: "Active"
last_updated: "2026-02-14"
---

# Knowledge Panel Tracker

A research and analysis tool for auditing, tracking, and improving an entity's presence in Google Knowledge Panels.

## What It Does

- **Entity search and identification** — Looks up entities via the Google Knowledge Graph API and identifies associated metadata, types, and official URLs.
- **Wikidata property analysis** — Cross-references the entity against Wikidata, checking for completeness of identifiers, social links, notable works, and descriptors.
- **Schema markup auditing** — Fetches and parses JSON-LD from the entity's official website, evaluates it against entity-type-aware requirements, and reports missing properties.
- **Entity Home signal evaluation** — Checks for structural schema signals (WebSite, BreadcrumbList, ProfilePage, mainEntityOfPage, sameAs completeness) that influence Knowledge Panel eligibility.
- **Web presence and E-E-A-T analysis** — Assesses the entity's official website for accessibility, About page quality, credentials, expertise indicators, and E-E-A-T signals.
- **Social and media footprint detection** — Identifies linked social profiles, media mentions, published works, and academic profiles (Google Scholar, ORCID).
- **AI-powered recommendations** — Generates prioritized, actionable recommendations using an LLM based on all collected signals.

## Where It Is Used

This tool is used internally by [Dr. Jordan Barber](https://drjordanbarber.com) for entity analysis and Knowledge Panel research. It is designed for individual practitioners, consultants, and researchers who need to audit entity representation across Google's Knowledge Graph and structured data ecosystems.

## High-Level Architecture

The system is a single-page web application with a server-side research layer. The core components are:

| Component | Role |
|---|---|
| **Web interface** | Search, entity detail pages, analysis dashboards, and tracked entity management |
| **Research engine** | Server-side modules that fetch and analyze data from external sources (Knowledge Graph API, Wikidata, target websites) |
| **Schema analyzer** | Parses JSON-LD and evaluates it against entity-type-specific requirements |
| **LLM analyzer** | Aggregates all research findings into a context payload and generates prioritized recommendations |
| **Local database** | Stores tracked entities, analysis history, and scoring snapshots |

```
┌──────────────────────┐
│    Web Interface     │
│  (Search, Dashboards)│
└──────────┬───────────┘
           │
┌──────────▼───────────┐
│   API Routes         │
│  (Research dispatch) │
└──────────┬───────────┘
           │
┌──────────▼───────────────────────────────┐
│         Research Engine                   │
│  ┌──────────┐ ┌──────────┐ ┌───────────┐│
│  │ Wikidata │ │ Schema   │ │ Social &  ││
│  │ Checker  │ │ Analyzer │ │ Web Check ││
│  └──────────┘ └──────────┘ └───────────┘│
│  ┌──────────┐ ┌──────────┐              │
│  │ Media    │ │ Published│              │
│  │ Footprint│ │ Works    │              │
│  └──────────┘ └──────────┘              │
└──────────────────────────────────────────┘
           │
┌──────────▼───────────┐
│   LLM Analyzer       │
│  (Recommendations)   │
└──────────────────────┘
```

## Tech Stack

- **Framework**: Next.js (React, server-side rendering)
- **Language**: TypeScript
- **Database**: SQLite (local, file-based)
- **External APIs**: Google Knowledge Graph Search API, Wikidata API, Google Gemini (LLM)
- **Data formats**: JSON-LD, schema.org vocabulary

## Operational Status

**Status**: Active — in regular use for entity analysis.

**Intended audience**: Individual practitioners and researchers auditing their own entity presence. This is a single-user tool, not a multi-tenant SaaS platform.

## Boundaries

The following are intentionally excluded from this public repository:

- **Source code** — The application source code is maintained in a private repository. This documentation repo provides architectural context without exposing implementation details.
- **API keys and credentials** — All external API credentials are stored in environment variables and never committed to any repository.
- **Local data** — The SQLite database containing tracked entities and analysis history is excluded from version control entirely.
- **Internal endpoints** — Specific API route implementations and internal URL structures are not documented here.

## Responsible Use and Privacy

- This tool performs read-only analysis of publicly available web content, structured data, and public APIs. It does not modify any external systems.
- No personal health information (PHI) is processed or stored.
- All data analysis is performed on publicly accessible websites and knowledge base entries.
- The local database stores only entity metadata derived from public sources (Knowledge Graph results, Wikidata properties, schema.org markup).
- API credentials are managed through environment variables and are never committed to version control.

## Further Reading

| Document | Description |
|---|---|
| [Architecture](docs/architecture.md) | Component breakdown and module responsibilities |
| [Data Flow](docs/data-flow.md) | How data moves through the analysis pipeline |
| [Changelog](docs/changelog.md) | High-level release history |
| [Glossary](docs/glossary.md) | Key terms and concepts |

## Author

**Dr. Jordan Barber** — [https://drjordanbarber.com](https://drjordanbarber.com)

This tool was built to support entity analysis and Knowledge Panel research.
