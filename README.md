# Pipeline-Agnostic Data Leakage Detection

An Advanced Data Analytics project that evaluates whether data leakage can be detected from the processed train/test data and a trained model's predictions, without access to the model training pipeline.

The notebooks inject controlled leakage into benchmark datasets, run a black-box detector, and measure detection quality and performance inflation against clean scenarios.

## Notebooks

| Notebook | Benchmark | Notes |
| --- | --- | --- |
| `adult_income_leakage_detection.ipynb` | UCI Adult Income | Target leakage, train/test contamination, and preprocessing leakage. Temporal leakage is not applicable to this snapshot dataset. |
| `california_housing_leakage_detection (1).ipynb` | California Housing | Target leakage, train/test contamination, and preprocessing leakage. Temporal leakage is not applicable. |
| `credit_card_fraud_leakage_detection.ipynb` | Credit Card Fraud (ULB / Kaggle) | Includes time-ordered evaluation and temporal leakage scenarios. |
| `rossmann_leakage_detection (1).ipynb` | Rossmann Store Sales | Includes time-ordered evaluation and temporal leakage scenarios. |

Each notebook is self-contained and documents its dataset format, data loading, configuration, benchmark scenarios, outputs, and caveats. They are designed for Google Colab, with data uploaded to `/content` where required. Follow the instructions at the top of the notebook you want to run; set its quick mode option for a shorter run. Full benchmark runs can take substantial time, especially for the larger datasets.

## Detector overview

The detector receives processed training and test splits, labels, feature names, optional timestamps and row IDs, and a black-box model interface (`predict` / `predict_proba`). It evaluates signals such as:

- **Target leakage:** features that strongly encode the target.
- **Train/test contamination:** exact or near-duplicate rows across splits.
- **Temporal leakage:** training data that comes from after the evaluation period, when a meaningful time axis is available.
- **Preprocessing leakage:** evidence that preprocessing was fit using both train and test data.

For each leakage type, the notebooks report scores, flags and supporting evidence, along with an overall verdict and estimated performance inflation. Scenarios are paired with clean counterparts to support controlled comparisons. Results and figures are written to `/content/results/`; individual notebooks describe their checkpointing and export behavior.

## Requirements and data

Use the setup and data-loading cells in each notebook as the source of truth for dependencies and dataset acquisition. Depending on the benchmark, data may be fetched by the notebook or uploaded manually. Some data sources require internet access. The notebooks use CPU-compatible model implementations; full benchmark runs may take a while.

## Running in Google Colab

1. Open a notebook from the table above in Colab.
2. Read its dataset instructions and upload any required files to `/content`.
3. Select **Runtime → Run all**. For a quicker exploratory run, enable the notebook's quick mode setting first.
4. Review the generated result tables and figures in `/content/results/`.

## Project team

Jackfruit Project (Advanced Data Analytics):

- Akula Pragnya (PES1UG24AM028)
- Abhay TS (PES1UG24AM008)
- Avyukt Ranjan (PES1UG24AM060)
