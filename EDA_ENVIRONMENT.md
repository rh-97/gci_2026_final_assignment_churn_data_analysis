# EDA environment

The project uses the existing Miniconda installation with an environment stored at `.conda/eda`. Python 3.12 and the notebook's required packages are specified in `environment.yml`.

## Open the notebook

Run these commands in Terminal:

```bash
cd '/Volumes/Projects/GCI World_202609/05. Final Assignment (due XX)'
conda activate "$PWD/.conda/eda"
cd 'Final Assignment'
jupyter lab 01_eda.ipynb
```

Select **Python (GCI EDA)** if prompted for a kernel. When running from VS Code, select the Python interpreter at `.conda/eda/bin/python` within this project.

The working directory must be `Final Assignment` because the notebook loads `telecom/Client.csv` and `telecom/Record.csv` using relative paths. Charts are saved to its `figures` directory.

## Packages

- NumPy and pandas for data manipulation
- Matplotlib and seaborn for plots
- scikit-learn for ROC-AUC
- JupyterLab, ipykernel, and nbconvert for interactive use and notebook execution

## Recreate the environment

From the project root:

```bash
CONDA_PKGS_DIRS="$PWD/.conda/pkgs" conda env create \
  --prefix "$PWD/.conda/eda" --file environment.yml
"$PWD/.conda/eda/bin/python" -m ipykernel install \
  --sys-prefix --name gci-eda --display-name 'Python (GCI EDA)'
```

`environment.yml` records the requested dependencies. `environment-osx-arm64.lock.txt` records the exact installed packages for this Apple Silicon Mac; it can be used with `conda create --prefix "$PWD/.conda/eda" --file environment-osx-arm64.lock.txt` instead of the YAML command.

The `.conda` directory contains the environment and package cache and is excluded by `.gitignore`. It is a local installation, so recreate it after moving the project to a different path.

## Verification

Verified on 12 November 2026 using Python 3.12.16, NumPy 2.5.4, pandas 3.1.0, Matplotlib 3.11.2, seaborn 0.13.2, and scikit-learn 1.9.1.

A temporary copy of `01_eda.ipynb` executed all 27 nonempty code cells successfully and generated 14 chart files. The original notebook was unchanged. Local verification details are recorded in `.conda/verification.json`.
