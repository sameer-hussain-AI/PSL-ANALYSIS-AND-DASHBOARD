# PSL Cricket Analytics — Power BI

## Project Overview
An interactive **Pakistan Super League (PSL) Cricket Analytics Dashboard** built in Power BI using ball-by-ball match data. The project transforms detailed delivery-level data into executive KPIs, team performance views, player analysis, bowling insights, and season trends.

### Dataset Coverage
- **Matches:** 357
- **Deliveries:** 83,799
- **Seasons:** 2016–2026 (11 seasons)
- **Teams represented:** 8
- **Wickets:** 4,503
- **Fours:** 10,006
- **Sixes:** 4,541
- **Total runs:** 115,022
- **Venues:** 7
- **Cities:** 7

## Dashboard Structure
1. **Executive Overview** — headline KPIs, season-level trends and league-wide scoring picture.
2. **Team Performance** — team batting output, scoring efficiency, boundaries and comparative performance.
3. **Player Performance** — leading run scorers, strike rates, boundary contribution and player comparisons.
4. **Bowling Performance** — wickets, runs conceded, economy and bowling effectiveness.
5. **Season / Match Analysis** — changes in scoring, wickets and playing patterns over time.

## Data Model
The project uses a Power BI model built around:
- **PSL Teams** — team dimension
- **PSL Players** — player dimension
- **PSL Match Players** — player participation/roster bridge
- **PSL Match Info** — match-level information
- **PSL Ball by Ball Merged** — delivery-level fact table

Key relationships connect players and teams to participation data and match information to ball-by-ball events.

## Main KPIs
- Matches Played
- Total Runs
- Total Wickets
- Fours
- Sixes
- Run Rate / scoring rate
- Team and player strike rate
- Bowling economy
- Wicket contribution

## Analytical Approach
The dashboard follows a simple analytics workflow:

**Raw ball-by-ball data → Power Query cleaning → Data model → DAX measures → Visual analysis → Cricket/business insights**

Important data-quality checks include match IDs, team/player names, legal-ball logic, wickets, extras, boundaries and season fields.

## Key Findings From the Current Dataset

### Batting
**Babar Azam** is the leading run scorer in the supplied dataset with **4,380 runs**, followed by **Fakhar Zaman (3,370)** and **Mohammad Rizwan (2,974)**.

### Team Scoring
**Peshawar Zalmi** has the highest aggregate batters' runs in the supplied ball-by-ball data with **19,353 runs**. **Islamabad United** follows with **18,685**.

### Boundary Profile
Across the dataset there are **10,006 fours** and **4,541 sixes**, showing the importance of boundary scoring in PSL run production.

### Bowling
The wicket leaderboard is headed by **Hasan Ali (140 wickets)** in the supplied data.

## Important Interpretation Note
The dashboard should distinguish **aggregate totals** from **rate-based metrics**. A team with more matches or seasons represented can naturally accumulate more runs or wickets. For fair comparisons, use strike rate, economy, run rate, per-match averages and season filters alongside cumulative totals.

## Portfolio Value
This project demonstrates:
- Power BI dashboard development
- Power Query data preparation
- DAX KPI creation
- Relational data modeling
- Sports analytics
- Trend and comparative analysis
- Business-style insight communication

## Suggested GitHub Repository Structure
```text
PSL-Cricket-Analytics/
├── data/
│   └── PSL_ball_by_ball_merged.csv
├── powerbi/
│   └── PSL_Cricket_Analytics.pbix
├── screenshots/
│   ├── executive-overview.png
│   ├── team-performance.png
│   ├── player-performance.png
│   └── bowling-performance.png
├── README.md
└── insights.pdf
```

## Tools
**Power BI • Power Query • DAX • CSV • Data Modeling • Sports Analytics**

---
*Prepared as a portfolio project documentation file. Metrics above are calculated from the supplied merged ball-by-ball dataset.*
