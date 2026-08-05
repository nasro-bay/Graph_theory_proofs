# Task: Convert handwritten math lecture notes (PDF) into styled LaTeX

## Input
A PDF of handwritten lecture notes (photographed pages), e.g. `Colouring_Graphs.pdf`.
Each PDF is one chapter/topic.

## Output
A single `.tex` file per chapter, using the template and style rules below, that
compiles cleanly with `pdflatex` (no manual fixes needed).

## Step 1 — Read and transcribe
- Read every page of the PDF as an image (do not skip pages).
- Transcribe the mathematical content faithfully: theorem statements, proofs,
  definitions, remarks, in the same order as the notes.
- Fix obvious handwriting artifacts (crossed-out words, stray strokes) — do not
  transcribe struck-through text.
- If a theorem/result is stated but the notes give no proof (e.g. a named theorem
  like Brooks' Theorem or the Four Colour Theorem left unproved), do NOT invent
  a proof. Mark it with a `remark` noting the proof was not included in the
  original notes.
- Clean up notation into proper LaTeX math (e.g. `X(G)` → `\chi(G)`, `<=` → `\leq`).
- Preserve the logical structure: number theorems in the order they appear.

## Step 2 — Identify figures
Every hand-drawn diagram becomes a **TikZ figure**, not an embedded image, when it's
a graph-theory diagram (vertices/edges — small graphs, degree diagrams, contraction
steps, K5, planar graphs, etc.). This is the default for this project.

Only fall back to cropping the scan and embedding as a PNG if a diagram is a messy
freehand sketch that isn't really a graph (rare for this material). If that happens,
say so explicitly rather than silently embedding an image.

For each figure:
- Recreate it with the same structure as the original (same vertices, same edges,
  same "before → after" transformation if the notes show one, e.g. deletion,
  contraction).
- Use an arrow (`\draw[-{Latex[length=3mm]}, thick]`) between "before" and "after"
  states, matching the notes' layout.
- Keep diagrams compact — `scale=0.85` to `0.9` fits most page widths well.

## Step 3 — Apply the fixed template and style

Use this exact preamble (documentclass, packages, colors, theorem box) for every
chapter, so all chapters look consistent when combined later:

```latex
\documentclass[11pt]{scrartcl}

\usepackage[margin=1in]{geometry}
\usepackage{mathpazo}
\usepackage{amsmath,amssymb,amsthm}
\usepackage{tikz}
\usetikzlibrary{arrows.meta,positioning}
\usepackage[most]{tcolorbox}
\usepackage{xcolor}
\usepackage{hyperref}

\definecolor{accentblue}{RGB}{44,95,138}
\definecolor{boxfill}{RGB}{240,245,250}
\definecolor{boxborder}{RGB}{180,200,220}
\definecolor{highlightred}{RGB}{200,50,50}

\newtcolorbox{thmbox}[1]{
  colback=boxfill, colframe=boxborder,
  boxrule=0.6pt, arc=2pt, left=6pt, right=6pt, top=4pt, bottom=4pt,
  fonttitle=\bfseries\color{accentblue}, title=#1
}
\theoremstyle{plain}
\newtheorem{theorem}{Theorem}
\theoremstyle{remark}
\newtheorem*{remark}{Remark}

\hypersetup{colorlinks=true, linkcolor=accentblue, urlcolor=accentblue}
```

Style rules:
- **Theorem statements** go inside `\begin{thmbox}{Theorem N}...\end{thmbox}`
  (or `{Theorem N (Name)}` if the theorem has a common name, e.g.
  "Theorem 6 (Four Colour Theorem)").
- **Proofs** go in a plain `\begin{proof}...\end{proof}` immediately after the
  box, in normal body text (Palatino via `mathpazo`), not inside a colored box.
- **Unproved/named results** get a `\begin{remark}...\end{remark}` instead of
  a `proof` environment, stating plainly that no proof was given in the notes.
- **TikZ node style for graph vertices**, use consistently across all figures:
  ```
  every node/.style={circle,draw=accentblue,fill=accentblue!15,minimum size=6mm,inner sep=0pt}
  ```
- **Edges/lines**: plain black (`\draw`), no styling needed.
- **Highlight color** (`highlightred`) is reserved ONLY for drawing attention to
  a specific contradiction, impossible substructure, or the key change between
  "before" and "after" states (e.g. the K5 subgraph in Theorem 5's proof, or a
  set of contracted/added edges). Never use it decoratively.
- Do not add a table of contents or chapter numbering inside a single chapter
  file — that belongs in a master `main.tex` that `\input`s each chapter
  (see Step 5).

## Step 4 — Compile and verify before delivering
- Run `pdflatex -interaction=nonstopmode <file>.tex` twice (once for cross-refs/
  bookmarks to settle) and check the log for errors (not just warnings).
- Confirm the PDF page count and that figures rendered (open key pages if unsure).
- Never hand over a `.tex` file that hasn't been test-compiled successfully.
- Clean up `.aux`/`.log`/`.out` build artifacts before delivering — only the
  `.tex` (and PDF if useful for the user to preview) should be the deliverable.

## Step 5 — Multi-chapter project structure
When multiple chapters accumulate, restructure into:
```
main.tex          % \documentclass + preamble (shared) + \input{chapters/...}
chapters/
  01-graph-coloring.tex
  02-<next-topic>.tex
  ...
```
Each chapter file should contain only `\section{...}` content (theorems, proofs,
figures) — no `\documentclass` or preamble — so `main.tex` can `\input` them in
order. Move the preamble from Step 3 into `main.tex` once this restructuring
happens; don't duplicate it per chapter file.

## Naming convention
File names: lowercase, hyphenated, matching the PDF's topic, e.g.
`graph-coloring.tex`, `chromatic-polynomials.tex`.

## What NOT to do
- Don't invent proofs, examples, or content not present in the source notes.
- Don't change theorem numbering/order from the original notes.
- Don't use a different font, color scheme, or box style between chapters —
  consistency across the whole set of notes is the point of this template.
- Don't embed the original scanned images unless a diagram genuinely can't be
  represented as TikZ.