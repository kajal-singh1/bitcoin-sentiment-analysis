readme = """# Bitcoin Sentiment vs Trader Behavior — Hyperliquid Analysis

## Project Overview
This project analyzes how Bitcoin market sentiment (Fear & Greed Index) 
relates to trader performance and behavior on the Hyperliquid DEX.
We use 211,224 trade records across 32 traders (May 2023 – May 2025) 
merged with 2,644 days of sentiment data to uncover patterns and 
derive actionable trading strategies.

---

## Datasets
| Dataset | Source | Rows | Key Columns |
|---------|--------|------|-------------|
| Bitcoin Fear & Greed Index | Alternative.me | 2,644 | date, value, classification |
| Hyperliquid Trader Data | Hyperliquid DEX | 211,224 | Account, Closed PnL, Direction, Size USD, Timestamp IST |

---

## Project Structure
```
bitcoin-sentiment-analysis/
│
├── data/
│   ├── fear_greed_index.csv        # Raw sentiment data
│   ├── trades_raw.csv              # Raw Hyperliquid trade data
│   ├── sentiment_clean.csv         # Cleaned sentiment (3 zones)
│   ├── trades_clean.csv            # Cleaned trades (noise removed)
│   ├── trades_closed.csv           # Closed trades only (realized PnL)
│   ├── daily_pnl.csv               # Daily PnL per account
│   ├── account_perf.csv            # Win rate, avg profit/loss per trader
│   ├── daily_behavior.csv          # Trade count, size, fees per day
│   ├── long_short.csv              # Long/short ratio per account per day
│   ├── drawdown.csv                # Max drawdown per trader
│   ├── master.csv                  # Merged master table (2,300 rows)
│   ├── master_final.csv            # Master + cluster labels
│   └── trader_profiles_clustered.csv  # 32 trader profiles with clusters
│
├── charts/
│   ├── chart1_performance_vs_sentiment.png
│   ├── chart2_behavior_vs_sentiment.png
│   ├── chart3_segment_heatmap.png
│   ├── chart4_insight3.png
│   ├── chart5_strategies.png
│   ├── chart6_elbow.png
│   ├── chart7_clusters_scatter.png
│   ├── chart8_cluster_profiles.png
│   ├── chart9_cluster_sentiment_heatmap.png
│   └── chart10_cluster_bars.png
│
├── notebooks/
│   └── main.ipynb              # Full analysis notebook
│
└── README.md
```

---

## How to Run

### 1. Install dependencies
```bash
pip install pandas numpy matplotlib scikit-learn
```

### 2. Place raw data files in /data/
- `fear_greed_index.csv`
- `trades_raw.csv` (your Hyperliquid export)

### 3. Run the notebook
Open `notebooks/analysis.ipynb` and run all cells in order.
Each step validates outputs before proceeding.

---

## Methodology
| Step | What We Did |
|------|-------------|
| 1 | Data understanding — shape, types, missing values, duplicates |
| 2 | Data cleaning — datetime conversion, noise removal, PnL filtering |
| 3 | Feature engineering — daily PnL, win rate, L/S ratio, drawdown |
| 4 | Dataset merging — trades joined to sentiment on date |
| 5 | Analysis — performance & behavior vs sentiment, segment analysis |
| 6 | Insights — 3 data-backed findings with explanations |
| 7 | Strategies — 3 actionable rules derived from data |
| 8 | Clustering — K-Means (K=4) behavioral archetypes |

---

## Key Insights

### Insight 1 — Traders are Contrarian: Long during Fear, Short during Greed
- Fear Zone L/S ratio: 1.77 (long biased)
- Greed Zone L/S ratio: 0.77 (short biased)
- Position sizes 44% larger during Fear ($8,711 vs $6,033)
- Trade frequency 38% higher during Fear (107 vs 78 trades/day)

### Insight 2 — Frequent Traders Extract 10x More Value
- Frequent traders: $9,439/day (Fear), win rate 70.7%
- Infrequent traders: $880/day (Fear), win rate 52.0%
- Gap widens during volatility — frequent traders capture more opportunities

### Insight 3 — Greed is a Trap for Unprofitable Traders
- Unprofitable traders avg -$9,717/day during Greed (win rate 37.8%)
- Same traders avg +$2,515/day during Fear (win rate 55.7%)
- Euphoria amplifies poor discipline — FOMO leads to catastrophic losses

---

## Trader Clusters (K-Means, K=4)
| Cluster | N | Win Rate | Avg Size | Best Sentiment Zone |
|---------|---|----------|----------|---------------------|
| Whales | 6 | 80.5% | $25,099 | Fear Zone ($9,944/day) |
| Precision Traders | 14 | 94.6% | $5,292 | Fear Zone ($5,890/day) |
| Balanced Traders | 11 | 73.9% | $4,918 | Greed Zone ($5,223/day) |
| Bot/Outlier | 1 | 100.0% | $8,335 | Neutral ($24,765/day) |

---

## Actionable Strategies
1. **Contrarian Activation Rule** — Go long + increase size during Fear; flip short + reduce size during Greed
2. **Greed Zone Survival Rule** — Unprofitable traders cap at 20 trades/day during Greed; preserve capital for Fear windows
3. **Sentiment-Scaled Position Sizing** — 1.4x size in Fear, 1.0x Neutral, 0.7x in Greed

---

## Author
Built as part of a real-world data analysis project.
Tools: Python, Pandas, NumPy, Matplotlib, Scikit-learn
