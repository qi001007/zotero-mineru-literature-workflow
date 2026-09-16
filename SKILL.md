---
name: zotero-mineru-literature-workflow
description: Set up or run a Zotero and MinerU workflow that stores legal local PDFs, converts each PDF to Markdown, and links both files to the corresponding Zotero item. Use for research literature collection, PDF-to-Markdown preparation, or Zotero linked-file management; do not use for citation-only tasks.
---

# Zotero + MinerU Literature Workflow

Use this skill to build a **readable local literature library**, not merely a list of citations. The successful unit is one paper with a verified local PDF, a MinerU-generated Markdown file (normally `full.md`), and two child linked-file attachments on the matching Zotero parent item. Never count metadata-only records as completed full-text papers.

## 1. Preflight before changing files

Inspect the available tools and local environment first. Determine separately whether Zotero desktop is installed and running with a connector/MCP/local API that can write attachments, MinerU is available through an MCP/CLI/supported app integration, and the user has a writable destination for research files.

If Zotero or MinerU is missing, state exactly which capability is absent, give the official installation route, and stop before creating library records or directories that imply the workflow is ready. Do not silently substitute another PDF-to-text tool for MinerU. Do not install software, alter Zotero's data directory, or move an existing library without explicit approval.

## 2. Ask for storage choices

Before the first download or conversion, ask the user to choose paths. Distinguish:

- **Zotero application**: the program installation; normally leave it at the operating system default.
- **Zotero data directory**: Zotero's database, index, and managed attachments; do not relocate it merely because a different drive is preferred.
- **Research files managed by this workflow**: request a root folder, then use two sibling folders:

```text
<research-root>/
├─ 学术论文/     # original, verified PDFs
└─ MinerU/        # one directory per PDF, including full.md and extracted assets
```

Offer a non-system drive when space is a concern, but let the user choose. Do not create redundant `source`, `export`, or duplicate library folders unless asked. Read [storage-and-preflight.md](references/storage-and-preflight.md) when validating paths or explaining this separation.

## 3. Build or select Zotero records

Create/select a clearly named Zotero collection with user approval. For each paper, use a real parent bibliographic item, preferably imported from DOI/ISBN/arXiv metadata and checked for title, authors, year, and identifier. Do not create duplicate parent items solely because a local PDF is being added. If a preprint is used because the publisher PDF is unavailable, preserve the published DOI and record the preprint URL/version clearly.

## 4. Acquire and validate full text

Use legal sources only: publisher open-access pages, institutional repositories, author-provided preprints, or arXiv. Respect paywalls and access controls. A landing page, login page, CAPTCHA response, or HTML error page is not a PDF.

For every downloaded candidate, write it under `学术论文/` with a stable ASCII-safe filename, verify a non-trivial size and the `%PDF` signature, and remove only the just-created invalid candidate file if validation fails. Report unavailable full text separately instead of treating it as done. Do not close-read a paper until its verified PDF has been converted with MinerU.

## 5. Convert using MinerU

For every verified PDF, create a unique, empty paper directory in `MinerU/`, then invoke MinerU with that directory as its output. Confirm that `full.md` exists and is non-empty before adding a Markdown attachment. Keep each conversion folder next to its paper identity rather than mixing all Markdown files together.

## 6. Link files into Zotero

Attach two **linked files** beneath the parent item: the local PDF (`application/pdf`) and the local Markdown (`text/markdown`, normally `full.md`). Use absolute paths. Prefer Zotero's connector/MCP or authorized Local API. Never write directly to `zotero.sqlite`; direct database writes can corrupt the library. If automation cannot create linked attachments, explain the fallback UI action (right-click parent item → add/link file attachment) and request permission before driving the UI.

Read [zotero-linking.md](references/zotero-linking.md) for API and fallback details.

## 7. Verify and report

After writes, read back each parent item and verify exactly two intended linked attachments with paths that exist on disk. Report four numbers separately: parent metadata records, verified local PDFs, MinerU `full.md` files, and Zotero parents with both links.

If the user asks for a target count, report the fulfilled count and a separate list of papers blocked by access, broken conversion, or missing metadata. Never inflate completion by including candidate-only records.

## Security and portability

Do not embed local API keys, account IDs, local paths, collection IDs, or personal names in the skill, a repository, or a final report. Obtain credentials through the active Zotero authorization mechanism each time. Keep all filesystem behavior configurable from the user's chosen root.

