# Recovery status and provenance

Recovery date: **October 28, 2026**.

Primary source: [Alia_Maluya_BCA153 — original published project page](https://sites.google.com/g.msuiit.edu.ph/aliamaluyabca153finalproject/home?read_current=1).

## What was recovered

| Material | Recovery status |
| --- | --- |
| PLC_PRG listing under FULL CODE | Recovered from the published HTML text; not a native export |
| HMI and alarm screenshots, Figures 1–2 | Recovered from the rendered public page and preserved as image files |
| Project-tree screenshot, Figure 3 | Recovered as an image; configuration itself unavailable |
| Embedded demonstration, Figure 4 | YouTube link recovered; video not copied or independently reviewed |
| Flowchart, Figure 5 | Original published image recovered |
| Design, variables, testing descriptions, credits | Summarized from the published report with source links |
| Native CODESYS project and configuration | Not recovered; owner reports original files lost after reformat |

## Source recovery procedure

The public page HTML was retrieved for inspection. Scripts and styles were excluded from text extraction, HTML entities decoded, and block boundaries represented as line breaks. The text from `PROGRAM PLC_PRG` through the end of the FULL CODE listing was saved as [PLC_PRG.published.txt](../provenance/PLC_PRG.published.txt). It is an extracted text record, not a byte-for-byte copy of the HTML or a verified copy of the lost original project.

The [Structured Text file](../src/recovered/PLC_PRG.st) was derived only by replacing nonbreaking spaces with ordinary spaces and removing the report's standalone hyphen-divider line between declarations and implementation. Line endings are LF. Comments, assignments, conditions, values, ordering, and missing punctuation were preserved. The combined declaration/body presentation follows the web report; it is not an importable CODESYS project export.

Images were downloaded from the public page through the browser's image-download facility, copied with descriptive filenames, and visually inspected. No cropping, enhancement, redrawing, or generated replacement was applied. An initial direct image request from a separately fetched page returned HTTP 403; the rendered public page loaded its current image URLs normally, and those were used for recovery.

The original page snapshot was used only for local inspection and is not published in this repository, since it includes unrelated Google Sites scripts and metadata. Its hash is recorded as a local inspection reference, not as a downloadable repository artifact. Image URLs can be transient; the source page, figure number, local file hash, and visible content provide the durable context.

[sources.json](../provenance/sources.json) records the recovered artifact inventory, source URLs, transformations, and SHA-256 hashes. Hashes establish the bytes captured during this recovery, not authorship, original creation time, permission, or equivalence to lost files.

## Missing context

The exact CODESYS version, native project, HMI event bindings, alarm definitions/classes/acknowledgement settings, library versions, task timing, runtime configuration, and detailed test logs were not recovered. The project-tree screenshot shows some component names but does not restore their settings.

The published source was not compiled or executed during this recovery. Screenshot states, report prose, and source listing may not represent one identical build. Known discrepancies are recorded in [code-review.md](code-review.md).

## Attribution and permission

The published report identifies Kent Alia and John Paul Maluya as the team. Individual contribution roles are not available. The owner confirmed Kent does not object to copying the group's published code and screenshots into this portfolio repository. See [CREDITS.md](../CREDITS.md) and [RIGHTS.md](../RIGHTS.md) for the scope and limits of this record.

New summaries and the README's Mermaid diagram were prepared with AI assistance for this archive. The Mermaid diagram is a new summary based on the published sequence, separate from the preserved original Figure 5. No newly generated code is labeled as recovered source.
