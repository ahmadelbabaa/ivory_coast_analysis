# AFCON Match Analysis

## Project Overview
This project analyzes match data from the **Africa Cup of Nations (AFCON)**, with a specific focus on **Ivory Coast's performance before and after a managerial change** during the tournament. The analysis is conducted using **StatsBombR**, **SBpitch**, and **soccermatics** libraries in R.

## Features
- **Fetches match data** from the free StatsBomb API.
- **Filters AFCON matches** to focus on a specific competition.
- **Analyzes Ivory Coast’s matches** before and after a managerial change.
- **Processes event data** for in-depth tactical analysis.
- **Visualizes match statistics** and performance changes.

## Installation

To run this analysis, ensure you have the following R packages installed:

```r
install.packages("devtools")
devtools::install_github("StatsBomb/StatsBombR")
install.packages("SBpitch")
install.packages("soccermatics")
```

## Data Extraction

The script fetches match data using the StatsBomb API:

```r
comps <- FreeCompetitions()
matches <- FreeMatches(comps)

afcon_matches <- matches %>% 
  filter(competition.competition_id == 1267) # AFCON Competition ID
```

## Ivory Coast Match Filtering

Ivory Coast’s matches are filtered into **pre- and post-managerial change** phases:

```r
ivory_coast_team_ID = 3374

# Group Stage (Before Manager Change)
ic_pre_manager_change <- afcon_matches %>% 
  filter(home_team.home_team_id == ivory_coast_team_ID | 
         away_team.away_team_id == ivory_coast_team_ID) %>% 
  filter(match_week < 4) %>% # Pre-managerial change (Group Stage)
  arrange(match_date)

# Knockout Stage (After Manager Change)
ic_post_manager_change <- afcon_matches %>% 
  filter(home_team.home_team_id == ivory_coast_team_ID | 
         away_team.away_team_id == ivory_coast_team_ID) %>% 
  filter(match_week >= 4) %>% # Post-managerial change (Knockout Stage)
  arrange(match_date)
```

## Event Data Processing

Event-level data is retrieved and cleaned:

```r
sbdata_pre <- free_allevents(MatchesDF = ic_pre_manager_change, Parallel = T)
sbdata_pre <- allclean(sbdata_pre)

sbdata_post <- free_allevents(MatchesDF = ic_post_manager_change, Parallel = T)
sbdata_post <- allclean(sbdata_post)
```

## Analysis and Visualization

- **Performance before and after the managerial change**
- **Match event statistics**
- **Tactical analysis using visualizations**

## Usage

1. Run the R script inside a **Quarto (qmd)** or R Markdown file.
2. Analyze the outputs and compare team performance before and after the managerial change.

## Authors
- IE Sports Analytics Club