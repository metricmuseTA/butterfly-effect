# 🦋 The Butterfly Effect
### How Short-Form Content Changed Audience Behavior in Film

> *"Did short-form content actually change audience behavior — or does it just feel that way?"*

A collaborative data research project by **Tiffani Anderson** and **Muhammad Monis**.

---

## The Project

TikTok didn't just change how we scroll. We built the data to find out if it changed how we watch everything else.

Across 50 films, two decades, and four data sources, we traced the butterfly effect of short-form content through Hollywood — from how films are made, to how they're marketed, to how audiences react and talk about them.

---

## Key Findings

- **Before 2015, zero films in our dataset were over-hyped.** Every film either matched or exceeded audience expectations.
- **After 2015, over-hyping became a measurable pattern.** The hype gap narrowed from −22.84 (Pre Short-Form) to −10.49 (Short-Form Era).
- **Audience retention dropped 16%** between eras — Short-Form Era films lost interest faster post-release.
- **Runtime shifts were uneven by genre** — Drama and Action-based films expanded while Comedy-led combinations compressed.
- **The language of film criticism shifted** — time-friction complaints ("too slow", "too long") increasingly replaced craft-based critique.

---

## The Four Chapters

| Chapter | Topic | Owner |
|---|---|---|
| 1 | Runtime Compression | Monis (Power BI) |
| 2 | Hype vs Reality | Tiffani (Databricks) |
| 3 | NLP Language Shift | Both |
| 4 | Full Case Study | Both |

---

## Data Sources

| Source | What We Pulled | How |
|---|---|---|
| **Google Trends** | Pre & post-release search interest per film | pytrends Python library |
| **YouTube Data API v3** | Trailer view counts, likes, comment counts | Google Cloud API key |
| **IMDb Bulk Dataset** | Ratings, runtime, genres, vote counts | datasets.imdbws.com (free) |
| **IMDb Reviews** | Review text for NLP analysis | Kaggle dataset |

---

## Pipeline Architecture

Built on **Databricks** using the **Bronze / Silver / Gold medallion architecture**.
```
Bronze → Raw ingestion from all four sources
Silver → Cleaned, joined, and normalized
Gold   → Analysis-ready tables (Hype Gap, NLP scores, Trends Combined)
```

**Bronze tables:**
- `google_trends_raw` — 4,550 rows (50 films × 91 days pre-release)
- `google_trends_postrelease_raw` — 4,550 rows (50 films × 91 days post-release)
- `youtube_trailers_raw` — 50 rows (one per film)
- `imdb_ratings_raw` — 49 rows

**Silver tables:**
- `trends_silver` — aggregated pre-release hype metrics
- `trends_postrelease_silver` — aggregated post-release decay metrics
- `trends_combined` — pre vs post release comparison (4 columns Monis uses)
- `youtube_silver` — cleaned trailer stats with engagement rate
- `film_master` — all sources joined on film title

**Gold tables:**
- `hype_gap_table` — hype index, reaction score, verdict per film
- `nlp_language_shift` — vocabulary bucket scores by year and era *(in progress)*

---

## Tech Stack

**Tiffani (Pipeline & Architecture)**
- Databricks (Bronze/Silver/Gold medallion pipeline)
- Python (pytrends, google-api-python-client, pandas, pyspark)
- Google Trends API (via pytrends)
- YouTube Data API v3
- IMDb bulk datasets

**Monis (Analysis & Visualization)**
- Power BI
- Data cleaning and preparation
- IMDb data sourcing

---

## Film List

50 films across two eras:

**Pre Short-Form Era (2005–2014) — 19 films**
Batman Begins, Brokeback Mountain, Casino Royale, The Departed, Ratatouille, No Country for Old Men, There Will Be Blood, The Dark Knight, The Hangover, Avatar, Inception, The Social Network, Paranormal Activity, Bridesmaids, Gravity, The Wolf of Wall Street, The Conjuring, Gone Girl, Interstellar

**Short-Form Era (2015–2025) — 31 films**
Mad Max: Fury Road, The Revenant, La La Land, Get Out, It, Black Panther, Crazy Rich Asians, A Quiet Place, Hereditary, Bohemian Rhapsody, Joker, Parasite, Tenet, Dune, The Batman, Top Gun: Maverick, Everything Everywhere All at Once, Morbius, Nope, The Menu, Oppenheimer, Barbie, The Flash, Indiana Jones and the Dial of Destiny, Five Nights at Freddy's, Poor Things, Dune: Part Two, Inside Out 2, Deadpool & Wolverine, Alien: Romulus, Wicked

---

## Repository Structure
```
butterfly-effect/
├── notebooks/          # Databricks pipeline notebooks
│   ├── bronze/         # Raw data ingestion
│   ├── silver/         # Cleaning and joining
│   └── gold/           # Analysis tables
├── dashboard/          # Interactive HTML dashboard
├── case-study/         # PDF case study
└── assets/             # Chart screenshots
```

---

## Collaborators

**Tiffani Anderson** — Pipeline architecture, data engineering, Databricks
[LinkedIn](https://www.linkedin.com/in/tiffani-anderson-821130363) | [Metric Muse](https://www.linkedin.com/in/company/metricmuse)

**Muhammad Monis** — Data analysis, Power BI visualization, data cleaning
[LinkedIn](https://www.linkedin.com/in/muhammad-monis/)

---

## Status

- [x] Bronze pipeline — all 4 data sources ingested
- [x] Silver pipeline — cleaned and joined
- [x] Gold pipeline — hype gap table complete
- [x] Interactive HTML dashboard
- [x] Chapter 1 published (Runtime Compression)
- [x] Chapter 2 published (Hype vs Reality)
- [ ] NLP pipeline (in progress)
- [ ] Chapter 3 (NLP Language Shift)
- [ ] Chapter 4 (Full Case Study)
- [ ] Project website

---

*Built with Databricks · Google Trends · YouTube API · IMDb · Power BI*# butterfly-effect
Data pipeline analyzing how short-form content changed audience behavior across 50 films and two eras. Built with Databricks, Google Trends, YouTube API, and IMDb.
