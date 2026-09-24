# Personal Website

This repository builds my personal Quarto website, including two reproducible computational posts (one in R, one in Python) analyzing NYC flight delay data, published via GitHub Pages.

## 1. Requirements

Install these before building:

- [Quarto](https://quarto.org/docs/get-started/) — version **1.10.18** used
- [uv](https://docs.astral.sh/uv/getting-started/installation/) — version **0.12.5** used (manages the Python environment)
- [R](https://www.r-project.org/) — version **4.6.1** used

`renv` (R's package manager) does not need to be installed separately — it bootstraps itself automatically the first time R runs in this project (via `.Rprofile`).

## 2. Build instructions

Run these in order.

```bash
# 1. Clone the repository (run anywhere in a terminal)
git clone https://github.com/sebas-tenro/mds-website.git
cd mds-website
```

```bash
# 2. Restore R packages (run in the terminal, from the repo root)
Rscript -e "renv::restore()"
```

```bash
# 3. Restore the Python environment (run in the terminal, from the repo root)
uv sync
```

```bash
# 4. Preview the site (run in the terminal, from the repo root)
uv run quarto preview
```

```bash
# 5. Render the full site (run in the terminal, from the repo root)
uv run quarto render
```

`uv run` makes sure Quarto uses this project's Python environment (`.venv`) for the Python post; R packages are picked up automatically from the `renv` library restored in step 2.

## 3. Viewing the built site

The rendered site is written to the `docs/` folder at the repository root (set via `output-dir: docs` in `_quarto.yml`). To view it locally:

- Open `docs/index.html` directly in a browser, or
- Run `uv run quarto preview` from the repo root, which starts a local server with live-reload.

🌐 The live, deployed version is at: https://sebas-tenro.github.io/mds-website/

## 4. Data sources & network dependency

- **R post:** uses the [`nycflights23`](https://cran.r-project.org/package=nycflights23) package (CC0 licensed), which bundles its data directly inside the installed package — no data files are committed to this repo.

  > Ismay C, Couch S, Wickham H (2025). *nycflights23: Flights and Other Useful Metadata for NYC Outbound Flights in 2023*. R package version 0.2.0, <https://moderndive.github.io/nycflights23/>.

- **Python post:** uses the [`nycflights13`](https://pypi.org/project/nycflights13/) package (CC0 licensed), a Python port of the original R `nycflights13` dataset, maintained by Michael Chow. Its data is similarly bundled inside the installed package.

Because both datasets are bundled inside their packages, **the render itself needs no network access**.