# LLM Wiki Schema

This document defines the schema, structure, and operations for this LLM-maintained knowledge base.

## Core Principles

1. **Raw Sources (`raw/`)**: Immutable files (papers, articles, transcripts). The LLM reads these but NEVER modifies them.
2. **The Wiki**: A structured collection of markdown files maintained entirely by the LLM. 
3. **The Schema (`AGENTS.md`)**: The configuration file that dictates conventions and workflows (this file).

## Operations

### 1. Ingesting New Sources

When you add a new source to `raw/` and ask the LLM to process it, the LLM will:

- Read the source and discuss key takeaways with you if instructed.
- Write a dedicated summary page for it in the `wiki/` directory.
- Update `index.md` with a link to the new page and a one-line summary.
- Update any relevant entity or concept pages logically connected to this source.
- Append an ingest entry to `log.md`.

### 2. Querying the Wiki

When you ask a complex question:

- The LLM will first read `index.md` to discover relevant pages.
- It will read those specific pages.
- It will synthesize an answer, heavily referencing existing wiki knowledge.
- Render outputs as standard Markdown, or if requested by the user, as Derived Outputs (e.g., Marp slide decks, matplotlib charts).
- If the synthesis is highly valuable, the LLM will propose filing it back into the wiki as a new concept/analysis page. Every exploration adds up!

### 3. Linting and Maintenance

When you ask the LLM to "lint the wiki" or "health-check":

- It will check for contradictions between pages.
- It will flag orphan pages (no inbound links).
- It will check for missing cross-references and ensure overall semantic consistency.
- It will impute missing information via web search.
- It will actively find connections between concepts to suggest new articles.

## File Structure Conventions

- All wiki pages should have a clear descriptive title.
- Link between pages using relative markdown paths. CRITICAL: Do NOT use Obsidian-style `[[WikiLinks]]`. ALL links must be formatted as standard Markdown relative paths (e.g., `[Title](../concepts/Concept_Name.md)`).
- All generated files (summaries, derived outputs, analyses) MUST be placed in designated subdirectories (e.g., `wiki/`, `outputs/`), and never directly in the project root.
- Avoid deleting history unless instructed; prefer to update and document evolving understanding.
