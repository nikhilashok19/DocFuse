# DocFuse — PDF & Image Combiner

> A zero-dependency, browser-based tool to merge PDFs and images into a single high-resolution PDF — with grayscale scan and CamScanner-style Enhanced B&W modes. No server. No upload. No install.

---

## ✨ Features

| Feature | Details |
|---|---|
| **Multi-file upload** | Drag & drop or click-to-browse. Accepts `.pdf`, `.jpg`, `.jpeg`, `.png` |
| **Sequential merge** | Files combine in the exact order shown in the queue |
| **Drag-to-reorder** | Grab any row and drag it to rearrange before combining |
| **Grayscale Scan mode** | Soft luminance conversion with mild contrast boost — ideal for clean documents destined for printing |
| **Enhanced B&W mode** | Adaptive local-threshold algorithm (CamScanner "Magic Color" style) — whitens backgrounds, deepens ink, compensates for uneven lighting and shadows |
| **PDF thumbnails** | First page of each uploaded PDF is previewed inline |
| **High-res output** | Pages rasterized at 2× scale before re-embedding for sharp output |
| **Pure client-side** | All processing happens in your browser via `pdf-lib` and `PDF.js`. Nothing leaves your device. |

---

## 🚀 Getting Started

No build step, no dependencies to install.

```bash
git clone https://github.com/your-username/docfuse.git
cd docfuse
```

Then just open `pdf-combiner.html` in any modern browser:

```bash
# macOS
open pdf-combiner.html

# Linux
xdg-open pdf-combiner.html

# Windows
start pdf-combiner.html
```

Or serve it locally if you prefer:

```bash
npx serve .
# then visit http://localhost:3000
```

---

## 🖥️ Usage

1. **Upload files** — drag them onto the drop zone or click to browse. Mix PDFs and images freely.
2. **Reorder** — drag rows in the queue to set the final page sequence.
3. **Choose a colour mode** (optional, mutually exclusive):
   - **Grayscale Scan** — converts everything to soft grey tones with a light contrast boost.
   - **Enhanced B&W** — runs an adaptive threshold to produce pure white backgrounds and deep black ink, mimicking CamScanner's "Magic Color / Enhanced" output. Best for scanned documents, whiteboards, and handwritten notes.
4. **Click "Combine & Download"** — a progress bar tracks each file. The merged `.pdf` downloads automatically when done.

---

## 🎨 Colour Mode Details

### Grayscale Scan
Standard luminance-weighted greyscale (`0.299R + 0.587G + 0.114B`) with a mild S-curve contrast enhancement. Preserves tonal gradients — good for photos or colour PDFs that need a print-friendly greyscale version.

### Enhanced B&W (Magic Color)
A multi-step adaptive pipeline inspired by document-scanning apps:

1. Convert to greyscale
2. Estimate local background brightness per pixel using a fast separable box-blur (integral image, ~4% of image dimension radius)
3. Compare each pixel's luminance against its local background
4. **Ink pixels** (darker than surroundings) → pushed to deep black (0–60)
5. **Background pixels** (lighter than surroundings) → pushed to near-white (230–255)

The result compensates for shadows, coffee stains, yellowed paper, and uneven lighting automatically — without any manual threshold tuning.

---

## 🛠️ Tech Stack

| Library | Version | Purpose |
|---|---|---|
| [pdf-lib](https://pdf-lib.js.org/) | 1.17.1 | PDF creation, merging, and image embedding |
| [PDF.js](https://mozilla.github.io/pdf.js/) | 3.11.174 | Rasterizing PDF pages to canvas for image-mode processing |

Both are loaded from `cdnjs.cloudflare.com`. No npm, no bundler, no framework.

---

## 📁 Project Structure

```
docfuse/
└── pdf-combiner.html   # The entire tool — HTML + CSS + JS in one file
└── README.md
```

---

## 🌐 Browser Compatibility

| Browser | Support |
|---|---|
| Chrome / Edge 90+ | ✅ Full |
| Firefox 90+ | ✅ Full |
| Safari 15+ | ✅ Full |
| Mobile Chrome / Safari | ✅ Works (desktop layout recommended) |

Requires support for: `File API`, `Canvas API`, `ArrayBuffer`, `Blob URLs`.

---

## ⚠️ Known Limitations

- **Encrypted PDFs** are loaded with `ignoreEncryption: true` — content may not render correctly if the PDF has strict DRM.
- **Very large files** (100+ MB PDFs) may be slow in the browser due to canvas rasterization at 2× scale. This is a browser memory constraint, not a bug.
- **Enhanced B&W on colour PDFs** rasterizes each page — the output file will be larger than the original since vector content is converted to images.

---

## 🤝 Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you'd like to change.

```bash
# Fork the repo, make your changes to pdf-combiner.html, then open a PR
```

---

## 📄 License

[MIT](LICENSE) — free to use, modify, and distribute.

---

<p align="center">Made with DocFuse — local, private, instant.</p>
