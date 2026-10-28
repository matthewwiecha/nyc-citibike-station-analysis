# NYC Citi Bike Station Activity and Imbalance (June 2026)

**Matthew Wiecha** · Urban planning and transportation data analysis

A Python/Jupyter analysis of trip patterns and station-level bike/dock pressure *indicators* using June 2026 Citi Bike trip-history records. The original exploration combined six monthly CSV parts (approximately 5.38 million trips) and examined weekday morning-start trips.

## Research question

Where do arrivals and departures create relatively large directional imbalances during the weekday morning commute—and how much trip activity accompanies those imbalances?

## Approach

1. Combine the June 2026 Citi Bike trip-history CSV parts and parse trip timestamps.
2. Review hourly trip-start patterns, weekday/weekend variation, and rider type.
3. Select trips **starting on weekdays from 7:00 a.m. through 9:59 a.m.**
4. Build station departure and arrival events; group events in 15-minute bins.
5. Calculate **net flow = arrivals − departures** and **total activity = arrivals + departures**.
6. For each station and clock-time bin, calculate an average across dates **on which events occurred**. Compare its most negative and most positive average flows, and use the larger absolute extreme to represent each station in a scatterplot.

A large negative net flow suggests potential **bike pressure** (more departures than arrivals); a large positive flow suggests potential **dock pressure** (more arrivals than departures). Total activity helps distinguish heavily used locations from quieter stations with similar imbalances.

## Files

- [`citibike_station_analysis_clean.ipynb`](citibike_station_analysis_clean.ipynb) — documented analysis notebook
- `station_imbalance_scatter.png` — generated when the notebook runs
- `citibike_station_imbalance_summary.csv` — generated station-level export

## Run locally

1. Install Python 3 and Jupyter.
2. Install dependencies: `pip install pandas matplotlib numpy openpyxl jupyter`.
3. Download **June 2026** trip-history data from [Citi Bike System Data](https://citibikenyc.com/system-data), and place the six CSV parts in a folder named `data/` next to the notebook. Expected filenames: `202606-citibike-tripdata_1.csv` through `_6.csv`.
4. Open the notebook and run the cells in order. **Raw trip data is not included** in this repository.

## Methodological limitations

- **These are imbalance indicators, not observed empty/full stations.** The analysis does not measure station inventory, capacity, or rebalancing.
- The trip cohort is defined by **start time**. Its arrival events may occur after 10 a.m.; it is not a complete time-bounded station inventory series.
- Station/time averages exclude calendar dates with **zero recorded events**, so they are conditional averages and may be higher than averages over all weekdays.
- Station names rather than IDs identify stations, so station renaming or duplicate names may affect grouping.

## Next steps

Integrate historical station availability and capacity, use event timestamps to define a fixed morning window, include zero-activity station intervals, and test sensitivity to the choice of peak period.

## Author

[Matthew Wiecha](https://www.matthewwiecha.com) — urban planning, transportation analysis, public space, and data analysis.
