# Predicting Formula 1 Race Winners

**When does pole position matter, and when does Friday practice tell a better story?**

CS 200 Capstone Project — Edmonds College Data Analytics Certificate — 2026

---

## Research Question

What predicts the winner of a Formula 1 Grand Prix better — starting from
pole position, or demonstrating consistent lap times during the second free
practice session (FP2)? And does this relative predictive power depend on
whether the race takes place on an open (purpose-built) or street circuit?

## Hypothesis (H1)

On open circuits, FP2 lap-time consistency has a stronger relationship to
winning a Formula 1 race than pole position. Formally:

> logit P(Y = 1) = β₀ + β₁·X₁ + β₂·X₂   (fit only on open-circuit races)

H1 is supported only if **|β₂| > |β₁|**, **β₂ < 0**, and both p-values **< 0.05**.

## Method

Binary logistic regression (statsmodels) fit on driver-race observations from
the four leading constructor teams (Red Bull Racing, Ferrari, McLaren,
Mercedes) during the 2023, 2024, and 2025 seasons. Circuit type enters as a
moderator through subset analysis. FP2 lap-time consistency is operationalized
as the standard deviation of clean race-pace laps within 107% of the
session-fastest lap.

## Key Findings

1. **Pole position dominates.** β₁ = +3.65 (p < 0.001), odds ratio ≈ 38.
   Starting from pole multiplies the odds of winning by about 38 times.
2. **FP2 consistency: null result.** β₂ = −0.11 (p = 0.92). The hypothesized
   effect is statistically indistinguishable from zero in this sample.
   H1 is **not supported**.
3. **Street-circuit surprise.** On street circuits, β₂ flips to positive
   (+1.13), suggesting higher FP2 variability may reflect deliberate setup
   exploration by top teams rather than inconsistent driving.

Full report including limitations (sample attrition, low events-per-variable,
winner concentration on Verstappen) is in `Fernandez_CS200_FinalReport.pdf`.

## Data Sources

- **FastF1** (Schaefer, 2024) — primary operational source. All variables in
  the model originate from FastF1.
- **Kaggle f1-predictions dataset** (Landry, 2024) — secondary validation
  reference for the 2024 grid and finish positions.
- **Manual circuit classification** — open vs street, curated by the analyst.

## How to Reproduce

1. Clone this repository:
```bash
   git clone https://github.com/AdrianFdata/f1-race-winner-prediction.git
   cd f1-race-winner-prediction
```

2. Install dependencies:
```bash
   pip install -r requirements.txt
```

3. Open the notebooks in order:
   - `F1_Step1_circuits.ipynb` — manual circuit classification
   - `F1_Step2_outcomes.ipynb` — race outcomes via FastF1
   - `F1_Step3_consistency.ipynb` — FP2 consistency per driver-race
   - `F1_Step4_master.ipynb` — merges the three datasets into the master table
   - `F1_Step5_model.ipynb` — logistic regression + predicted probability chart

The first run of Step 2 and Step 3 takes ~30 minutes total because FastF1
downloads and caches session data. Subsequent runs are near-instant.

## Project Structure
├── F1_Step1_circuits.ipynb

├── F1_Step2_outcomes.ipynb

├── F1_Step3_consistency.ipynb

├── F1_Step4_master.ipynb

├── F1_Step5_model.ipynb

├── circuits_df.csv

├── outcomes_df.csv

├── consistency_df.csv

├── master_df.csv

├── Fernandez_CS200_FinalReport.pdf

├── requirements.txt

├── LICENSE

└── README.md

## References

- O'Hanlon, E. (2022). *Using supervised machine learning to predict the
  final rankings of the 2021 Formula One Championship* [Master's thesis,
  National College of Ireland].
- Weissbock, J., & Mills, S. (2025). *Evaluating the predictive power of
  qualifying performance in Formula One Grand Prix* [Preprint]. arXiv.
  https://arxiv.org/abs/2507.10966
- Peduzzi, P., Concato, J., Kemper, E., Holford, T. R., & Feinstein, A. R.
  (1996). A simulation study of the number of events per variable in logistic
  regression analysis. *Journal of Clinical Epidemiology*, 49(12), 1373–1379.

## Author

**Adrian Fernandez** — junior data analyst, Edmonds College Data Analytics
Certificate program.

## License

MIT License — see [LICENSE](LICENSE) for details.
