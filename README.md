# docker-zoomcamp

## Question 1. Understanding Docker images
Run docker with the python:3.13 image. Use an entrypoint bash to interact with the container.

What's the version of pip in the image?
25.3


## Question 2. Understanding Docker networking and docker-compose
Given the following docker-compose.yaml, what is the hostname and port that pgadmin should use to connect to the postgres database?
postgres:5432


## Question 3. Counting short trips
SELECT COUNT(*)
FROM green_taxi_2025_11
WHERE lpep_pickup_datetime >= '2025-11-01'
  AND lpep_pickup_datetime < '2025-12-01'
  AND trip_distance <= 1;

8,007

## Question 4
SELECT
    DATE(lpep_pickup_datetime) AS pickup_day,
    MAX(trip_distance) AS max_distance
FROM green_taxi_2025_11
WHERE trip_distance < 100
GROUP BY pickup_day
ORDER BY max_distance DESC
LIMIT 1

## Question 5
SELECT
    z.Zone,
    SUM(t.total_amount) AS total_amount_sum
FROM green_taxi_2025_11 t
JOIN taxi_zone_lookup z
    ON t.PULocationID = z.LocationID
WHERE DATE(t.lpep_pickup_datetime) = '2025-11-18'
GROUP BY z.Zone
ORDER BY total_amount_sum DESC
LIMIT 1;

## Question 6
SELECT
    z_do.Zone,
    SUM(t.tip_amount) AS total_tip
FROM green_taxi_2025_11 t
JOIN taxi_zone_lookup z_pu
    ON t.PULocationID = z_pu.LocationID
JOIN taxi_zone_lookup z_do
    ON t.DOLocationID = z_do.LocationID
WHERE z_pu.Zone = 'East Harlem North'
  AND DATE(t.lpep_pickup_datetime) >= '2025-11-01'
  AND DATE(t.lpep_pickup_datetime) < '2025-12-01'
GROUP BY z_do.Zone
ORDER BY total_tip DESC
LIMIT 1;
