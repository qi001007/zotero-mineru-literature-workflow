# Zotero linked-file integration

## Preferred integration order

1. Use an available Zotero MCP/connector that supports linked-file creation and readback.
2. Otherwise use Zotero's authorized Local API if the desktop app exposes it.
3. Only if neither backend route can create links, use the Zotero UI with the user's permission.

Never alter `zotero.sqlite` directly. Zotero's database and storage are application-owned and direct writes are unsafe.

## Linked files, not managed copies

The required attachment mode is a **linked file**, pointing to the existing absolute PDF or Markdown path. It should not upload, duplicate, or relocate the research file.

Use descriptive attachment titles, e.g. `PDF — <short title>` and `MinerU Markdown — <short title>`. Use `application/pdf` for the PDF and `text/markdown` for `full.md` when the integration exposes a content type.

## Local API requirements

Zotero Local API write requests require current user authorization. Treat local API keys and server identifiers as secrets: never print them in chat, logs, repository files, or commits. After a create request, request the parent's children and verify the link mode, paths, and count.

## UI fallback

When manual interaction is necessary, select the parent item, then use its context menu's command equivalent to **Add Link to File…**. Add the PDF and `full.md` separately. Confirm the two child attachments appear under the parent before moving to the next item.

