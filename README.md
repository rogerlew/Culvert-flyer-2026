# CULVERT Workshop Flyer — 2026

Editable LaTeX flyer for the December 3, 2026 virtual workshop on culvert vulnerability assessment research, with details of the January 10, 2027 in-person opportunity.

## Files

- `Culvert_Workshop_Flyer_Redesigned.tex`: editable flyer source.
- `Culvert_Workshop_Flyer_Redesigned.pdf`: original reference PDF. Builds do not overwrite this file.
- `culvert-photo.png` and `culvert-manual.png`: flyer images.
- `flyer-assets/`: four partner logos extracted from the reference PDF.
- `output/pdf/Culvert_Workshop_Flyer_Redesigned.pdf`: rendered LaTeX flyer.

## Required software

Install a TeX distribution with **XeLaTeX**, such as MacTeX on macOS or TeX Live on Linux/Windows. A full installation includes the dependencies used here:

- LaTeX packages: `geometry`, `fontspec`, `graphicx`, `tikz` (provided by `pgf`), and `hyperref`.
- Inter OpenType fonts: the TeX Live `inter` package, including `Inter-Regular.otf`, `Inter-Bold.otf`, `Inter-Italic.otf`, and `Inter-SemiBold.otf`.

For a minimal TeX Live installation managed by `tlmgr`, install missing packages with:

```sh
tlmgr install xetex geometry fontspec graphics pgf hyperref inter
```

Use your operating system's package manager instead if it manages your TeX Live installation. Ensure the TeX binaries are on your `PATH`; MacTeX normally exposes them through `/Library/TeX/texbin`.

Check the compiler and font installation:

```sh
xelatex --version
kpsewhich Inter-Regular.otf
```

Poppler is optional; its `pdftoppm` utility can render the PDF to PNG for visual review. Python and external image-generation tools are not required to build the flyer.

## Build

Run from the repository root, keeping the images and `flyer-assets/` beside the `.tex` file:

```sh
mkdir -p output/pdf
xelatex -interaction=nonstopmode -halt-on-error -output-directory=output/pdf Culvert_Workshop_Flyer_Redesigned.tex
xelatex -interaction=nonstopmode -halt-on-error -output-directory=output/pdf Culvert_Workshop_Flyer_Redesigned.tex
```

**Run both passes.** TikZ needs the second pass to resolve page anchors; a first build can otherwise produce a blank page.

Open `output/pdf/Culvert_Workshop_Flyer_Redesigned.pdf` in a PDF viewer. On macOS:

```sh
open output/pdf/Culvert_Workshop_Flyer_Redesigned.pdf
```

The flyer was verified with XeLaTeX from TeX Live 2025.

## Editing and visual review

Edit the text directly in the commented sections of the `.tex` file. Colors are defined near the top. The `\block{x}{y}{width}{content}` helper positions editable text panels in PDF points, measured from the upper-left corner. Text wraps inside each panel; the panel positions are fixed to preserve the single-page US Letter design.

After changing wording, font sizes, or images, rebuild and inspect the entire page for overflow, clipping, spacing, and legibility. Longer text may require adjusting panel positions or widths. The email address, project website, manual cover, and research article have clickable links defined with `\href`.

For an optional image preview using Poppler:

```sh
pdftoppm -scale-to 1600 -png -singlefile output/pdf/Culvert_Workshop_Flyer_Redesigned.pdf output/pdf/flyer-preview
```

Inspect `output/pdf/flyer-preview.png`. Build logs, auxiliary files, and this preview are ignored by Git; the source, image assets, reference PDF, and rendered PDF can be committed.
