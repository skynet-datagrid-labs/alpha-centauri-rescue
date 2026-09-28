# Spaceship Titanic — Alternate Dimension Predictor

Team submission for Kaggle's [Spaceship Titanic](https://www.kaggle.com/competitions/spaceship-titanic) 
competition: a binary classification task predicting which passengers were transported to an 
alternate dimension when the Spaceship Titanic collided with a spacetime anomaly.

## Team
| Name | Role | Focus |
|------|------|-------|
| Tony Kenga | Team Leader | Feature engineering |
| Ivan Mosoti | Member | |
| Will Gift | Member | |

## Problem
- **Task:** Binary classification — predict `Transported` (True/False) for each passenger.
- **Metric:** Classification accuracy.
- **Data:** ~8,700 training records, ~4,300 test records, 13 features including `HomePlanet`, 
  `CryoSleep`, `Cabin`, `Destination`, `Age`, `VIP`, and 5 amenity-spend columns.

## Repo structure
├── data/ # train.csv, test.csv, sample_submission.csv (gitignored — pull from Kaggle)
├── notebooks/ # individual exploration notebooks, one per teammate
├── src/
│ ├── features.py # shared feature engineering functions
│ ├── models.py # model training/eval functions
│ └── ensemble.py # blending/stacking logic
├── submissions/ # dated CSV submissions + the score each one got
├── requirements.txt
└── README.md


## Workflow
1. Each person branches off `main` for their own approach (e.g. `feature-cabin-split`, `model-catboost`).
2. Log every submission's local CV score and public LB score in `submissions/log.md` before opening a PR.
3. Agree on a shared CV split (fixed `random_state`, same folds) so scores are comparable across branches.
4. Merge working features into `src/features.py` once validated — don't duplicate feature logic across notebooks.
5. Final model = best single model or blend, agreed on as a team before the deadline.

## Key feature ideas to explore
- Split `Cabin` into `Deck` / `Num` / `Side`
- Split `PassengerId` group (`gggg`) to capture family/group size and group-level CryoSleep patterns
- Total spend across the 5 amenity columns, and spend-while-in-CryoSleep as an anomaly flag
- Extract surname from `Name` for family grouping

## Submission log
| Date | Model | CV Score | Public LB | Notes |
|------|-------|----------|-----------|-------|
|9/28/2026 | CatBoost, XGBoost, and HistGradientBoosting |0.81684 ± 0.01264 |0.80780 |Passenger transport predictions from an ensemble of CatBoost, XGBoost, and HistGradientBoosting models. Models were evaluated using five-fold cross-validation grouped by passenger group to reduce validation leakage. Final predictions use a 0.50 probability threshold. |
|9/28/2026| HistGradientBoosting, XGBoost | 0.81508 ± 0.01294 | 0.80640|This submission predicts whether each Spaceship Titanic passenger was transported to another dimension. It uses engineered passenger group, cabin, spending, and missing-data features, with an equal-weight blend of HistGradientBoosting, XGBoost, and CatBoost. The blend achieved 0.8147 five-fold cross-validation accuracy at the default threshold. Predictions were generated for all 4,277 test passengers.|
|9/28/2026| LightGBM, XGBoost | 0.8153 ± 0.0117  | 0.80360 | Trained both LightGBM and XGBoost side-by-side with 5-fold Cross Validation. By blending their predicted probabilities 50/50|  

## Useful links
- [Competition page](https://www.kaggle.com/competitions/spaceship-titanic)
- [Getting started notebook](https://www.kaggle.com/competitions/spaceship-titanic)
- [Kaggle Discord](https://discord.gg/kaggle)
