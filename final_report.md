# Time Series Forecasting Project — Prophet (Optuna) vs ARIMA

## Dataset
- Type: Synthetic daily dataset
- Duration: 2016-01-01 00:00:00 to 2019-12-30 00:00:00 (1460 rows)
- Components: trend, yearly_seasonality, weekly_seasonality, holiday_spikes, noise

## Cross-Validation Strategy
- Method: Expanding-window manual CV
- Folds: 8
- Initial window: 365 days
- Horizon: 90 days
- Step: 90 days

## Hyperparameter Search (Optuna)
Search space used:
- changepoint_prior_scale: [0.001, 3.0] (log-uniform)
- seasonality_prior_scale: [0.01, 10.0] (log-uniform)
- seasonality_mode: ['additive', 'multiplicative']
- fourier_order_yearly: int [5, 15]
- fourier_order_weekly: int [3, 8]

Best parameters found (Optuna):
```json
{
  "changepoint_prior_scale": 0.018289895582215797,
  "seasonality_prior_scale": 0.8722798602334374,
  "seasonality_mode": "additive",
  "fourier_order_yearly": 5,
  "fourier_order_weekly": 7
}
```

## Performance on held-out test set
| Model | MAE | RMSE | MAPE |
|---|---:|---:|---:|
| Prophet (optimized) | 1.9032 | 2.8208 | 1.5097 |
| ARIMA(3, 1, 3) | 6.2634 | 7.5446 | 4.8590 |

## Computational Efficiency
- Optuna tuning time: 64.09 seconds
- Final Prophet (train on train+val) time: 0.14 seconds
- ARIMA train/selection time: 12.38 seconds

## Files produced
- **forecast_plot**: `/content/forecast_plot.jpg`
- **comparison_plot**: `/content/comparison_plot.jpg`
- **summary_json**: `/content/ts_project_summary.json`
- **final_report_md**: `/content/final_report.md`
- **final_summary_txt**: `/content/final_summary.txt`
- **uploaded_image_path**: `/mnt/data/2d2d05bf-630e-4d12-98d4-ef55cd8ae6c1.png`

## Notes & Next Steps
- The dataset is synthetic to guarantee multiple seasonalities and reproducibility.
- For production or real datasets, include external regressors (holiday flags, promotions) and consider increasing Optuna trials.
- The uploaded image provided by the user is referenced here for inclusion in the report:
  - Uploaded image path: `/mnt/data/2d2d05bf-630e-4d12-98d4-ef55cd8ae6c1.png`
