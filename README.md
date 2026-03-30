# RF Power Estimation — ISCAS'89 (Paper Reproduction)

Reproduction of the Random Forest model from:

> Govindaraj & Arunadevi (2021). *Machine Learning Based Power Estimation
> for CMOS VLSI Circuits.*

## Paper targets (Table 4 / Table 6)

| Metric | Paper |
|--------|-------|
| MSE    | 1.46e-06 |
| RMSE   | 0.000116 |
| R      | 0.99938  |

## Setup
```bash
python -m venv .venv
source .venv/bin/activate      # Windows: .venv\Scripts\activate
pip install -r requirements.txt
python main.py
```

## Key implementation notes

- **R is Pearson correlation coefficient**, not sklearn's r2_score
- **10-fold CV is used only for hyperparameter selection**, not metric reporting
- **Eval set (Table 4)** = S344, S382, S641 (unseen) + S386, S400 (from training features)
- Hyperparameter ranges match paper: n_estimators 150–750, max_depth 10–15