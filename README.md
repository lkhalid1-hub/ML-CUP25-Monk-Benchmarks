# ML-CUP25 Regression and MONK Classification Experiments

Machine-learning coursework project covering two benchmark families:

- **MONK-1, MONK-2, and MONK-3:** binary classification with k-nearest neighbours, RBF SVM, and MLP classifiers.
- **ML-CUP25:** multi-output regression (12 input features and 4 targets) with Linear Regression, SVR, Random Forest, and MLP regressors.

The notebooks use cross-validation and hyperparameter search, generate analysis figures, and retain the project’s original result tables, plots, report, and ML-CUP25 blind-test prediction file.

## Repository layout

```text
.
├── data/
│   ├── cup/                       # ML-CUP25 train and blind-test CSV files
│   └── monk/README.txt            # MONK data are fetched from OpenML
├── notebooks/
│   ├── cup_project.ipynb          # ML-CUP25 regression workflow
│   └── monk_experiments.ipynb     # MONK classification workflow
├── results/
│   ├── cup/                       # ML-CUP25 figures, abstract, and prediction CSV
│   └── monk/                      # MONK result tables and figures
├── KathiriyaKhalid.pdf            # Project report
├── requirements.txt
└── .gitignore
```

## Requirements

- Python 3.10 or newer
- `pip`
- Internet access for the MONK notebook's first run, because it downloads MONK datasets through OpenML

## Setup

Run these commands from the repository root.

### Windows PowerShell

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

### macOS / Linux

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

## Run the ML-CUP25 regression project

The ML-CUP25 data files are already included under `data/cup/`. The notebook expects to be started from the `notebooks` directory:

```powershell
cd notebooks
jupyter notebook cup_project.ipynb
```

Run the cells from top to bottom. The notebook:

1. Splits the 500 labelled samples into train/validation/test partitions.
2. Compares Linear Regression, SVR, Random Forest, and MLP models using Mean Euclidean Error (MEE).
3. Tunes SVR, Random Forest, and MLP models with 5-fold `GridSearchCV`.
4. Produces learning curves, residual/prediction analysis, feature-importance charts, and model comparisons in `../results/cup/`.
5. Retrains the selected model and writes blind-test predictions to `../results/cup/KathiriyaKhalid_ML-CUP25-TS.csv`.

The tuning cells are computationally intensive, particularly the MLP and Random Forest grid searches. They can take several minutes or longer, depending on the computer.

## Run the MONK classification project

From the repository root, start Jupyter in the same way:

```powershell
cd notebooks
jupyter notebook monk_experiments.ipynb
```

Run the cells in order. On its first data-loading cell, the notebook fetches MONK-1, MONK-2, and MONK-3 from OpenML. It one-hot encodes features, compares k-NN/SVM/MLP baselines, runs 5-fold hyperparameter searches, and saves tables and figures under `../results/monk/`.

## Existing results

The provided original outputs are kept in the repository:

- `results/monk/final_monk_summary.csv` — classification summaries for all MONK tasks.
- `results/cup/KathiriyaKhalid_ML-CUP25-TS.csv` — submitted-format ML-CUP25 blind-test predictions.
- `results/cup/` and `results/monk/` — plots, learning curves, confusion matrices, hyperparameter analyses, and evaluation tables.

The original reported ML-CUP25 results select the MLP regressor, with validation MEE 19.51 and internal test MEE 20.80.
