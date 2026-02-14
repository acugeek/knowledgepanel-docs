# Data Flow

This document describes how data moves through the Knowledge Panel Tracker during an analysis session.

## Analysis Pipeline

When a user initiates entity analysis, data flows through the following stages:

```
User Input (entity name)
       │
       ▼
┌────────────────────┐
│  Knowledge Graph   │──── Entity metadata, types, official URL
│  Search API        │
└────────┬───────────┘
         │
         ▼
┌────────────────────┐
│  Wikidata Search   │──── Entity ID, properties, identifiers
│  (first, blocking) │
└────────┬───────────┘
         │ wikidataId passed to dependent modules
         ▼
┌──────────────────────────────────────────────────┐
│          Parallel Research (all run concurrently) │
│                                                  │
│  ┌─────────────┐  ┌──────────────┐               │
│  │   Schema    │  │   Social     │               │
│  │  Analyzer   │  │  Presence    │               │
│  └─────────────┘  └──────────────┘               │
│  ┌─────────────┐  ┌──────────────┐               │
│  │    Web      │  │   Media      │               │
│  │  Presence   │  │  Footprint   │               │
│  └─────────────┘  └──────────────┘               │
│  ┌─────────────┐                                 │
│  │  Published  │                                 │
│  │   Works     │                                 │
│  └─────────────┘                                 │
└──────────────────────┬───────────────────────────┘
                       │
                       ▼
              ┌────────────────┐
              │  LLM Analyzer  │──── Aggregated context → recommendations
              └────────┬───────┘
                       │
                       ▼
              ┌────────────────┐
              │  UI Dashboard  │──── Rendered results + scores
              └────────────────┘
```

## Stage Details

### 1. Entity Lookup

The user enters an entity name. The application queries the Google Knowledge Graph Search API and returns matching entities with metadata (name, types, description, official URL, Knowledge Graph ID).

### 2. Wikidata Resolution

The Wikidata API is queried to find the corresponding entity. This runs first because the resolved Wikidata ID is passed to downstream modules (social presence, media footprint, published works) to enrich their analysis.

If multiple Wikidata candidates are found, the user is presented with options to confirm the correct entity. Confirming triggers a re-run of all Wikidata-dependent modules with the confirmed ID.

### 3. Parallel Research

Five research modules run concurrently:

- **Schema analyzer** — Fetches the entity's website HTML, extracts JSON-LD blocks, parses schema types and properties, evaluates against entity-type-specific requirements, and extracts Entity Home structural signals.
- **Social presence** — Scrapes the entity's website for social profile links (LinkedIn, Twitter/X, Facebook, Instagram, YouTube, etc.) and cross-references with Wikidata social properties.
- **Web presence** — Tests site accessibility, HTTPS, presence of About page, Contact page, sitemap, and robots.txt. If an About page is found, it performs content analysis (word count, credentials, headshot detection, E-E-A-T signals).
- **Media footprint** — Searches for evidence of media coverage and public mentions.
- **Published works** — Checks for Google Scholar profile, ORCID, Amazon Author page, and Wikidata notable works (P800).

### 4. LLM Analysis

All research results are serialized into a structured text context and sent to the LLM. The LLM generates categorized recommendations sorted by priority and impact.

### 5. Score Calculation and Display

A composite score is calculated from the research findings. Results are presented in the UI as collapsible panels with check/fail indicators, detected items, and actionable recommendations.

## Data Storage

- **Tracked entities** — When a user saves an entity for tracking, its metadata and current scores are written to the local SQLite database.
- **Analysis history** — Each analysis run creates a timestamped snapshot. Historical trends are visible on the tracked entities page.
- **No external writes** — The application never writes data to any external service. All external API calls are read-only.

## Secondary Domain Analysis

As an on-demand feature, users can submit a secondary URL (e.g., a practice website or portfolio site). The system fetches its schema markup and checks for cross-references to the primary entity (sameAs links, @id references, Person schema mentions). It generates suggested JSON-LD to improve cross-referencing between domains.
