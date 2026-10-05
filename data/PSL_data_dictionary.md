# PSL Analytics - Data Dictionary & QA Report

Source: Cricsheet "All Men's Pakistan Super League" CSV archive (psl_male_csv.zip, format version 1.8.0). "DERIVED" = computed here; everything else is the source data (blank cells stay blank).

## PSL_ball_by_ball_merged.csv  (83,799 rows x 49 columns)

| Column | Description |
|---|---|
| `match_id` | Cricsheet match id (from file name; verified against info row). Key to PSL_match_info. |
| `delivery_id` | Unique delivery key: matchid-innings-overindex.deliveryinover (e.g. 1075986-1-00.01). |
| `innings_ball_seq` | Row order of the delivery within its innings, exactly as in the source file (1..N). |
| `season` | Cricsheet season label, unchanged (e.g. 2016/17, 2021). NB: Cricsheet splits the 2020 and 2021 editions oddly - use psl_year for a clean edition. |
| `psl_year` | DERIVED. Calendar year of the match date = PSL edition year (2016-2026). |
| `date` | Match date, ISO yyyy-mm-dd. |
| `venue` | Venue name as in source (spelling varies by season for the same ground). |
| `venue_clean` | DERIVED. Standardised venue name (Gaddafi / National / Sheikh Zayed stadium variants merged). |
| `city` | City as in source (blank for 43 matches at Dubai/Sharjah venues). |
| `city_clean` | DERIVED. City looked up from venue_clean using the source's own populated city values. |
| `innings` | Innings number (1-2; 3-4 are super overs). |
| `is_super_over` | DERIVED. 1 if the innings is a super over (from the info super_over rows). |
| `batting_team` | Batting team (source). |
| `bowling_team` | DERIVED. The other team in the match. |
| `over` | DERIVED. Over number, 1-based (1-20). Use this for powerplay/phase logic. |
| `over_index` | Over number 0-based, as Cricsheet stores it (0-19). |
| `ball` | Cricsheet-style legal ball number in the over (source 2nd over.ball label). Wides/no-balls carry the number of the legal ball that follows. Can reach 7 in the 2 overs with 7 legal balls. |
| `delivery_in_over` | Sequential delivery count in the over including wides/no-balls (source 1st over.ball label); can exceed 6. |
| `over_ball_seq_raw` | Original source label for delivery_in_over (text, e.g. "17.7"). |
| `over_ball_legal_raw` | Original source label for ball (text). |
| `batter` | Striker, exactly as in source. May carry a Cricsheet disambiguation suffix, e.g. "Mohammad Irfan (4)". Use batter_id for reliable identity. |
| `batter_id` | Cricsheet registry id of the striker (join to PSL_players.player_id). |
| `non_striker` | Non-striker (source). |
| `non_striker_id` | Registry id of the non-striker. |
| `bowler` | Bowler (source). |
| `bowler_id` | Registry id of the bowler. |
| `runs_off_bat` | Runs scored off the bat. |
| `extras` | Total extras on the delivery (= wides+noballs+byes+legbyes+penalty; verified on every row). |
| `total_runs` | DERIVED. runs_off_bat + extras. |
| `wides` | Wide runs (blank in source -> 0). |
| `noballs` | No-ball extra runs (blank -> 0). |
| `byes` | Bye runs (blank -> 0). |
| `legbyes` | Leg-bye runs (blank -> 0). |
| `penalty` | Penalty runs (blank -> 0). |
| `is_legal_ball` | DERIVED. 1 if the delivery is not a wide or no-ball. |
| `non_boundary` | Source flag converted to 1/0: 4/6 runs that were run rather than hit to the boundary. |
| `is_four` | DERIVED. 1 if runs_off_bat = 4 and non_boundary = 0. |
| `is_six` | DERIVED. 1 if runs_off_bat = 6 and non_boundary = 0. |
| `dismissal_kind` | Kind of dismissal (source). Includes retired hurt / retired out / obstructing the field. |
| `player_dismissed` | Dismissed batter (source name). |
| `player_dismissed_id` | Registry id of dismissed batter. |
| `is_wicket` | DERIVED. 1 if a wicket fell: any dismissal_kind except "retired hurt" (3 rows keep their kind but score 0). |
| `is_bowler_wicket` | DERIVED. 1 if credited to the bowler: bowled, caught, caught and bowled, lbw, stumped, hit wicket. |
| `fielder_1` | First fielder involved (catcher / keeper / run-out fielder). |
| `fielder_1_id` | Registry id. |
| `fielder_2` | Second fielder (run-outs). |
| `fielder_2_id` | Registry id. |
| `fielder_3` | Third fielder (run-outs). |
| `fielder_3_id` | Registry id. |

## PSL_match_info.csv  (357 rows x 53 columns)

| Column | Description |
|---|---|
| `match_id` | Primary key. |
| `season` | Cricsheet season label (unchanged). |
| `psl_year` | DERIVED. Calendar year = PSL edition year. |
| `psl_edition` | DERIVED. PSL edition number (2016 = 1 ... 2026 = 11). |
| `date` | ISO date. |
| `match_number` | Match number in the tournament (blank for 44 matches, mostly playoffs; not in source). |
| `event` | Event name. |
| `match_type` | T20. |
| `gender` | male. |
| `team_type` | club. |
| `overs` | Scheduled overs per innings. |
| `balls_per_over` | Balls per over. |
| `venue` | Venue (source). |
| `venue_clean` | DERIVED. Standardised venue. |
| `city` | City (source; blank for Dubai/Sharjah early seasons). |
| `city_clean` | DERIVED. Standardised city. |
| `neutral_venue` | 1 if Cricsheet flagged a neutral venue; 0 = not flagged (Cricsheet only writes the flag when true). |
| `team_1` | First team in the source info rows (order carries no meaning: not home/away/toss). |
| `team_2` | Second team. |
| `toss_winner` | Toss winner. |
| `toss_loser` | DERIVED. Other team. |
| `toss_decision` | bat / field. |
| `batting_first_team` | DERIVED from ball-by-ball (innings 1 batting team). |
| `batting_second_team` | DERIVED (innings 2 batting team). |
| `result` | Normalised result: win / tie / no result. |
| `winner` | Outright winner (source); blank for ties and no results. |
| `super_over_winner` | Winner of the super over in tied matches (source "eliminator"). |
| `final_winner` | DERIVED. winner, else super_over_winner. |
| `has_super_over` | 1 if a super over was played. |
| `win_margin_type` | runs / wickets. |
| `win_margin` | Numeric margin. |
| `win_margin_text` | e.g. "58 runs". |
| `win_by_runs` | Source winner_runs. |
| `win_by_wickets` | Source winner_wickets. |
| `dls_method` | D/L when applied (source method). |
| `target_runs` | Target set for innings 2 (source). |
| `target_overs` | Overs for the target, cricket notation (9.4 = 9 overs 4 balls). |
| `innings1_runs` | DERIVED. Innings 1 total (incl. extras). |
| `innings1_wickets` | DERIVED. |
| `innings1_legal_balls` | DERIVED. |
| `innings2_runs` | DERIVED (blank for 3 no-result matches with 1 innings). |
| `innings2_wickets` | DERIVED. |
| `innings2_legal_balls` | DERIVED. |
| `total_deliveries` | DERIVED. All delivery rows for the match incl. super over. |
| `player_of_match` | Player of the match (source; blank for 5). |
| `player_of_match_id` | Registry id. |
| `umpire_1` | On-field umpire. |
| `umpire_2` | On-field umpire. |
| `tv_umpire` | TV umpire. |
| `reserve_umpire` | Reserve umpire. |
| `match_referee` | Match referee. |
| `data_version` | Cricsheet CSV format version. |
| `source_file` | Originating file in the ZIP. |

## PSL_players.csv  (466 rows x 39 columns)

| Column | Description |
|---|---|
| `player_id` | Cricsheet registry id (primary key). |
| `player` | Canonical name (disambiguation suffix removed). |
| `player_unique` | player, plus [id prefix] when the same name belongs to different people - safe for visuals. |
| `name_shared_by_multiple_ids` | 1 if another player id has the same name. |
| `name_variants` | All name strings used for this id in the source. |
| `teams` | Teams played for, in chronological order, "|" separated. |
| `team_count` | Number of teams. |
| `first_psl_year` | First edition year. |
| `last_psl_year` | Last edition year. |
| `seasons_played` | Number of editions. |
| `first_match_date` | ISO date. |
| `last_match_date` | ISO date. |
| `matches` | Matches in a squad/XI list or seen batting/bowling. |
| `substitute_fielder_only` | 1 = only appears as a fielder (never in an XI list). |
| `innings_batted` | Innings at the crease (batter, non-striker or dismissed). Excludes super overs. |
| `not_outs` | innings_batted - times_out. |
| `times_out` | Dismissals (excl. retired hurt). |
| `runs` | Runs off the bat. |
| `balls_faced` | Balls faced (excl. wides). |
| `fours` | Fours. |
| `sixes` | Sixes. |
| `highest_score` | Highest innings score. |
| `fifties` | 50-99 scores. |
| `hundreds` | 100+ scores. |
| `batting_average` | runs / times_out. |
| `batting_strike_rate` | runs x 100 / balls_faced. |
| `innings_bowled` | Innings bowled in. |
| `balls_bowled` | Legal balls bowled. |
| `overs_bowled` | Cricket notation (e.g. 3.4). |
| `runs_conceded` | Bat runs + wides + no-balls (byes/leg-byes/penalty excluded). |
| `wickets` | Bowler-credited wickets. |
| `bowling_average` | runs_conceded / wickets. |
| `economy_rate` | Runs per 6 balls. |
| `bowling_strike_rate` | Balls per wicket. |
| `wides_bowled` | Wide deliveries. |
| `noballs_bowled` | No-ball deliveries. |
| `catches` | Catches (incl. caught & bowled). |
| `stumpings` | Stumpings. |
| `player_of_match_awards` | Player-of-the-match awards. |

## PSL_teams.csv  (8 rows x 19 columns)

| Column | Description |
|---|---|
| `team` | Team name. |
| `first_psl_year` | First edition. |
| `last_psl_year` | Last edition. |
| `seasons_played` | Editions played. |
| `seasons` | Edition years, "|" separated. |
| `matches` | Matches in the data. |
| `wins` | Outright wins (incl. D/L). |
| `losses` | Outright losses. |
| `ties` | Tied matches. |
| `super_over_wins` | Ties won in the super over. |
| `super_over_losses` | Ties lost in the super over. |
| `no_results` | No-result matches. |
| `win_pct` | (wins + super_over_wins) / (matches - no_results) x 100. |
| `toss_wins` | Tosses won. |
| `matches_batting_first` | Matches batting first. |
| `wins_batting_first` | Wins (incl. super over) batting first. |
| `matches_chasing` | Matches batting second. |
| `wins_chasing` | Wins (incl. super over) chasing. |
| `players_used` | Distinct players used. |

## PSL_match_players.csv  (7,858 rows x 10 columns)

| Column | Description |
|---|---|
| `match_id` | Key to match info. |
| `season` | Cricsheet season label. |
| `psl_year` | DERIVED edition year. |
| `date` | ISO date. |
| `team` | Team. |
| `player` | Name as in source. |
| `player_id` | Registry id (key to PSL_players). |
| `in_squad_list` | 1 = listed in the match info player rows (XI; 12 for 4 team-matches); 0 = added because seen batting/bowling. |
| `batted` | DERIVED. At the crease in innings 1-2. |
| `bowled` | DERIVED. Bowled in innings 1-2. |
