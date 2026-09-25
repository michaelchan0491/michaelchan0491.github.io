# michaelchan0491.github.io

My personal website and blog for the UBC MDS program, built with Quarto and
published with GitHub Pages at <https://michaelchan0491.github.io>. It includes
two computational posts, one in R and one in Python, each with a reproducible
environment pinned by renv and uv.

## Requirements

Install these first (versions I used):

- [Quarto](https://quarto.org/docs/get-started/) 1.10.18
- [uv](https://docs.astral.sh/uv/getting-started/installation/) 0.12.7
  (uv installs Python 3.14 for you, so you do not need Python separately)
- [R](https://cran.r-project.org/) 4.6.1

renv does not need to be installed; it bootstraps itself the first time R
starts in this project.

## Build the site

Run every command from a terminal, in the top level of the repository
(the folder containing `_quarto.yml`).

1. Clone the repository and move into it:

```bash
   git clone https://github.com/michaelchan0491/michaelchan0491.github.io.git
   cd michaelchan0491.github.io
```

2. Create the Python environment from `uv.lock` (creates `.venv/`):

```bash
   uv sync
```

3. Restore the R packages from `renv.lock`:

```bash
   Rscript -e 'renv::restore(prompt = FALSE)'
```

   If you prefer, start R in the top-level folder and run
   `renv::restore()` in the R console instead.

4. Render the site using the project's Python environment:

```bash
   uv run quarto render
```

   Always render from the top level. That is how R finds `.Rprofile` and
   activates renv, and `uv run` makes Quarto use the project's `.venv`.

## View the site locally

The built site is written to the `docs/` folder. To open it:

```bash
open docs/index.html        # macOS
```

On Windows, double-click `docs/index.html`. Alternatively, run
`uv run quarto preview` to serve the site at a local address with live reload.

## Data

Both posts use the Palmer Penguins dataset (Horst, Hill & Gorman, 2020),
collected at Palmer Station Antarctica LTER and released under CC0:
<https://allisonhorst.github.io/palmerpenguins/>

- **R post:** data comes from the `palmerpenguins` R package, installed by
  `renv::restore()`.
- **Python post:** data is read from `posts/python_project/data/penguins.csv`,
  which is committed to this repository (about 20 KB).
