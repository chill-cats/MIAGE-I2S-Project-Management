# LaTeX setup and build guide

This repository contains the project document in [`main.tex`](./main.tex). The
compiled PDF is written to `build/latex/main.pdf` and is intentionally tracked
in Git; all other LaTeX build files are ignored.

## One-time setup

### 1. Install Visual Studio Code and LaTeX Workshop

1. Install [Visual Studio Code](https://code.visualstudio.com/).
2. In VS Code, open the **Extensions** view (`Ctrl+Shift+X` on Windows/Linux or
   `Cmd+Shift+X` on macOS).
3. Search for **LaTeX Workshop** and install the extension published by *James
   Yu*.

### 2. Install a LaTeX distribution

LaTeX Workshop needs a local TeX installation that provides `latexmk` and
`pdflatex`.

| Operating system | Distribution | Install notes |
| --- | --- | --- |
| macOS | [MacTeX](https://www.tug.org/mactex/) | Install the full MacTeX package, then restart VS Code. |
| Windows | [MiKTeX](https://miktex.org/download) | During setup, allow missing packages to be installed automatically. |
| Linux | TeX Live | For Debian/Ubuntu, run `sudo apt install latexmk texlive-latex-extra`. |

After installing it, open a new terminal and run:

```sh
latexmk --version
```

If the command prints a version, the distribution is ready. If it is not found
on macOS, restart VS Code (and, if needed, sign out and back in) so its terminal
can see the MacTeX path.

## Configure LaTeX Workshop for this project

Open the repository folder, rather than only [`main.tex`](./main.tex), in VS
Code. The included workspace configuration in
[`.vscode/settings.json`](./.vscode/settings.json) already tells LaTeX Workshop
to put generated files in `build/latex/`. No additional configuration is needed.

If VS Code asks whether you trust the folder, choose **Yes, I trust the
authors** so extensions can run the LaTeX build command. The repository's ignore
rules retain only `build/latex/main.pdf` for version control.

## Build the PDF

Open [`main.tex`](./main.tex), then use one of these options:

- Press `Ctrl+Alt+B` on Windows/Linux or `Cmd+Option+B` on macOS.
- Or open the Command Palette and select **LaTeX Workshop: Build LaTeX project**.

LaTeX Workshop uses its default `latexmk` PDF recipe and writes the result to
`build/latex/main.pdf`. Select **View LaTeX PDF** from the editor toolbar or
Command Palette to preview it within VS Code.

## Build from a terminal

From the repository root, run:

```sh
latexmk -pdf -interaction=nonstopmode -synctex=1 -outdir=build/latex main.tex
```

To remove generated build files before a clean rebuild, run:

```sh
latexmk -C -outdir=build/latex main.tex
```

The clean command removes generated files, including the PDF. Rebuild afterward
before committing if you want the current PDF included in Git.

## Troubleshooting

- **`latexmk` not found:** install the distribution above, restart VS Code, and
  verify `latexmk --version` in its integrated terminal.
- **Missing package error:** on MiKTeX, allow automatic package installation;
  on TeX Live/MacTeX, install the package named in the error or use the full
  distribution.
- **Build errors:** open the LaTeX Workshop **Output** panel and select
  `LaTeX Workshop` to see the first error. Correct it in [`main.tex`](./main.tex)
  and build again.
