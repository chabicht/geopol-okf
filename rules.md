# Geopolitics OKF Bundle — Rules & Conventions

This document captures all design decisions governing the structure, formatting,
and authoring of concepts in this OKF bundle. It is project governance, not an
OKF concept, and has no frontmatter.

All agents and humans creating or editing concepts in this bundle MUST follow
these conventions.

---

## 1. Bundle Overview

- **Format**: OKF v0.1 (see `okf.md` for the full specification).
- **Bundle root**: The repository root. All top-level OKF directories are at the root.
- **Sources**: The `sources/` directory contains raw source material (clippings,
  articles, essays). It is NOT part of the OKF bundle. Concepts cite sources by
  their original URL, not by local file path.
- **OKF version**: Declared in root `index.md` as `okf_version: "0.1"`.

---

## 2. Directory Structure

```
geopol-okf/
├── index.md              # Bundle root index (has frontmatter with okf_version)
├── log.md                # Bundle update log
├── rules.md              # This file (governance, not an OKF concept)
├── okf.md                # The OKF specification (reference, not a concept)
├── sources/              # Raw source material (not part of the OKF bundle)
├── actors/               # Countries, leaders, organizations, authors
├── conflicts/            # Wars, crises, sustained standoffs
├── regions/              # Geographic areas with independent dynamics
├── themes/               # Cross-cutting analytical topics and frameworks
└── events/               # Discrete occurrences
```

---

## 3. Type System

Five types, one per top-level directory. Types are flat — subcategories are
expressed via tags, not via subtyped `type` values.

| Directory | `type` value | Covers |
|-----------|-------------|--------|
| `actors/` | `Actor` | Countries, leaders, organizations, authors |
| `conflicts/` | `Conflict` | Wars, crises, sustained standoffs |
| `regions/` | `Region` | Geographic areas with independent dynamics |
| `themes/` | `Theme` | Cross-cutting topics, analytical frameworks |
| `events/` | `Event` | Discrete occurrences (explosions, summits, ceasefires) |

---

## 4. Frontmatter

### 4.1 Required fields

```yaml
type: Actor              # REQUIRED — one of the 5 types
```

### 4.2 Recommended fields

```yaml
title: United States     # Human-readable display name
description: <one-line summary>
tags: [country, military, nuclear]
status: ongoing           # Lifecycle state (see §6)
timestamp: 2026-07-02T00:00:00Z  # ISO 8601 last-modified
```

### 4.3 Extension fields

Producers MAY add any additional keys. Common extensions in this bundle:

```yaml
author: Velina Tchakarova       # For author actor concepts
source_url: https://...         # For events sourced from a single article
```

---

## 5. Naming Conventions

- **Kebab-case, descriptive**: `united-states.md`, not `us.md` or `UnitedStates.md`.
- **Year suffix for time-bound concepts**: `us-iran-war-2026.md`, not
  `2026-us-iran-war.md`. The year goes at the end, not as a date prefix.
- **Full English names for countries**: `united-states`, `united-kingdom`,
  `south-korea`. Short forms (`us`, `usa`) may appear in tags for discoverability.
- **Full names for authors**: `velina-tchakarova`, `phillips-obrien`.
- **Concept IDs**: Derived from the file path with `.md` removed.
  E.g., `actors/united-states.md` → concept ID `actors/united-states`.

---

## 6. Status Field

A custom frontmatter field indicating the lifecycle state of the concept.

| Value | Meaning | Examples |
|-------|---------|----------|
| `ongoing` | Actively evolving situation | US-Iran War, Global System Rupture, Taiwan standoff |
| `concluded` | Situation has ended; recorded for context | A past ceasefire, a concluded election |
| `evergreen` | Structural/enduring knowledge | Geography of Hormuz, energy fundamentals |
| `historical` | Past event recorded for historical context | Cold War, WWII |

For `ongoing` concepts, `timestamp` tracks the last update, and `log.md`
entries record what changed.

---

## 7. Body Section Conventions

The body uses standard markdown with conventional section headings:

| Heading | When to use |
|---------|-------------|
| `# Background` | Evergreen/structural context — geography, history, fundamentals. Always relevant. |
| `# Current Situation` | Time-bound description of the present state. Updated as things evolve. |
| `# Key Dynamics` | For regions/themes: the structural forces that shape the concept. |
| `# Analysis` | Dissolved analytical content (see §8). |
| `# Citations` | Numbered external sources. Always at the bottom of the document. |

Not all sections are required for every concept. Use what applies.

---

## 8. Analysis Dissolution

There is no `analyses/` directory. Analytical content from source articles is
**dissolved into the concepts it describes**, under `# Analysis` sections.

### 8.1 Format

Analysis sections use **thematic subsections** (organized by topic, not by
author). Multiple authors' perspectives are woven together in prose within each
subsection. Attribution is inline. Citations appear after each attributed claim.

```markdown
# Analysis

### Military Assessment
The US-Iran war revealed significant US military weakness. O'Brien notes poor
planning, failure to protect facilities, and inability to achieve strategic
objectives. [1] Tchakarova frames this within the broader Global System
Rupture, where US decline is a structural feature. [2]

### Technology and Cost Dynamics
Both O'Brien and Tchakarova identify the advantage of cheap mass systems over
expensive precision platforms. [1][2]
```

### 8.2 Author tracking

Recurring authors (3+ sources, or anticipated to reach that threshold) get
**actor concepts** in `actors/` that serve as indexes:

- Describe their analytical framework, worldview, recurring themes, and perspective.
- Link to all concepts where their analysis appears.

### 8.3 Frameworks that span multiple concepts

Analytical frameworks that apply broadly (e.g., "Global System Rupture",
"energy is power") become **theme concepts** in `themes/`, where the framework
itself is the concept.

---

## 9. Cross-linking

- **Absolute (bundle-relative) links** are preferred: `[US-Iran War](/conflicts/us-iran-war-2026.md)`.
- Links express relationships; the kind of relationship is conveyed by
  surrounding prose, not by the link itself.
- **Broken links are tolerated** — they represent not-yet-written knowledge.
- Link generously: every concept should connect to related actors, conflicts,
  themes, regions, and events.

---

## 10. Citations

- Citations are numbered and listed under `# Citations` at the bottom of each
  document.
- The primary citation is the **original article URL** (from the source's
  `source:` frontmatter field).
- Citation format:

```markdown
# Citations

[1] [Early Lessons From The US-Iran War](https://phillipspobrien.substack.com/p/early-lessons-from-the-us-iran-war)
[2] [Ceasefire in Iran](https://substack.com/@velinatchakarova/p-202096137)
```

---

## 11. Tag Vocabulary

Tags are used for subcategorization and cross-cutting filtering. The following
starter vocabulary MUST be used where applicable. New tags may be added as the
bundle grows, but existing tags should not be fragmented (e.g., use `energy`,
not `energy-policy`).

### 11.1 Actor subtypes

| Tag | Used for |
|-----|----------|
| `country` | Nation-states |
| `leader` | Individual political/military leaders |
| `organization` | International orgs, alliances, agencies, companies |
| `author` | Analysts, writers, publications whose interpretive work is tracked |

### 11.2 Thematic tags

`energy`, `military`, `technology`, `ai`, `ideology`, `economics`,
`cognitive-warfare`, `drone-warfare`, `nuclear`, `sanctions`, `trade`,
`demography`, `intelligence`, `critical-minerals`, `supply-chain`,
`naval`, `air-defense`, `missile`, `cyber`, `elections`

### 11.3 Regional tags

`middle-east`, `indo-pacific`, `europe`, `africa`, `latin-america`,
`central-asia`, `caucasus`, `sahel`, `baltic`, `black-sea`

### 11.4 Conflict character tags

`kinetic`, `gray-zone`, `cold-war`, `proxy`, `insurgency`, `hybrid`

### 11.5 Source-type tags (context only, not on concepts)

`news`, `opinion`, `framework` — used informally when describing an author's
output, not as concept tags.

---

## 12. Index Files

Each top-level directory has an `index.md` with no frontmatter (except the
root `index.md`, which has `okf_version`). Index files list all concepts in
the directory grouped by section, with one-line descriptions.

---

## 13. Log Files

`log.md` at the bundle root records the history of changes. Entries are
date-grouped, newest first, using ISO 8601 dates. The leading bold word
(`**Creation**`, `**Update**`, etc.) is a convention.

---

## 14. Source Handling

- The `sources/` directory contains raw articles and essays. It is NOT part of
  the OKF bundle.
- Concepts cite sources by their **original URL**, not by local file path.
- When a source is referenced in a concept's `# Citations` section, the URL
  from the source's `source:` frontmatter field is used.
- Author actor concepts list the sources that inform them, linking to the
  original URLs.
