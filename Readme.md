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

## Configuring the public repo

Target: https://github.com/nasro-bay/Graph_theory_proofs

Run these yourself (not executed for you):

```bash
# 1. Point this local repo at the GitHub remote
git remote add origin https://github.com/nasro-bay/Graph_theory_proofs.git

# 2. (optional) rename local branch to main to match GitHub's default
git branch -M main

# 3. Stage and commit the new readme (and anything else pending)
git add Reaadme.md
git commit -m "Add collaboration readme"

# 4. Push and set upstream
git push -u origin main
```

On GitHub itself (Settings tab of the repo):

- **Visibility**: confirm it's set to *Public*.
- **Description/topics**: add a short description and topics like
  `graph-theory`, `latex`, `tikz`, `lecture-notes`.
- **Issues**: make sure Issues are enabled (Settings → General → Features) so
  people can report proof errors.
- **Branch protection** (Settings → Branches): protect `main` and require
  pull requests before merging, so contributions come in via review instead
  of direct pushes.
- **License**: add a LICENSE file (e.g. MIT or CC-BY for lecture-note-style
  content) so contributors know what they can reuse.
- **`.gitignore`**: add a LaTeX `.gitignore` (ignore `*.aux`, `*.log`, `*.out`,
  `*.synctex.gz`) — the `Trees/` folder already has some of these tracked and
  they're just build noise, not source.
