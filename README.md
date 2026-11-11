# Telecom Customer Churn Analysis

Data analysis for the GCI World 2026 final assignment, using customer and usage records from an anonymous telecommunications provider, Company A. The project explores patterns associated with churn to support a data-driven customer retention proposal.

The current work focuses on exploratory data analysis. Model comparison, retention targeting, and a quantified business case are planned next.

## Project contents

- `Final Assignment/01_eda.ipynb` — exploratory analysis of data quality, customer profiles, churn patterns, and revenue concentration.
- `Final Assignment/telecom/` — customer information (`Client.csv`) and usage records (`Record.csv`), joined by `Customer_ID`.
- `Final Assignment/tutorial.ipynb` — supplied analysis and modeling example.
- `FINAL_ASSIGNMENT_PLAN.md` — assignment requirements and the project work plan.
- `environment.yml` — Conda dependencies; `environment-osx-arm64.lock.txt` records the exact Apple Silicon package versions.
- `EDA_ENVIRONMENT.md` — detailed setup instructions and environment verification notes.

## Getting started

Install Miniconda, then run these commands from the repository root:

```bash
conda env create --prefix "$PWD/.conda/eda" --file environment.yml
conda activate "$PWD/.conda/eda"
python -m ipykernel install --sys-prefix --name gci-eda --display-name 'Python (GCI EDA)'
cd 'Final Assignment'
jupyter lab 01_eda.ipynb
```

If the environment already exists, skip the creation command. Select **Python (GCI EDA)** as the notebook kernel. Run the notebook from `Final Assignment` so its relative data paths resolve correctly; charts are written to `figures/` within that directory.

The project uses Python 3.12, NumPy, pandas, Matplotlib, seaborn, and scikit-learn. The local Conda environment, package cache, notebook checkpoints, and `.DS_Store` files are excluded from Git.
