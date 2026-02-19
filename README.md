# Modular LaTeX CV

A clean, modular LaTeX CV project. Your personal data lives in **one configuration file**, each CV section lives in **its own file**, and the layout is handled separately in `main.tex`. Empty sections are automatically hidden.

## Repository Structure

```
.
├── main.tex                 # CV layout — imports config & sections
├── config.tex               # Your personal info (name, contact, etc.)
├── sections/                # One file per CV section
│   ├── summary.tex
│   ├── skills.tex
│   ├── experience.tex
│   ├── projects.tex
│   ├── education.tex
│   ├── certifications.tex
│   ├── awards.tex
│   ├── languages.tex
│   └── interests.tex
├── .latexmkrc               # Latexmk configuration
├── .github/workflows/
│   └── latex.yml            # GitHub Actions: compile PDF on push
└── README.md
```

## Quick Start

1. **Edit your information** in `config.tex` (name, email, phone, links, location).
2. **Edit each section** file under `sections/` with your content.
3. **Compile** locally:
   ```bash
   latexmk            # uses .latexmkrc settings
   # or
   pdflatex main.tex
   ```
4. **Push** to GitHub — the Actions workflow compiles the PDF automatically and uploads it as an artifact.

## How to Edit Your Information

Open `config.tex` and change the values:

```latex
\newcommand{\cvname}{Your Name}
\newcommand{\cvemail}{you@example.com}
\newcommand{\cvphone}{+1-000-000-0000}
\newcommand{\cvgithub}{https://github.com/you}
\newcommand{\cvgithubname}{github.com/you}
\newcommand{\cvlinkedin}{https://linkedin.com/in/you}
\newcommand{\cvlinkedinname}{linkedin.com/in/you}
\newcommand{\cvlocation}{City, Country}
```

## How to Edit a Section

Each file in `sections/` contains only the **content** for that section (no `\section*{}` header — the header is added automatically by `main.tex`). Simply open the file and write your content using standard LaTeX.

## How to Hide a Section

To hide a section, remove all non-comment content from its file. A file that is empty or contains only LaTeX comments (`% ...`) will be skipped entirely — no header, no blank space.

For example, to hide **Interests**, change `sections/interests.tex` to:

```latex
% Interests
% (currently hidden — add content here to show this section)
```

## How to Add a New Section

1. Create a new file in `sections/`, e.g. `sections/volunteering.tex`.
2. Add your content to the file.
3. In `main.tex`, add a line where you want the section to appear:
   ```latex
   \cvsection{Volunteering}{sections/volunteering.tex}
   ```

That's it — the section will appear automatically when the file has content, and will be hidden when the file is empty.

## Continuous Integration

Every push triggers the GitHub Actions workflow (`.github/workflows/latex.yml`), which:

1. Checks out the repository.
2. Compiles `main.tex` into a PDF using `pdflatex`.
3. Uploads the resulting `main.pdf` as a build artifact named **cv-pdf**.

Download the artifact from the **Actions** tab in your repository.

## Compilation Requirements

- A TeX distribution with `pdflatex` (e.g., TeX Live, MiKTeX).
- `latexmk` (optional, but recommended — included in most TeX distributions).
- Required LaTeX packages: `geometry`, `enumitem`, `hyperref`, `titlesec`, `parskip`, `xcolor`, `catchfile`.
