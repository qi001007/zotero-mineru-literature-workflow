# Storage and preflight

## What to detect

Check for a usable Zotero desktop instance and a usable MinerU path before attempting the workflow. Prefer an explicitly available Zotero connector/MCP, then a running Zotero Local API with write authorization. Prefer an explicitly available MinerU MCP; a MinerU desktop/CLI may be used only if it can reliably produce a Markdown output folder.

State missing prerequisites plainly and provide official install pages. Do not claim that a browser extension, a citation database, OCR, or another converter is MinerU.

## Ask before path creation

Ask for a research root. Explain that the data directory configured inside Zotero is separate from linked research files. Do not assume a Windows drive letter or write research PDFs under a system/user home directory merely because it is convenient.

Validate that the proposed root is writable and has sufficient free space. If it already exists, preserve unrelated files. Create only:

```text
<research-root>/学术论文/
<research-root>/MinerU/
```

Use stable filename slugs such as `firstauthor-year-short-title.pdf`; use the same slug for the MinerU folder.

## Completion invariant

```text
<research-root>/学术论文/<slug>.pdf
<research-root>/MinerU/<slug>/full.md
Zotero parent item
  ├─ linked PDF attachment
  └─ linked Markdown attachment
```

Any missing edge makes a paper incomplete, even when its citation exists in Zotero.

