# Volleyball Statistics Tracker

## 1. The demo

I open a terminal in the project folder and run **`streamlit run app.py`**. The browser opens the Volleyball Statistics Tracker with the included `data/sample_matches.csv`; I select **Match 01** and the page shows the six player records, team statistics, and calculated attack and serve efficiency. I select **Anna Kovacs** in the comparison section and the application shows her statistics for Match 01 and Match 02, including attack efficiency changing from 0.35 to 0.46. I upload another CSV with the same format, and the application validates it before displaying the results; a CSV with a missing required column is rejected with the column name shown as the reason.

## 2. The shape

```text
in     a CSV export containing one row per player per match, with match,
       team, player, position, attack, serve, reception and block statistics

out    validated match data, team/player summaries, player comparisons,
       and a downloadable player-statistics CSV

in between   validate the CSV → aggregate statistics → calculate
             performance efficiencies → filter by match/player → display
             tables and comparisons
```

## 3. The size

**First useful version**

- load the included sample CSV or upload another CSV with the documented format
- validate required columns and basic impossible values
- select a match and view its raw player records
- calculate team and player statistics
- calculate attack efficiency as `(kills - attack_errors) / attacks`
- calculate serve efficiency as `(aces - serve_errors) / serves`
- compare one player's attack and serve efficiency across matches
- download the displayed player statistics as a CSV

**Not this term**

- live, point-by-point match recording
- video analysis or automatic player tracking
- replacing professional systems such as Data Volley
- mobile application
- user accounts, authentication or cloud storage
- machine-learning predictions of match results
- automatic scraping of every volleyball website
- persistent online rankings or public player profiles

## 4. How we would know it works

- Given a record with 10 attacks, 6 kills and 2 attack errors, the application calculates an attack efficiency of **0.40**.
- Given a CSV missing the required `player` column, the application stops processing the file and reports `player` as a missing required column.
- Given a record with a negative number of attacks, the application flags the file instead of calculating statistics from invalid data.

Automated versions of these checks are in `tests/test_statistics.py` and can be run with:

```bash
pytest
```

## 5. What could stop this

- **Data availability and consistency.** Volleyball statistics are not necessarily exported in the same format by every source. The project therefore defines one CSV schema and includes a small sample dataset that can be used without an external website.
- **Real-world data access.** Public volleyball statistics may change format or may not be available for redistribution. The application does not depend on scraping a website: the core workflow works from a local CSV file.
- **Data privacy.** The sample contains fictional player names and no private information. The classroom demonstration can therefore be performed without personal or sensitive data.
- **Scope.** Live scoring, video analysis, player tracking and machine learning could each become separate projects. They are explicitly outside the first useful version.
- **Technical risk.** The calculated statistics need known examples so that the formulas can be checked independently. The test suite contains a hand-calculated attack-efficiency example.

The project runs locally and does not require an account, API key, database or internet connection after the Python packages have been installed.


