# Third-party notices

Argonaut's own code is licensed under the MIT License; see `LICENSE`.

The browser libraries below are redistributed unmodified in `vendor/` so that
PDF import and OCR work without a network connection. They remain under their
own licenses.

| Component | Version | License | Upstream |
|---|---|---|---|
| PDF.js (`vendor/pdfjs/`) | 3.11.174 | Apache-2.0 | https://github.com/mozilla/pdf.js |
| Tesseract.js (`vendor/tesseract/`) | 5.1.1 | Apache-2.0 | https://github.com/naptha/tesseract.js |
| tesseract.js-core (`vendor/tesseract/core/`) | 5.1.1 | Apache-2.0 | https://github.com/naptha/tesseract.js-core |
| English traineddata (`vendor/tesseract/lang/eng.traineddata.gz`) | 4.0.0 | Apache-2.0 | https://github.com/tesseract-ocr/tessdata |

A copy of the Apache License, Version 2.0 is in `licenses/Apache-2.0.txt`.

No changes were made to the vendored files. If a vendored file is missing from
a deployment, the page falls back to the same pinned versions on
`cdnjs.cloudflare.com` (PDF.js) and `cdn.jsdelivr.net` (Tesseract.js).

Tesseract is a trademark of Google LLC. PDF.js is a project of Mozilla.
`eng.traineddata` training data is part of the Tesseract OCR project. All
names are used only to identify the components.
