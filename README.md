## IPL Winning Strategy Analysis – Final Report

<img width="1353" height="737" alt="Page 1" src="https://github.com/user-attachments/assets/d65bc263-0f4d-4ff4-85cf-803dd0ba8828" />
<img width="1347" height="737" alt="Page2" src="https://github.com/user-attachments/assets/a4256c94-fb35-41b6-804a-0cfaf4eaaff1" />

1. Problem Statement
The objective of this project is to analyze IPL match data to identify factors that increase the chances of winning matches.
The analysis focuses on:
•	Which teams perform best at certain venues
•	Impact of toss decision
•	Key performance indicators for winning
•	Player performance patterns
•	Match scoring patterns
The goal is to provide strategies to improve winning probability.
________________________________________
2. Dataset Used
Dataset used:
•	matches.csv
•	deliveries.csv
Matches table contains match-level data.
Deliveries table contains ball-by-ball data.
Key columns used:
Matches table:
•	id: Unique match identifier
•	season: IPL season of the match
•	venue: Stadium where match was played
•	team1: First team playing the match
•	team2: First team playing the match
•	toss_winner: Team that won the toss
•	toss_decision: Decision taken after toss
•	winner: Decision taken after toss
•	target_runs: Target score for second inning team
•	target_overs: Number of overs available for chasing team
Deliveries table:
•	match_id: Foreign key linking to matches table
•	inning: Inning number
•	over: Over number (1–20)
•	batter: Player who is batting
•	bowler: Player who is bowling
•	batting_team: Team currently batting
•	total_runs: Total runs scored in that ball
•	is_wicket: Indicates if wicket fell

Relationship created:
matches[id] → deliveries[match_id]
One to many

________________________________________
3. Data Cleaning
Steps performed:
•	Converted numeric columns to whole number
•	Fixed target_runs type	
•	Filtered inning to only 1 and 2
•	Checked null values
•	Verified relationships
________________________________________
4. Calculated Columns
Toss Match Win
Toss Match Win =
IF(matches[toss_winner] = matches[winner], 1, 0)
Used to check if toss winner won match.
Chase Win
Chase Win =
IF(
matches[toss_decision] = "field"
&& matches[winner] = matches[toss_winner],
1,
0
)
Used to check if chasing team won.
Bat Win
Bat Win =
IF(
matches[toss_decision] = "bat"
&& matches[winner] = matches[toss_winner],
1,
0
)
Used to check batting first win.

5. Measures Created
Matches table :
Total Matches
Total Matches =
COUNT(matches[id])
Toss Win %
Toss Win % =
DIVIDE(
SUM(matches[Toss Match Win]),
COUNT(matches[id])
)
Chase Win %
Chase Win % =
DIVIDE(
SUM(matches[Chase Win]),
COUNT(matches[id])
)
Bat Win %
Bat Win % =
DIVIDE(
SUM(matches[Bat Win]),
COUNT(matches[id])
)

Average Score
Avg Score =
AVERAGE(matches[target_runs])
Highest Score
Highest Score =
MAX(matches[target_runs])
Matches Won
Matches Won =
COUNT(matches[winner])




Deliveries table:
Total Runs
Total Runs =
SUM(deliveries[total_runs])
Total Wickets
Total Wickets =
SUM(deliveries[is_wicket])
Total Balls
Total Balls =
COUNT(deliveries[ball])
Avg Runs
Avg Runs =
AVERAGE(deliveries[total_runs])
________________________________________
6. Dashboard Page 1 – IPL Winning Strategy Analysis
KPI’s:
	Total Matches
Shows total matches analyzed.
Used to understand dataset size.

	Toss Win %
Shows percentage of matches where toss winner also won.
Used to measure toss advantage.

	Chase Win %
Shows how often chasing team wins.
Used to analyze strategy.

	Average Score
Shows average target score.
Used to find safe score.

	Highest Score
Shows highest target.
Used to understand scoring range.
Charts:
	Chart – Wins by Team
Shows number of wins per team.
Used to identify strongest teams.



	Chart – Toss Winner vs Match Winner
Shows toss impact.
Used to check advantage.

	Chart – Bat vs Chase Strategy
Shows wins based on toss decision.
Used to see best strategy.

	Chart – Average Score by Venue
Shows venue scoring pattern.
Used for venue strategy.

	Chart – Matches Won by Venue
Shows which venue has more wins.
Used to analyze venue performance.

	Chart – Winning Score Distribution
Shows score range where most matches are won.
Used to find safe target.
________________________________________
7. Dashboard Page 2 – Player & Match Performance Impact
KPI’s:
	Total Runs
Total runs scored in dataset.
Used to measure scoring.

	Total Wickets
Total wickets.
Used to measure bowling impact.

	Total Balls
Total deliveries.
Used to calculate averages.

	Avg Run / Ball
Average runs per ball.
Used to check scoring rate.

	Total Matches
Total matches analyzed.
Charts:
	Chart – Top Run Scorers
Shows best batsmen.
Used to analyze player impact.

	Chart – Top Wicket Takers
Shows best bowlers.
Used to analyze bowling impact.

	Chart – Team Scoring Performance
Shows runs per team.
Used to check team strength.

	Chart – Runs by Over
Shows scoring pattern per over.
Used to analyze powerplay and death overs.

	Chart – Wickets by Over
Shows wicket pattern.
Used to identify pressure overs.

	Chart – Run Share by Inning
Shows runs in 1st vs 2nd inning.
Used to analyze chasing vs batting.
________________________________________
8. Key Insights
1.	Toss has moderate impact (~50%).
2.	Chasing teams win more often.
3.	Winning score usually 150–180.
4.	Some venues have higher scores.
5.	Death overs have highest runs.
6.	Top players influence results.
7.	First inning scores slightly higher.
________________________________________
9. Strategy Recommendations
•	Prefer chasing on good pitches.
•	Target 160+ runs.
•	Use aggressive death overs.
•	Select high-performing players.
•	Analyze venue before toss.
________________________________________
10. Conclusion
Winning depends on:
•	Toss decision
•	Venue conditions
•	Score range
•	Player performance
•	Over strategy

