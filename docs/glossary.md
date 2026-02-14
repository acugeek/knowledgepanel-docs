# Glossary

Key terms and concepts used in the Knowledge Panel Tracker.

## Entity

A distinct, well-defined thing that Google can identify — a person, organization, place, event, or concept. Entities are the foundation of the Knowledge Graph.

## Knowledge Panel

The information box that appears on the right side of Google search results for recognized entities. It displays structured facts sourced from the Knowledge Graph, Wikidata, and the entity's official website.

## Knowledge Graph

Google's database of entities and their relationships. It powers Knowledge Panels, featured snippets, and other structured search features. Entities are identified by a Knowledge Graph Machine ID (KGMID).

## Entity Home

The single authoritative website that Google associates with an entity. Establishing a clear Entity Home with proper schema markup is a foundational step for Knowledge Panel eligibility.

## Schema Markup (JSON-LD)

A structured data format embedded in web pages using the schema.org vocabulary. JSON-LD (JavaScript Object Notation for Linked Data) is the recommended format. It helps search engines understand the content and relationships on a page.

## Entity Home Signals

Structural schema elements that tell Google a page is the authoritative home for an entity. Key signals include WebSite schema, mainEntityOfPage, BreadcrumbList, ProfilePage or AboutPage types, @id cross-references between schemas, and comprehensive sameAs links.

## sameAs

A schema.org property that lists URLs for the same entity on other platforms — Wikipedia, Wikidata, LinkedIn, social media profiles, etc. Each verified sameAs link strengthens the entity's identity in the Knowledge Graph.

## E-E-A-T

Experience, Expertise, Authoritativeness, and Trust. Google's quality framework for evaluating content and its creators. Strong E-E-A-T signals on an entity's About page contribute to entity recognition and content ranking.

## Wikidata

A free, collaborative knowledge base maintained by the Wikimedia Foundation. Wikidata entries provide structured data that Google uses to populate Knowledge Panels. Key properties include official website (P856), social media IDs, ORCID (P496), Google Scholar ID (P1960), and notable works (P800).

## KGMID

Knowledge Graph Machine ID. A unique identifier Google assigns to each entity in the Knowledge Graph (e.g., `/g/11lzp14jzd`). It appears in the entity's Google search URL and can be used to reference the entity programmatically.

## ORCID

Open Researcher and Contributor ID. A persistent digital identifier for researchers. Linking an ORCID profile to Wikidata (P496) strengthens the connection between an entity and their published research.

## Secondary Domain

A website other than the primary Entity Home that is associated with the entity — for example, a practice website, portfolio, or project site. Cross-referencing between the Entity Home and secondary domains via schema markup strengthens entity coherence.

## Deep Dive

The application's term for a comprehensive analysis run that executes all research modules (Wikidata, schema, social, web presence, media, published works) and generates LLM recommendations.
