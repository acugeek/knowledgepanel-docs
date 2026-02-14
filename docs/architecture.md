# Architecture

This document describes the high-level architecture of the Knowledge Panel Tracker.

## Overview

The application follows a standard Next.js server-rendered architecture. The frontend provides a search and analysis interface, while the backend handles data fetching, analysis, and persistence.

## Components

### Web Interface

The frontend is a React-based single-page application with three primary views:

- **Search page** — Entity lookup via the Google Knowledge Graph API. Users enter a name, review matched entities, and select one for analysis.
- **Entity detail page** — The main analysis dashboard. Displays research results organized into collapsible panels: Wikidata, Schema Markup, Social Presence, Web Presence, Media Footprint, and Published Works.
- **Tracked entities page** — A list of entities the user has saved for ongoing monitoring, with historical score snapshots.

### API Layer

Server-side API routes handle all external data fetching and analysis. Each research module is independently callable, and a combined endpoint runs all modules in parallel for initial analysis.

Research endpoints include:
- Entity search and lookup
- Wikidata property resolution
- Schema markup extraction and scoring
- Social media profile detection
- Web presence and About page analysis
- Media footprint scanning
- Published works and academic profile detection
- Secondary domain schema cross-referencing
- LLM-powered recommendation generation

### Research Engine

The research engine is a collection of server-side modules, each responsible for a specific analysis domain:

| Module | Responsibility |
|---|---|
| Wikidata checker | Searches Wikidata for the entity, evaluates property completeness, identifies missing identifiers |
| Schema analyzer | Fetches JSON-LD from the entity's website, evaluates against entity-type-specific requirements, extracts Entity Home signals |
| Social presence checker | Scrapes the entity's website for social profile links, cross-references with Wikidata social properties |
| Web presence checker | Tests site accessibility, HTTPS, About page availability, sitemap, robots.txt, and performs About page content analysis |
| Media footprint scanner | Searches for media mentions and coverage indicators |
| Published works checker | Detects Google Scholar, ORCID, Amazon Author pages, and Wikidata notable works |
| Secondary domain checker | Analyzes schema on a secondary domain for cross-references to the primary entity |

### LLM Analyzer

After all research modules complete, their findings are aggregated into a structured context payload. This payload is sent to an LLM, which generates prioritized recommendations grouped by category (entity establishment, content authority, technical SEO, digital presence).

### Local Database

A SQLite database stores:
- Tracked entity records (name, type, official URL, Knowledge Graph ID)
- Analysis history with timestamped scores
- No external credentials or sensitive data are stored in the database

## Entity-Type-Aware Analysis

Schema requirements are dynamically selected based on the entity's type (Person, Organization, Athlete, Musician, Author, etc.). Each type has tailored property recommendations drawn from schema.org vocabulary. This ensures recommendations are relevant rather than generic.

## External Dependencies

The system interacts with the following external services (read-only):

- **Google Knowledge Graph Search API** — Entity lookup and metadata retrieval
- **Wikidata API** — Property and identifier verification
- **Google Gemini** — LLM-powered recommendation generation
- **Target websites** — HTML fetching for schema, social links, and content analysis (user-specified URLs only)

No data is written to any external service. All interactions are read-only.
