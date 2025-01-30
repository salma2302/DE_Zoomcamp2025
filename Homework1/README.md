# Module 1 Homework: Docker & SQL

## Question 1 

We run this command :

**`docker run -it python:3.12.8 bash`**


## Question 3

#### Up to 1:

**`
SELECT
    count(*)
FROM 
    yellow_taxi_data t
WHERE
	(trip_distance <= 1) and
	cast(t.lpep_pickup_datetime as date) >= '2019-10-01' and cast(t.lpep_pickup_datetime as date) < '2019-11-01'
;
`**

#### Query "between 1 and 3":

**`
SELECT
    count(*)
FROM 
    yellow_taxi_data t
WHERE
	(trip_distance > 1 and trip_distance <= 3) and
	cast(t.lpep_pickup_datetime as date) >= '2019-10-01' and cast(t.lpep_pickup_datetime as date) < '2019-11-01'
;
`**

#### Query "between 3 and 7":

**`
SELECT
    count(*)
FROM 
    yellow_taxi_data t
WHERE
	(trip_distance > 3 and trip_distance <= 7) and
	cast(t.lpep_pickup_datetime as date) >= '2019-10-01' and cast(t.lpep_pickup_datetime as date) < '2019-11-01'
;
`**

#### between 7 and 10:

**`
SELECT
    count(*)
FROM 
    yellow_taxi_data t
WHERE
	(trip_distance > 7 and trip_distance <= 10) and
	cast(t.lpep_pickup_datetime as date) >= '2019-10-01' and cast(t.lpep_pickup_datetime as date) < '2019-11-01'
;
`**

#### Over 10 miles

**`
SELECT
    count(*)
FROM 
    yellow_taxi_data t
WHERE
	(trip_distance > 10) and
	cast(t.lpep_pickup_datetime as date) >= '2019-10-01' and cast(t.lpep_pickup_datetime as date) < '2019-11-01'
;
`**

### Question 4
**`
SELECT
	cast(t.lpep_pickup_datetime as date),
    Max(t.trip_distance) as max_trip
FROM 
    yellow_taxi_data t
GROUP BY 
	cast(t.lpep_pickup_datetime as date)
ORDER BY 
	max_trip desc
;
`**

### Question 5:

**`
SELECT
	zpu."Zone",
    count(t.total_amount) as ta
FROM 
    yellow_taxi_data t
INNER JOIN 
    zones zpu ON t."PULocationID" = zpu."LocationID"
INNER JOIN
    zones zdo ON t."DOLocationID" = zdo."LocationID"
WHERE
	total_amount >= 13.000 and cast(t.lpep_pickup_datetime as date) = '2019-10-18'
GROUP BY
	zpu."Zone"
ORDER BY 
	ta desc
LIMIT 5;
`**

### Question 6 :

**`
SELECT
	zpu."Zone",
	SUM(t.tip_amount)
FROM 
    yellow_taxi_data t
INNER JOIN 
    zones zpu ON t."PULocationID" = zpu."LocationID"
INNER JOIN
    zones zdo ON t."DOLocationID" = zdo."LocationID"
WHERE
	 zpu."Zone" = 'East Harlem North' and cast(t.lpep_pickup_datetime as date) = '2019-10-01'
GROUP BY 
	zpu."Zone";
`**




