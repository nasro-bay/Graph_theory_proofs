# Graph Theory Proofs

A collection of Graph Theory lecture notes, transcribed from handwritten scans
into clean, typeset LaTeX documents (theorem/proof boxes + TikZ-drawn figures
for every graph diagram).

## What's in this repo

| Folder | Topic | Contents |
|---|---|---|
| `Connectivity_Cycles/` | Connectivity & cycles | Scanned notes (PDF) |
| `Eurlian_Graphs/` | Eulerian graphs | Scanned notes (PDF) |
| `Graph_coloring/` | Graph coloring | `main.tex` + compiled `main.pdf` |
| `Hamiltonian_graphs/` | Hamiltonian graphs | Scanned notes + `hamiltonian-graphs.tex`/`.pdf` |
| `Planarity/` | Planarity | Scanned notes (PDF) |
| `Trees/` | Trees | Scanned notes + `trees.tex` + compiled PDF/previews |

Some topics are already converted to LaTeX (`.tex` + compiled `.pdf`); others
are still just the original scanned PDF, waiting to be transcribed.

> Note: `Readme.md` (no extra "a") in the repo root is **not** a description
> file — it's the conversion spec/prompt that defines how a scanned PDF gets
> turned into the styled `.tex` template used across every chapter here. Keep
> using it as the reference for style/formatting when adding a new chapter.

## Collaboration

This repo is open to contributions:

- **Pull requests** are the way to contribute — fixes to a proof, a
  mistranscribed theorem, a TikZ diagram that doesn't match the original
  notes, or converting one of the still-scanned-only topics into LaTeX.
- **Found an error in a proof or statement?** Open an Issue describing the
  mistake (which file, which theorem/line) even if you can't fix it yourself —
  reporting is just as valuable as fixing.
- When converting a new chapter or editing an existing one, follow the
  template and rules in `Readme.md` so every chapter stays visually and
  structurally consistent (same preamble, same theorem box style, same TikZ
  vertex style).
- Please test-compile (`pdflatex`) before opening a PR, and don't commit
  build artifacts (`.aux`, `.log`, `.out`) — see the `.gitignore` note below.


