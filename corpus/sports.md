# Sports corpus

The source of truth the retrieval pipeline grounds superlative answers in. Each row is one competitive field: a sport, discipline, gender category, and age group that share an official record. The corpus stores where the record lives, not the current leaders, so the pipeline always reads rankings from the source.

## Columns

| Column | Meaning |
|---|---|
| `id` | Stable key: `sport-discipline-field-age_group` |
| `sport` | Sport name |
| `discipline` | Format or event within the sport |
| `field` | `Men`, `Women`, or `Open` |
| `eligibility` | Who may enter this field |
| `age_group` | `Senior`, or the junior band (e.g. `U20`) |
| `governing_body` | Organisation that publishes the record |
| `official_website` | Governing body home page |
| `ranking_source` | Official ranking or record list |
| `primary_metric` | The metric the ranking uses |
| `cross_field_comparable` | `Yes`: one shared scale across fields. `Partial`: same units, separate competition. `No`: no shared record. |
| `comparability_note` | Why, in one line |
| `last_verified` | Date the URLs were last checked |

## Fields

[sports.csv](sports.csv) holds the same rows and is the copy to edit; the pipeline reads it. Update this table to match.

| id | sport | discipline | field | eligibility | age_group | governing_body | official_website | ranking_source | primary_metric | cross_field_comparable | comparability_note | last_verified |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| pool-wpa-men-senior | Pool | All disciplines (9-, 10-, 8-ball) | Men | Men | Senior | World Pool-Billiard Association (WPA) | https://wpapool.com | https://wpapool.com/rankings/ | WPA ranking points | No | Men's and women's rankings come from separate events with no shared head-to-head record | 2026-09-28 |
| pool-wpa-women-senior | Pool | All disciplines (9-, 10-, 8-ball) | Women | Women | Senior | World Pool-Billiard Association (WPA) | https://wpapool.com | https://wpapool.com/rankings/ | WPA ranking points | No | Men's and women's rankings come from separate events with no shared head-to-head record | 2026-09-28 |
| pool-wpba-women-senior | Pool | All disciplines (9-, 10-, 8-ball) | Women | Women, WPBA tour | Senior | Women's Professional Billiard Association (WPBA) | https://wpba.com | https://wpba.com/rankings | WPBA ranking points | No | US women's tour; its points do not convert to WPA points | 2026-09-28 |
| cricket-international-men-senior | Cricket | Test, ODI, T20I | Men | Men's international players | Senior | International Cricket Council (ICC) | https://www.icc-cricket.com | https://www.icc-cricket.com/rankings | ICC player rating, per format | No | Men and women play separate fixtures; ratings are computed within each field | 2026-09-28 |
| cricket-international-women-senior | Cricket | ODI, T20I | Women | Women's international players | Senior | International Cricket Council (ICC) | https://www.icc-cricket.com | https://www.icc-cricket.com/rankings | ICC player rating, per format | No | Men and women play separate fixtures; ratings are computed within each field | 2026-09-28 |
| chess-classical-open-senior | Chess | Classical | Open | All players, any gender | Senior | International Chess Federation (FIDE) | https://www.fide.com | https://ratings.fide.com/top_lists.phtml | FIDE Elo rating | Yes | One rating pool for all players, so a single ranking across genders is valid (control case) | 2026-09-28 |
| chess-classical-women-senior | Chess | Classical | Women | Women | Senior | International Chess Federation (FIDE) | https://www.fide.com | https://ratings.fide.com/top_lists.phtml | FIDE Elo rating | Yes | Women's list is a subset of the same rating pool as Open | 2026-09-28 |
| tennis-singles-men-senior | Tennis | Singles | Men | Men | Senior | ATP Tour | https://www.atptour.com | https://www.atptour.com/en/rankings/singles | ATP ranking points | No | ATP and WTA award points on separate tours with no singles matches between them | 2026-09-28 |
| tennis-singles-women-senior | Tennis | Singles | Women | Women | Senior | WTA | https://www.wtatennis.com | https://www.wtatennis.com/rankings/singles | WTA ranking points | No | ATP and WTA award points on separate tours with no singles matches between them | 2026-09-28 |
| tennis-singles-junior | Tennis | Singles | Men, Women | Boys and girls, separate lists | Junior | International Tennis Federation (ITF) | https://www.itftennis.com | https://www.itftennis.com/en/rankings/world-tennis-tour-juniors-rankings/ | ITF junior ranking points | No | Boys' and girls' lists come from separate draws | 2026-09-28 |
| football-national-team-men-senior | Football | National teams | Men | Men's national teams | Senior | FIFA | https://www.fifa.com | https://inside.fifa.com/fifa-rankings/world-ranking/men | FIFA ranking points (teams) | No | Ranks teams, not players; no official record ranks individual players | 2026-09-28 |
| football-national-team-women-senior | Football | National teams | Women | Women's national teams | Senior | FIFA | https://www.fifa.com | https://inside.fifa.com/fifa-rankings/world-ranking/women | FIFA ranking points (teams) | No | Ranks teams, not players; no official record ranks individual players | 2026-09-28 |
| athletics-100m-men-senior | Athletics | 100 m | Men | Men | Senior | World Athletics | https://worldathletics.org | https://worldathletics.org/world-rankings | Time (seconds); World Ranking score | Partial | Times share a unit, but the fields race separately and a faster time does not settle "best athlete" | 2026-09-28 |
| athletics-100m-women-senior | Athletics | 100 m | Women | Women | Senior | World Athletics | https://worldathletics.org | https://worldathletics.org/world-rankings | Time (seconds); World Ranking score | Partial | Times share a unit, but the fields race separately and a faster time does not settle "best athlete" | 2026-09-28 |
| athletics-100m-u20 | Athletics | 100 m | Men, Women | Under 20, separate lists | U20 | World Athletics | https://worldathletics.org | https://worldathletics.org/records/by-category/world-u20-records | Time (seconds), U20 records | Partial | Separate men's and women's U20 records; same caveat as senior | 2026-09-28 |

## Notes

- Every URL returned HTTP 200 on 2026-09-28, except atptour.com, which blocks automated requests (HTTP 403); it is the ATP's official site.
- Football has an official ranking only for teams. Asked for "the best footballer," the pipeline has no record to ground in and should decline to rank, the same as for "the best programmer."
