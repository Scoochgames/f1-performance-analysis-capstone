# F1 Performance Analysis: A Data-Driven Look at Formula 1 (1950–2024)

Capstone project analyzing Formula 1 racing data from 1950 to 2024, sourced from the Ergast Developer API via Kaggle.

---

## About the Data

This dataset is from Kaggle ([accessible here](https://www.kaggle.com/datasets/rohanrao/formula-1-world-championship-1950-2020)), originally compiled from the Ergast Developer API. It covers every Formula 1 season from 1950 to 2024 across 14 CSV files. All 14 tables were loaded into Google BigQuery and joined into a single master view called `f1_master` for analysis. Each record in the master view represents one driver's result in one race, and includes:

- **year / round / race_name / race_date:** When and where the race took place
- **circuit_name / country:** The track and country it was held in
- **forename / surname / driver_nationality:** Driver identification and nationality
- **constructor_name / constructor_nationality:** The team the driver raced for
- **grid:** The driver's starting position on the grid
- **position / positionOrder:** Finishing position (position is null for non-finishers; positionOrder always has a value)
- **points:** Championship points earned in the race
- **laps:** Number of laps completed
- **finish_time:** Total race time for classified finishers
- **fastestLapTime / fastestLapSpeed:** The driver's fastest lap in the race
- **status:** How the race ended (Finished, Retired, Accident, etc.)
- **quali_position / q1 / q2 / q3:** Qualifying session times and final grid position
- **total_pit_stops / avg_pit_duration_ms / first_pit_lap:** Pit stop summary per driver per race
- **avg_lap_ms / best_lap_ms / worst_lap_ms / lap_time_stddev:** Lap time statistics per driver per race

Several columns in the raw data use `\N` as a placeholder for missing values. These were replaced with nulls directly in the BigQuery view. Qualifying, pit stop, and lap time data is limited before 2011, so analysis using those fields focuses on the 2011–2024 period.

---

## Project Overview

**Problem Statement:** Formula 1 produces a huge amount of data, but it rarely gets looked at across the full history of the sport. The goal of this project is to find patterns in over 70 years of race data — which teams have dominated, whether starting position actually determines the winner, how pit stop strategy affects results, what makes a consistent driver, and how much faster cars have gotten at the circuits that show up year after year.

**Research Questions:**

- Which constructors have dominated F1 over the past two decades, and how has the competitive balance between teams shifted over time?
- How does qualifying grid position relate to final race finishing position? Does starting near the front actually determine who wins?
- What is the relationship between pit stop strategy (number of stops, timing, and duration) and where a driver finishes the race?
- Which drivers show the most consistent lap times across a season, and does that consistency track with championship results?
- How have average lap times at major circuits changed over the years?
- What do DNF and reliability patterns look like across constructors?
