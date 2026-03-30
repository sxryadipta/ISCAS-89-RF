# RF Power Estimation — ISCAS'89 (Paper Reproduction)

Reproduction of the Random Forest model from:

> Govindaraj & Arunadevi (2021). *Machine Learning Based Power Estimation
> for CMOS VLSI Circuits.* ResearchSquare.
> https://doi.org/10.21203/rs.3.rs-723965/v1

## Results

| Metric | Paper | Reproduced |
|--------|-------|------------|
| MSE    | 1.46e-06 | 9.22e-06 |
| RMSE   | 0.000116 | 0.003037 |
| R      | 0.99938  | 0.98731  |

### Per-circuit prediction error

| Circuit | Actual (mW) | Predicted (mW) | Error % |
|---------|-------------|----------------|---------|
| S344    | 0.01846     | 0.01616        | 12.47%  |
| S382    | 0.01046     | 0.01091        |  4.28%  |
| S386    | 0.01628     | 0.01848        | 13.50%  |
| S400    | 0.01065     | 0.01112        |  4.45%  |
| S641    | 0.03629     | 0.04225        | 16.43%  |

## Notes on the gap

The paper uses NSGA-II (a multi-objective evolutionary optimizer) to tune
hyperparameters, which is more exhaustive than GridSearchCV. The paper also
does not fully disclose its exact train/eval split for S386 and S400, which
appear in both Table 1 (training) and Table 4 (evaluation). These factors
account for most of the remaining gap.

The core methodology is faithfully reproduced:
- 20 training circuits, 5 evaluation circuits (Table 1 and Table 4)
- 9 circuit attributes as features
- 10-fold cross-validation for hyperparameter selection
- n_estimators: 150–750, max_depth: 10–15 (paper's stated ranges)
- R reported as Pearson correlation coefficient, not R²

## How to run

Open in Google Colab and run all cells in order:

1. Cell 1 — install dependencies
2. Cell 2 — load data
3. Cell 3 — train and tune (GridSearchCV, ~1 min)
4. Cell 4 — evaluate and print results
5. Cell 5 — download predictions.csv

## Dataset

ISCAS'89 sequential benchmark circuits. Features: GATE, AND, INV, NOR,
NAND, OR, DFF, IN, OUT. Target: Monte Carlo simulation power in mW.
Original data sourced from Ligang Hou et al. (2006).

## Dependencies

- scikit-learn >= 1.3.0
- numpy >= 1.24.0