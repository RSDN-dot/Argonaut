# Argonaut

Open-source and rule-based patent claims analysis tools. A single-page workspace for 
reading patent claims, charting them against evidence, comparing versions, reviewing
potential weak points, and mapping dependencies.

No backend, no account, no build step. Data stays in this browser
(`localStorage`), and no claim text or document is uploaded.

> Argonaut is a support tool for patent analysis.
It does not replace review by a qualified lawyer or patent attorney. Verify every
result against the current law and the record.

## What is included

- **Claim chart** to map patent claims.
- **Claim comparison** to compare claim versions word by word, down to the character.
- **Claim review** with rule-based findings to assess potential weak points under US practice.
- **Claim tree** to see the dependency structure of every claim, with each dependent
  claim sitting under its parent.

Two jurisdictions share one code path:

- **United States** 6 review headings: Eligibility, Definiteness,
  Description, Enablement, Structure, and Consistency.
- **EPC** 13 EPC review sections based on the EPO guidelines on patentability: Technical, Two-part form,
  Category, Clarity, Antecedent, Relative terms, Optional features, Result / negative, References, Parameters,
  Support, Conciseness, Numbering / form.

The mode changes rule selection, labels, vocabulary, and export headers.

## PDF import and OCR

Claim text can be pasted, read from a PDF's text layer, or read from a scanned
PDF with OCR. PDF.js and Tesseract.js are **bundled in `vendor/`**, together
with the Tesseract worker, WASM core, and English language data, so PDF reading
and OCR do not need a network connection.

- Text-layer PDFs are used directly.
- Scanned pages are OCR'd automatically when the text layer is unusable; **Force
  OCR** re-reads every page.
- OCR language data is cached by the browser after the first run.
- If a vendored file is missing, the page falls back to the same pinned
  versions on cdnjs/jsDelivr. The library status pill in the sidebar reports
  whether PDF and OCR are ready.

Browsers block the background workers used by PDF.js and Tesseract.js on
`file://` pages, so run the app from a local web server or from the hosted site
when you need PDF import or OCR. Pasted text works either way.

## Privacy

- No accounts, telemetry, analytics, or automatic updates.
- No AI, no model calls, and no server-side processing.
- Claim text, PDFs, and OCR output stay in the tab. PDF and OCR libraries are
  served from this site (or, only if a vendored file is missing, from their
  public CDNs).
- State is kept in `localStorage`; clearing site data clears the workspace. Use
  the Markdown, CSV, and Word exports for durable copies.

## Known limits

- The Claim review tool is a heuristic aid; it will miss issues and can produce false
  positives.
- Chart verdicts, comparison prompts, support and basis checks, and scope hints
  are descriptive.
- Antecedent-basis checks are English-centric. The tree parses German and French
  dependency phrases, but the checker reviews English claim language only.
- EP feature classification, added-subject-matter and extension-of-protection
  hints, and the basis table are heuristics.
- PDF extraction depends on the text layer and OCR quality. Always review
  extracted claims before running any check.
- No automatic updates, accounts, or external processing.

## License

Argonaut's own code is released under the [MIT License](LICENSE). Bundled
third-party libraries are Apache-2.0; see
[THIRD-PARTY-LICENSES.md](THIRD-PARTY-LICENSES.md).
