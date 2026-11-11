# Argonaut

Open-source and rule-based patent claims analysis tools. A single-page workspace for 
reading patent claims, charting them against evidence, comparing versions, reviewing
potential weak points, and mapping dependencies.

No backend, no account, no build step. Case data stays in this browser
(`localStorage`), and no claim text or document is uploaded.

> **Litigation aid, not legal advice.** Argonaut flags potential issues and
> records your own analysis. It does not decide infringement, validity, claim
> construction, or scope, and it does not replace review by a qualified patent
> litigator or patent professional. Findings are prompts for review, never
> conclusions. Verify every result against the current law and the record.

## What is included

- **Claim chart** — split a claim into elements and record evidence, exhibit and
  pinpoint references, a verdict, and notes. Infringement/FTO and validity chart
  types, named references and embodiments, a priority-date warning, and
  Markdown/CSV exports.
- **Claim comparison** — word- and character-level redline with inline or
  side-by-side views, four comparison framings (original vs amended, granted vs
  application, two versions, claim vs prior art), feature-change and overlap
  views, and optional EPC support checks for amendments.
- **Claim review** — rule-based findings for the selected jurisdiction, with
  per-issue dismissal, sorting, grouping, copying, and Markdown/CSV export. A
  specification field enables definition and support checks. Send a term to the
  construction (US) or interpretation (EPC) list.
- **Claim tree** — dependency forest with independent/dependent/orphan status,
  orphan and multiple-dependent-claim detection, and normal or expanded
  Markdown exports.

Two jurisdictions share one code path:

- **United States** — six review headings: eligibility, definiteness,
  description, enablement, structure, and consistency.
- **Europe (UPC)** — 13 EPC review sections, including added subject-matter and
  extension-of-protection hints.

The mode changes rule selection, labels, vocabulary, and export headers; it does
not change the stored case data.

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

## Patent-number lookup

Each claim box has a lookup for a patent number such as `US 10,000,000 B2`.
Argonaut normalises the number, reuses a browser-cached copy when available, and
otherwise tries to read the public patent page. Most patent servers block
cross-origin reads, so the fallback is a paste dialog: open the patent page,
copy its claims, and Argonaut extracts and numbers them locally. Only the patent
number is sent; claim text is not.

## Privacy

- No accounts, telemetry, analytics, or automatic updates.
- No AI, no model calls, and no server-side processing.
- Claim text, PDFs, and OCR output stay in the tab. PDF and OCR libraries are
  served from this site (or, only if a vendored file is missing, from their
  public CDNs).
- State is kept in `localStorage`; clearing site data clears the workspace. Use
  the Markdown, CSV, and Word exports for durable copies.

## Run locally

From this folder:

```sh
python -m http.server 8000
```

Then open <http://localhost:8000>. Any static file server works. Opening
`index.html` directly is fine for pasted text, but PDF import and OCR need the
HTTP origin.

Exports build `.docx`, Markdown, and CSV files in the browser. Print styles hide
the controls so printouts show the analysis only.

## Publish with GitHub Pages

1. Create a new **public** repository on GitHub. Do not add a README or
   `.gitignore` there; this folder already has them.
2. On the repository page, choose **Add file → Upload files**, then drag the
   **contents** of this folder into the browser (not the folder itself), or
   upload the provided ZIP, extract it locally, and drag the extracted
   contents. Keep the `vendor/` folder structure intact.
3. Make sure `.nojekyll` is present at the repository root. If your browser
   hides dotfiles during upload, use **Add file → Create new file**, name it
   `.nojekyll`, leave it empty, and commit.
4. Open **Settings → Pages**. Under **Build and deployment**, choose
   **Deploy from a branch**, branch **main**, folder **/ (root)**, and save.
5. Wait for the Pages URL, then open it and check that the sidebar reports
   **PDF + OCR ready**. Import a text PDF and a scanned PDF to confirm both
   paths.

All paths in the page are relative, so it works from a project site
(`https://<user>.github.io/<repo>/`) as well as a user site.

## Project layout

```text
index.html                     the complete application
vendor/pdfjs/                  PDF.js 3.11.174 + worker
vendor/tesseract/              Tesseract.js 5.1.1 + worker
vendor/tesseract/core/         WASM core (SIMD and non-SIMD LSTM builds)
vendor/tesseract/lang/         English traineddata
LICENSE                        MIT (Argonaut's own code)
THIRD-PARTY-LICENSES.md        bundled components and their licenses
licenses/Apache-2.0.txt        Apache License 2.0 text
```

## Known limits

- The checker is a heuristic aid; it will miss issues and can produce false
  positives. Litigation relevance lines are prompts, not advice.
- Chart verdicts, comparison prompts, support and basis checks, and scope hints
  are descriptive.
- Antecedent-basis checks are English-centric. The tree parses German and French
  dependency phrases, but the checker reviews English claim language only.
- EP feature classification, added-subject-matter and extension-of-protection
  hints, and the basis table are heuristics.
- Status labels and dependency notes are user annotations, not legal findings.
- PDF extraction depends on the text layer and OCR quality. Always review
  extracted claims before running any check.
- No automatic updates, accounts, or external processing.

## License

Argonaut's own code is released under the [MIT License](LICENSE). Bundled
third-party libraries are Apache-2.0; see
[THIRD-PARTY-LICENSES.md](THIRD-PARTY-LICENSES.md).
