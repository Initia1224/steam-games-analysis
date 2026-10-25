# Steam Games Data Analysis

**What factors affect the positive review rate of Steam games?**

An exploratory data analysis of 122,611 Steam games, looking at how price, genre, average playtime and DLC count relate to how positively players review a game.

## Key findings

1. **Higher price = lower positive rate** — players expect more from expensive games, and judge them more harshly.
2. **Casual and Indie games have the highest positive rate (~77.8%)**, while Racing and Simulation games sit at the bottom (~73–74%).
3. **Average playtime has almost no correlation with positive rate (r = -0.01)** — playing a game longer does not mean rating it better.
4. **Games with 20+ DLCs have the highest positive rate (~83%)** — most plausibly because well-liked games keep receiving content support (reverse causality), not because DLCs mechanically cause good reviews.

## Data source

- Kaggle — **Steam Games Dataset** (122,611 games). One row per game, including price, positive/negative review counts, genres, average playtime and DLC count.
- The data file (`games.csv`, ~large) is not stored in this repository. Download it from the dataset page on Kaggle and place it next to the notebook before running (see *How to run*).

## Method

- Built the target metric `positive_rate = Positive / (Positive + Negative)`, plus a `total_reviews` column used for robustness checks.
- Analysis sample: paid games (`Price > 0`) with a computable positive rate.
- Price: scatter plot plus grouped averages over price ranges ($0–5, $5–15, $15–30, $30–50, $50–100).
- Genre: a game can have several genres, so genre lists were split and exploded (one row per game–genre pair); genres with ≤100 games were excluded to avoid small-sample noise.
- Playtime: scatter on a log scale plus a Pearson correlation coefficient.
- DLC count: grouped averages over DLC-count ranges.
- **Robustness check (Section 7 of the notebook):** the headline price results are recomputed with minimum review-count thresholds (0 / 10 / 50 reviews), because a game with a single positive review otherwise counts as a 100% positive rate.

## Charts

All charts are generated inside the notebook (`steam_analysis.ipynb`):

- Price vs positive rate (scatter + average by price range)
- Average positive rate by genre — note the y-axis starts at 0.7, so differences are visually amplified
- Playtime vs positive rate (log-scale scatter)
- DLC count vs positive rate

## How to run

1. Download `games.csv` from the Kaggle dataset page and put it in this folder.
2. Install dependencies: `pip install -r requirements.txt`
3. Open `steam_analysis.ipynb` in Jupyter and run all cells from top to bottom.

## Limitations

- Everything here is correlational; no causal claims are made (see the DLC discussion above).
- The main sections do not require a minimum number of reviews; Section 7 quantifies how much that matters.
- Price grouping stops at $100, so extreme price outliers are outside the grouped chart.

## Next steps

- Cross-check the headline results with a SQL (SQLite) version of the same queries.
- Add significance testing for the genre differences.

## Tools

Python · Pandas · Matplotlib · Jupyter Notebook
