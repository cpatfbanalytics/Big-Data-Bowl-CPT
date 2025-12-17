# Coverage Performance Tracking (CPT): NFL Defensive Back Ball-Tracking Metric

**NFL Big Data Bowl 2026 Submission (University Track)**

A novel metric that quantifies defensive back ball-tracking technique using NFL Next Gen Stats tracking data. CPT measures how effectively DBs locate and track the football during its flight, isolating technique from situational factors.

## 🏈 Key Findings

- **34 percentage point gap** in completion rate between elite (D10) and poor (D1) ball-trackers
- **4.5× higher ball production** for elite technique vs poor technique
- **Statistically significant** (p < 0.001) after controlling for route depth, separation, coverage scheme
- **Situationally stable** across route depths (<1% variation) and coverage schemes

## 📊 What is CPT?

CPT combines three components measured during ball flight:

1. **Head-Turn Timing (55% weight)**: When DB's movement aligns with ball trajectory
2. **Ball Leverage (35% weight)**: Positioning relative to ball path at arrival
3. **Late Risk Indicator (-60% penalty)**: Closing hard without ball awareness

Final scores calibrated via logistic regression predicting P(INT or PBU), yielding interpretable probability scale from 0 (poor technique) to 1 (elite technique).

## 🎯 Practical Applications

### Weekly Scouting
Identify exploitable matchups: DBs below 0.480 CPT are high-priority targets. Elite QBs already target weaker ball-trackers (0.4907 vs 0.4962 CPT), achieving 5.4pp higher completion rates.

### Player Development
CPT diagnoses technique from 25-30 plays (vs 100+ for outcome metrics), enabling faster feedback loops. Components isolate specific breakdowns for targeted coaching.

### Game Planning
Optimize DB-route matchups. Elite CPT DBs show 38pp advantage on short routes where technique matters most.

## 📈 Top Performers (2023 Season)

| Rank | Player | CPT | Comp% Allowed | Ball Productions |
|------|--------|-----|---------------|------------------|
| 1 | Darrell Baker | 0.537 | 67.6% | 5 |
| 2 | Ahkello Witherspoon | 0.535 | 53.6% | 10 |
| 3 | Ambry Thomas | 0.534 | 62.1% | 6 |
| 4 | Charvarius Ward | 0.532 | 59.6% | 9 |
| 5 | Carrington Valentine | 0.529 | 64.7% | 5 |

*Minimum 25 plays, n=101 qualifying DBs*

## 🔬 Methodology

### Data Processing
- **Dataset**: 7,958 plays from 2023 NFL regular season
- **Source**: NFL Next Gen Stats tracking data + nflverse play-by-play
- **Filtering**: Excluded deep zone responsibilities where DBs defend areas vs receivers

### Context Normalization
Raw metrics residualized against coverage scheme × route depth baskets to isolate player skill from assignment difficulty. Z-scored residuals ensure DBs are evaluated relative to situational demands.

### Validation
- **Decile analysis**: Monotonic relationship across full CPT range
- **Logistic regression**: Coefficient -2.08 (p < 0.001), controls for depth/separation/scheme
- **Situational stability**: <1% variance across depths, identical means across Man/Zone
- **Player consistency**: Within-player SD = 0.016 vs between-player SD = 0.077

## 🚀 Getting Started

### Prerequisites
```bash
pip install polars pyarrow scikit-learn matplotlib pandas numpy statsmodels
```

### Running the Analysis
```python
# Load notebook
jupyter notebook notebooks/cpt_analysis.ipynb

# Or run cells sequentially:
# Cell 0: Setup and imports
# Cell 0B: Load player roster (name mapping)
# Cells 1-2: Load and integrate tracking + coverage data
# Cells 3-6: Compute CPT components and calibrate
# Cell 7: Decile analysis
# Cell 8: QB exploitation validation
# Cells 9-10: Route-specific and regression analysis
# Cell 11: Player rankings
# Cell 12: Situational stability
```

## 📊 Data Requirements

### Required Files
- **NFL Tracking Data**: `input_2023_w[1-9].csv`, `output_2023_w[1-9].csv`
- **Play-by-Play**: `supplementary_data.csv` (from BDB 2026 competition)
- **Coverage Data**: SumerSports coverage responsibilities (optional but recommended)
- **Roster Data**: Loaded automatically from nflverse

### Data Format
Tracking data at 10 Hz (0.1s per frame). Input frames cover pre-snap through ball release. Output frames cover ball flight through arrival.

## 🎓 Statistical Details

### Model Specifications
- **Family**: Logistic regression (binary outcome: ball production)
- **Features**: HTL_frac_z, Lev_z, LateRisk
- **Class balancing**: Applied (12.8% base rate)
- **Performance**: AUC 0.782, Brier score 0.187
- **Sample size**: 7,958 plays, 593 defensive backs

### Key Parameters
- **Head-turn threshold**: 0.7 dot product (45° cone)
- **Late risk threshold**: < 2 yards separation
- **Minimum plays**: 25 for player rankings
- **Context buckets**: 2 schemes × 3 depths = 6 categories

## 🏆 Competition Details

**NFL Big Data Bowl 2026 - University Track**

**Submission Components:**
- Kaggle Writeup (1,497 words)
- Public Notebook (12 analysis cells)
- 9 Visualizations (under 10-figure limit)

**Evaluation Criteria:**
- Football Score (30%): Week-to-week actionable, accounts for complexity, unique
- Data Science Score (30%): Correct methodology, validated claims, innovative
- Writeup Score (20%): Well-written, clear motivation, easy to follow
- Visualization Score (20%): Accessible, accurate, innovative

## 🔮 Future Enhancements

- **Route-specific weights**: Optimize HTL/Lev importance by route tree branch
- **Pre-snap integration**: Combine with alignment metrics for comprehensive evaluation
- **Real-time computation**: Deploy for in-game coaching adjustments
- **Predictive modeling**: Aging curves, injury recovery, rookie projection
- **Cross-sport applications**: Baseball outfielders, basketball help defense, soccer goalkeepers

## 📝 Citation

If you use this work, please cite:
```bibtex
@misc{cpt2026,
  title={Coverage Performance Tracking: Measuring Defensive Back Ball-Tracking Technique},
  author={[Your Name]},
  year={2026},
  howpublished={NFL Big Data Bowl 2026 Submission},
  url={https://github.com/[your-username]/cpt-metric}
}
```

## 📧 Contact

**Author**: Conor Patten  
**Email**: conor.patten@duke.edu 
**LinkedIn**: https://www.linkedin.com/in/conor-patten/
**Kaggle**: https://www.kaggle.com/conorpatten

## 🙏 Acknowledgments

- NFL and AWS for providing Next Gen Stats tracking data
- SumerSports for coverage responsibility classifications
- nflverse for play-by-play data and roster information
- Big Data Bowl organizing committee and judges

---

**Built with**: Python • Polars • scikit-learn • statsmodels • matplotlib

**Competition**: NFL Big Data Bowl 2026 (University Track)

**Status**: 🚀 Submitted Dec 2025
