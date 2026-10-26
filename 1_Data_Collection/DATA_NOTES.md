# Olympic dataset – build notes (1992–2026)

Source: the three uploaded CSVs (athletes, editions, medal_results). Nothing was invented. `sports_investment` is NOT available and is not included.

## Files (load all in Tableau; relate on `games` + `noc_code`)
| File | Grain | Rows |
|---|---|---|
| athletes.csv | one row per athlete-event | 166,194 |
| medal_results.csv | one row per NOC per Games (incl. zero-medal NOCs) | 2,608 |
| games_summary.csv | one row per Games | 19 |
| alltime_country_rankings.csv | one row per NOC | 218 |
| noc_reference.csv | NOC -> country name, region, entity type | 219 |

## Relationship key
Use `games` (e.g. "1992 Summer") with `noc_code`. `year` alone is NOT unique: 1992 has both a Summer and a Winter Games.

## Added fields
- region (7 regions from the original brief + Neutral/Refugee + Unknown). Europe/Asia = ARM AZE GEO KAZ RUS ROC TUR EUN. Region assignment is my own mapping; review it.
- sport_category: my own grouping of the 54 sports into 18 categories (not the original 21).
- athletes_sent = unique athlete IDs per NOC per Games.
- medal_points = 3*gold + 2*silver + 1*bronze.
- medal_efficiency_pct = total medals / athletes_sent * 100 (can exceed 100, e.g. LUX 1992 Winter: 1 athlete, 2 medals). Team medals count once in the medal table, so this is not a pure per-athlete rate.
- is_host, host_city, host_country, host_noc.

## Known data issues
1. 3,907 athlete rows have no NOC (all in 2018–2026). 57 were recovered from the same athlete's other rows in the same Games; 3,850 remain `UNK`. Those NOCs cannot be reliably inferred. None of the unknown rows are medallists.
2. Because of (1), athletes_sent is understated for real countries in 2018+ editions. `efficiency_reliable` = 0 for those Games; do not compare efficiency across that boundary without a caveat.
3. For 1992–2016 the athlete file matches official `participants` within a few athletes. For 2018+ it exceeds official figures by roughly 100–220 per Games (cause unknown).
4. EUN, TCH, YUG, SCG, AHO, COR are kept as separate historical entities; ROC and RUS are separate; AIN, EOR, IOA, ROT are Neutral/Refugee. All-time rankings therefore split Russia/USSR-era results.
5. Accented characters in athlete names are missing in the source (e.g. "Andrs"); not fixable here.
6. Athlete-level medal counts (athletes.csv) count every team member; they will NOT equal medal_results totals. Do not mix them on one chart.
7. Medal total check: gold/silver/bronze/total in medal_results.csv sum to exactly the original file (11,106 medals).
