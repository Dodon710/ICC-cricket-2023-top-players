# ICC-cricket-2023-top-players
-- top 5 run scorer --
SELECT striker, sum(runs_off_bat) as total_runs
FROM `virtual-stratum-447213-m7.cricketICC.Deliveries`
group by striker
order by total_runs desc
limit 5

-- Top 5 batsman by most sixes --

SELECT striker, sum(runs_off_bat) as total_sixes
FROM `virtual-stratum-447213-m7.cricketICC.Deliveries`
where runs_off_bat = 6
group by striker
order by total_sixes desc
limit 5

-- Top 5 teams by most sixes --

SELECT batting_team, sum(runs_off_bat) as total_sixes
FROM `virtual-stratum-447213-m7.cricketICC.Deliveries`
where runs_off_bat = 6
group by batting_team
order by total_sixes desc
limit 5

-- Top 5 highest batting average 

select striker, match_played,
 round(case when match_played > 0 then cast(total_runs as int) / match_played else 0
  end, 1) as average
from (SELECT striker, count(distinct match_id) as match_played, sum(runs_off_bat) as total_runs
FROM `virtual-stratum-447213-m7.cricketICC.Deliveries`
group by striker)
order by average desc
limit 5

-- top 10 wicket taker --

SELECT bowler, count(wicket_type) as wicket
FROM `virtual-stratum-447213-m7.cricketICC.Deliveries`
where wicket_type is not null
group by bowler
order by wicket desc
limit 10

-- top 10 most expensive bowler --

SELECT bowler, sum(runs_off_bat) as runs_given
FROM `virtual-stratum-447213-m7.cricketICC.Deliveries`
group by bowler
order by runs_given desc
limit 10

-- most match winner --

select winner as team, count(*) as won
from virtual-stratum-447213-m7.cricketICC.Matches
group by winner
order by won desc
