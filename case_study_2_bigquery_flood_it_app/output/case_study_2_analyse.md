Hypothese 1:
Die Anzahl aktiver Nutzer nimmt über einen Zeitraum von 2 Monaten zu.

Vorgehen:
Aktiven Nutzer nach Tag analysieren. Hier zunächst einmal eine Gruppierung über die Zeit, evtl erst einmal Buckets(Woche)

Wie ändert sich das Nutzerverhalten über Zeit? Nimmt das VErhgalten der Aktiven Nutzer zu oder nimmt es ab?


SQL Query um Nutzer pro Tag zu zählen

SELECT  event_timestamp as event_date,
COUNT(DISTINCT user_id) 
FROM `firebase-public-project.analytics_153293282.events_*`
GROUP BY event_timestamp
LIMIT 10

SQL Query um 2 Wochen Buckets zu vollziehen

-- CTE für Tägliche User 
WITH daily_users AS (
SELECT DATE(event_timestamp) as event_date,
count(DISTINCT user_id) AS dist_user
FROM `firebase-public-project.analytics_153293282.events_*`
GROUP BY event_date
),
--CTE für 2 Wochen Buckets 
buckets as (
SELECT event_date, dist_user,
DATE_TRUNC(event_date, WEEK(MONDAY)) + Interval (FLOOR(DATE_DIFF(event_date, WEEK(MONDAY)), DAY)/14) *14 DAY as start_bucket
FROM daily_users
)
--Query mit Sum user, AVG user pro Tag, Count tage im Bucket
SELECT bucket_start, SUM(dist_user) AS dist_user_in_bucket, AVG(dist_user) AS avg_dist_user_per_day, COUNT(*) AS days_in_bucket 
FROM buckets
--Pro bucket und sortiert
GROUP BY bucket_start 
ORDER BY bucket_start


