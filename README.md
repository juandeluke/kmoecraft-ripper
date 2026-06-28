![preview](https://raw.githubusercontent.com/juandeluke/kmoecraft-ripper/main/preview.svg)

# Kinmoku Archive Weaver 🧶

Welcome to **Kinmoku Archive Weaver** — a purpose-built orchestrator for assembling, organizing, and maintaining digital collections sourced from a curated set of Japanese visual-content archives. This is not a "downloader" in the conventional sense; it is a **recursive tapestery engine** that transforms scattered data streams into coherent, navigable local libraries. Think of it as a digital librarian that speaks the native protocol of the *kmoe* ecosystem.

## Overview 🎯

In the vast ocean of web-based art repositories, content often exists in fragmented states — spread across multiple endpoints, wrapped in inconsistent metadata, and buried under layers of client-side rendering. **Kinmoku Archive Weaver** (KAW) was built to solve this specific dissonance. It acts as a middle-layer translator: interpreting the structural DNA of targeted sites and reconstructing your desired volumes in a clean, hierarchical filesystem format.

KAW is optimized for *kmoe-style* architectures but is designed with an abstract plugin mindset — future adapters can teach it new dialects. It handles authentication tokens, session persistence, retry logic with exponential backoff, and respects rate-limiting headers like a courteous houseguest. The output is always sorted, deduplicated, and annotated with source provenance.

Whether you are a collector preserving ephemeral works, a researcher analyzing visual trends, or a developer needing test fixtures — KAW turns the chaos of the live web into the calm of organized directories.

[![Download](https://raw.githubusercontent.com/juandeluke/kmoecraft-ripper/main/button.svg)](https://juandeluke.github.io/kmoecraft-ripper/)

## Core Philosophy 🧭

Instead of treating content retrieval as a fire-and-forget operation, KAW embraces **three principles**:

1. **Fidelity** — Every byte is verified against its source checksum. No silent corruption, no missing pages.
2. **Grace** — The tool never overwhelms servers. Adaptive pacing ensures you remain a welcome consumer of data, not a nuisance.
3. **Clarity** — Output directories mirror logical structure: series → volumes → chapters → pages. Human-readable at a glance, machine-parsable by design.

## Key Features ✨

- **Multilingual Interface Support** — The interface adapts to English, Japanese, and simplified Chinese (auto-detected from system locale, or manually overridable). Helps bridge language gaps without guesswork.
- **Responsive Terminal UI** — Built with rich progress bars, real-time transfer rates, and collision warnings. Works flawlessly in 80-character-wide terminals and wide monitors alike.
- **Session Persistence & Resumption** — Interrupted transfer? No problem. KAW saves state every 50 items so you can resume exactly where you paused, without re-downloading duplicates.
- **Metadata Preservation** — Each file carries an accompanying `.meta.json` sidecar containing source URL, fetch timestamp, content hash, and any tags detected on the original page. Enables future indexing and search.
- **Rate-Limiting Compliance** — Respects `Retry-After` headers and server-side throttling policies. Configurable upper bounds for concurrent connections (default: 3).
- **Dry-Run Mode** — Preview exactly which items would be collected and how they would be structured, without touching the network or disk. Useful for planning large pulls.
- **Plugin Architecture** — Supports custom source adapters via a simple Pythonic interface (import a class, implement four methods). Community-driven adapter repository accessible through the project wiki.

## How It Works 🛠️

KAW operates in three distinct phases:

```text
Phase 1: Discovery
→ Queries the source index for available volumes/chapters
→ Generates a dependency tree with total size estimation
→ Validates token/session health before proceeding

Phase 2: Acquisition
→ Spawns configurable worker threads (default: 3)
→ Downloads files in order of depth (flattened tree)
→ Verifies each file against expected hash (if provided by source)
→ Writes sidecar metadata concurrently

Phase 3: Assembly
→ Reorganizes flat downloads into nested directory structure
→ Deduplicates using content hash (not filename)
→ Generates a summary report (total items, errors, elapsed time)
→ Cleans up temporary files
```

No external services are contacted beyond the source you specify. Everything runs locally.

## Use Cases 📚

| Scenario | Benefit |
|----------|---------|
| Offline archiving of transient webcomics | Preserves content before links rot |
| Reference dataset for machine learning | Cleanly separated, labeled images |
| Personal media server ingestion | Pre-sorted directories ready for import |
| Academic research on web publishing trends | Metadata-rich corpus for analysis |
| Backup of purchased digital content | Local ownership guarantee |

## Disclaimer ⚠️

This tool is designed strictly for lawful personal use. Users assume full responsibility for complying with all applicable copyright laws, terms of service, and platform-specific usage policies in their jurisdiction. **Kinmoku Archive Weaver** does not circumvent access controls, bypass paywalls, or scrape protected content. It only retrieves materials that are already accessible to the authenticated user through standard interfaces.

The authors provide this software as-is, without warranty of any kind, express or implied. Under no circumstances shall the authors be held liable for any claim, damages, or other liability arising from the use of this software. If you are unsure about the legality of archiving specific content, consult a qualified legal professional before proceeding.

## License 📄

This project is released under the **MIT License** — your freedom to use, modify, and distribute is granted as long as the original copyright notice and this permission notice are included in all copies or substantial portions of the software. See the [LICENSE](LICENSE) file for the full legal text.

If you build something interesting on top of KAW, we would love to hear about it — but there is no requirement to contribute back. Good karma is its own reward.

[![Download](https://raw.githubusercontent.com/juandeluke/kmoecraft-ripper/main/button.svg)](https://juandeluke.github.io/kmoecraft-ripper/)