# PDFrigged

A PDF toolkit I built because I didn't want to keep paying for one.

Every free online converter either watermarks the output, caps the file size, or uploads your document to someone else's server. I needed merge, split and sign often enough that a subscription started to look reasonable — so I built the tool instead. It's been my daily driver since.

**Live:** web app · also shipped to iOS and Android via Capacitor from the same codebase.

---

## What it does

| Tool | |
|---|---|
| **Merge** | Combine multiple PDFs, reorder before export |
| **Split** | Extract page ranges into separate documents |
| **Compress** | Reduce file size for upload limits |
| **Sign** | Draw a signature on canvas and place it on the page |
| **Scanner** | Capture pages with the device camera and build a PDF |
| **JPG → PDF** | Batch images into a single document |
| **PDF → JPG** | Render pages out as images |
| **AI PDF tools** | LLM-assisted operations over document content |

---

## How it's built

Rendering and manipulation run **client-side** — `pdf-lib` for document construction, `pdfjs-dist` for rendering. Files don't leave the device for the core operations, which was the point: the tools I was replacing all required an upload.

The same Next.js codebase ships to mobile through **Capacitor**, using native plugins for camera capture, filesystem access and the share sheet rather than reimplementing a mobile client.

```
src/
├── app/           route per tool — merge_pdf, split_pdf, sign_pdf, scanner, …
├── features/      tool logic, isolated per capability
├── components/    shared UI
├── context/       app-level state
└── lib/ utils/    PDF helpers
```

**Stack:** Next.js · TypeScript · Tailwind · pdf-lib · pdfjs-dist · react-signature-canvas · react-webcam · react-image-crop · Framer Motion · Capacitor (iOS + Android)

---

## Running it

```bash
npm install
npm run dev          # http://localhost:3000
```

Mobile builds:

```bash
npm run build
npx cap sync
npx cap open ios     # or: npx cap open android
```

---

Built by [Yash Rawal](https://github.com/yaashhrawal).
