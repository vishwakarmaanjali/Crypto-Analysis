# Copilot / AI Agent Instructions for Crypto-Analysis

Purpose: give an AI code assistant the minimal, actionable context needed to make productive changes in this repository.

- **Big picture:** This project is a data/analytics workspace for cryptocurrency analysis. Data flows from `raw_data/` (ingested API dumps) → `clean_data/` (processed datasets) → `report/` (Power BI visuals) → `result/` (final exports). The root `README.md` contains the high-level dataset and analytic intent (momentum scoring, price-change analysis).

- **Key locations:**
  - `README.md` — project overview and dataset features.
  - `raw_data/` — store raw API outputs and endpoints metadata.
  - `clean_data/` — cleaned/normalized dataset files consumed by analysis.
  - `report/` — Power BI files and report assets (requires Power BI Desktop to open).
  - `result/` — exports and final analysis outputs.

- **What agents should know before editing:**
  - This repo currently contains documentation and data folders; there is no build/test pipeline or CI configuration present to run code automatically.
  - Target environment is Windows (developer used Power BI Desktop). Avoid Linux-specific assumptions for local manual workflows unless the user adds cross-platform tooling.
  - Data and report consistency matters: when changing schema in `clean_data/`, update any dependent report visuals in `report/` and note the change in `README.md`.

- **Conventions and patterns observed:**
  - Folder names use underscores (e.g., `clean_data`, `raw_data`). Follow the same naming style for new top-level directories.
  - Data files are kept under `*/data` subfolders. When adding derived datasets, place them in `clean_data/data` and document the columns added/removed.
  - Power BI is the final visualization layer — expect transformations to be reflected there rather than in code files inside this repo.

- **Typical agent tasks and how to approach them:**
  - Adding a new ETL script: create a `scripts/` or `src/` folder, add a descriptive README in the new folder, and place outputs under `clean_data/data`. Add a short note to `README.md` summarizing the change.
  - Updating analysis fields (e.g., momentum, price-change): locate the CSV/TSV in `clean_data/data`, modify or add columns, then list the downstream report items that must be updated in `report/`.
  - Fixing report issues: describe the expected visual change and where the source data lives; do not attempt to edit `.pbix` binaries programmatically without explicit user instruction.

- **Integration & external dependencies:**
  - External data ingestion endpoints are kept with raw dumps in `raw_data/`. If adding connectors, record credentials/endpoint details OUTSIDE the repository and ask the user where secrets should be stored.
  - There is no requirements file or package manifest yet. If you add code that requires dependencies, include a `requirements.txt` (for Python) or equivalent, and update `README.md` with setup/run steps.

- **Developer workflow notes (explicit):**
  - Opening and editing reports: use Power BI Desktop on Windows to open `report/` files.
  - No automated tests detected — verify dataset changes by producing a small sample output in `result/` and documenting verification steps in `README.md`.
  - When you add scripts, include example commands like `python scripts/transform.py --input raw_data/data/foo.csv --output clean_data/data/foo_clean.csv`.

- **When in doubt:** Ask the repository owner for: sample credentials, the exact Power BI `.pbix` file to modify, preferred runtime (Python version), and whether they want a CI pipeline added. Document any assumptions you make in your pull request description.

- **Examples from this repo:**
  - To add a cleaned dataset: place the output in `clean_data/data/` and add a one-line summary to `README.md` describing schema changes.
  - To update visuals that rely on momentum scoring: update `clean_data` first, then open `report/` in Power BI Desktop and refresh visuals.

If any of these areas are unclear or you want the instructions to be broader/narrower, tell me which sections to expand or which files you'd like me to inspect and I'll iterate.
