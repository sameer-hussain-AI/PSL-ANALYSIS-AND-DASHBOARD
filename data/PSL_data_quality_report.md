# PSL Data Quality Report

- Match files found / parsed: **357 / 357**; unparsed: **0**
- Source ball rows: **83,799** -> delivery rows written: **83,799** (none lost; re-read from disk OK)
- Match-info rows: **357**; duplicate match_ids: **0**; duplicate delivery_ids: **0**
- Deliveries with null match_id: **0**; delivery match_ids not in match info: **0**; matches with no deliveries: **0**
- Reconciliation: 153 win-by-runs and 193 win-by-wickets margins, and 346 chase targets, all agree with the ball-by-ball totals (0 mismatches); toss decision agrees with who batted first in every match; player runs/wickets sum to delivery totals.

## Known source-data characteristics (not parsing errors)

- 3 no-result matches have only 1 innings: [1075994, 1211660, 1475258]
- 4 matches went to a super over (innings 3-4, 50 deliveries).
- 2 overs contain 7 legal balls in the source (match, innings, over, balls): [[1168820, 1, 2, 7], [1416502, 1, 11, 7]]
- City is blank in the source for 43 matches (Dubai / Sharjah); filled in `city_clean`.
- match_number is blank for 44 matches (mostly playoffs); the source has no stage/playoff field.
- Match-id gaps (ids absent from the archive; reason not determinable from the data): {'2018': [1128828], '2020': [1211654, 1211666, 1211674], '2024': [1416488, 1416489], '2026': [1527558]}
- 1 fielder name (`Usman Khan`, delivery 1247024-2-11.05) is missing from that match's registry -> fielder_1_id is blank for that row.
- Cricsheet disambiguates same-name players with suffixes, and one player can appear under two spellings across matches. 3,007 deliveries involve a suffixed name. **Use the *_id columns / PSL_players.player_id for player identity**; names alone can merge different people (Mohammad Irfan, Imran Khan, Mohammad Imran, Khurram Shahzad, Tayyab Abbas).

## Missing values (important columns)

| Dataset | Column | Missing |
|---|---|---|
| ball_by_ball | city | 9,887 |
| ball_by_ball | dismissal_kind | 79,293 |
| ball_by_ball | player_dismissed | 79,293 |
| ball_by_ball | player_dismissed_id | 79,293 |
| ball_by_ball | fielder_1 | 80,756 |
| ball_by_ball | fielder_1_id | 80,757 |
| match_info | match_number | 44 |
| match_info | city | 43 |
| match_info | winner | 7 |
| match_info | super_over_winner | 353 |
| match_info | win_margin | 7 |
| match_info | dls_method | 353 |
| match_info | target_runs | 3 |
| match_info | player_of_match | 5 |
| match_info | player_of_match_id | 5 |
| match_info | tv_umpire | 6 |
| match_info | reserve_umpire | 26 |
| match_info | match_referee | 11 |
| match_info | innings2_runs | 3 |

(dismissal / fielder columns are blank by design on non-wicket deliveries; superover/dls/winner/margin columns are blank when not applicable.)