# Changelog

High-level release history for the Knowledge Panel Tracker.

## 2026-02-15

- Multi-page schema analysis: `analyzeSchema` now fetches both homepage and `/about` page (with `/about-me`, `/bio`, `/about-us` fallbacks)
- Page-aware schema requirements: each property tagged with target page (`home`, `about`, or `either`)
- Entity Home Signals now detect AboutPage/ProfilePage schemas found on the about page
- Removed hallucinated schema recommendations (`author` on Person, `nationality`)
- Missing property UI shows page attribution badges (🏠 homepage / 📄 about page / 📍 either)
- Fixed secondary domain schema checker when entity has no pre-populated official URL
- AI Analysis now receives about-page schema data; no longer recommends adding schemas that already exist on `/about`
- Fixed `missingSchemas` serialization in LLM context (was outputting `[object Object]`)
- Secondary domain checker now detects relationship type (same-entity vs founded-business vs employer) and adjusts recommendations accordingly — no longer recommends `sameAs` for separate businesses

## 2026-02-14

- Entity-type-aware schema requirements (supports Person, Organization, Athlete, Musician, Actor, Author, Politician, BusinessPerson, Medical entity types)
- Entity Home signal evaluation (WebSite schema, BreadcrumbList, ProfilePage, mainEntityOfPage, @id cross-references, sameAs completeness with per-platform breakdown)
- Secondary domain schema checker with cross-reference analysis and suggested JSON-LD generation
- About page deep analysis with E-E-A-T signal assessment (Experience, Expertise, Authoritativeness, Trust)
- Expanded Wikidata social property lookups (GitHub, TikTok, Pinterest)
- Context-aware Published Works recommendations

## 2026-02-10

- Historical score tracking and trend visualization
- Dynamic year selection across analysis panels
- YTD-to-YTD comparison for accurate trend indicators

## 2026-01-28

- Initial release
- Entity search via Google Knowledge Graph API
- Wikidata property analysis and completeness scoring
- Schema markup extraction and evaluation
- Social media presence detection
- Web presence health checks
- Published works and academic profile detection
- Media footprint analysis
- LLM-powered recommendation engine
- Entity tracking with SQLite persistence
- Dark-themed responsive UI
