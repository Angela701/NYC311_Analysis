
-- 1. Source of request with relation to number of closed tickets 

select distinct source
, count(request_id) as num_reqs
, date_part('year', "closed_date")
from nyc_311_2018
where status = 'Closed'
group by 1, 3
having count(request_id) > 1000
and date_part('year', "closed_date") = 2018 -- change to 2019 to see this year 
union  
select distinct source
, count(request_id) as num_reqs
, date_part('year', "closed_date")
from nyc_311_2019
where status = 'Closed'
group by 1, 3
having count(request_id) > 1000
and date_part('year', "closed_date") = 2018 -- change to 2019 to see this year 
order by 2 desc
limit 1000; 

-- 2. Type of request with relation to time to close requests 

-- year 2018
select requesttype
	, date_part('minute', closed_date) as time_close_ticket
from nyc_311_2018
where status = 'Closed' 
and date_part('minute', closed_date) is not null
order by 2 desc 

-- year 2019
select requesttype
	, date_part('minute', closed_date) as time_close_ticket
from nyc_311_2019
where status = 'Closed' 
and date_part('minute', closed_date) is not null
order by 2 desc 

-- 3. Agency with relation to closed ticket requests 

-- 2018 query
select distinct agency_code
	, count(request_id) as num_reqs
from nyc_311_2018
where status = 'Closed'
group by 1 
order by 2 desc

-- 2019 query
select distinct agency_code
	, count(request_id) as num_reqs
from nyc_311_2019
where status = 'Closed'
group by 1 
order by 2 desc

-- 4. Incident location with relation to time to close tickets 

-- 2018 query
select locationtype
	, date_part('minute', closed_date) as min_tickets_closed
from nyc_311_2018
where status = 'Closed' 
and date_part('minute', closed_date) is not null 
and locationtype is not null
order by 2 desc

-- 2019 query
select locationtype
	, date_part('minute', closed_date) as min_tickets_closed
from nyc_311_2019
where status = 'Closed' 
and date_part('minute', closed_date) is not null 
and locationtype is not null
order by 2 desc

-- 5. Landmark with relation to time to close tickets 

-- 2018 query 
select distinct landmark
	, count(request_id) as num_reqs
	, date_part('hour', closed_date) as hour 
	, case 
		when date_part('hour', closed_date) = 1 then '1AM'
		when date_part('hour', closed_date) = 2 then '2AM'
		when date_part('hour', closed_date) = 3 then '3AM'
		when date_part('hour', closed_date) = 4 then '4AM'
		when date_part('hour', closed_date) = 5 then '5AM'
		when date_part('hour', closed_date) = 6 then '6AM'
		when date_part('hour', closed_date) = 7 then '7AM'
		when date_part('hour', closed_date) = 8 then '8AM'
		when date_part('hour', closed_date) = 9 then '9AM'
		when date_part('hour', closed_date) = 10 then '10AM'
		when date_part('hour', closed_date) = 11 then '11AM'
		when date_part('hour', closed_date) = 12 then '12PM'
		when date_part('hour', closed_date) = 13 then '1PM'
		when date_part('hour', closed_date) = 14 then '2PM'
		when date_part('hour', closed_date) = 15 then '3PM'
		when date_part('hour', closed_date) = 16 then '4PM'
		when date_part('hour', closed_date) = 17 then '5PM'
		when date_part('hour', closed_date) = 18 then '6PM'
		when date_part('hour', closed_date) = 19 then '7PM'
		when date_part('hour', closed_date) = 20 then '8PM'
		when date_part('hour', closed_date) = 21 then '9PM'
		when date_part('hour', closed_date) = 22 then '10PM'
		when date_part('hour', closed_date) = 23 then '11PM'
		when date_part('hour', closed_date) = 24 then '12AM'
	end as time 
from nyc_311_2018
where landmark is not null 
and date_trunc('hour', closed_date) is not null
group by 1,3
order by 2 desc 

-- 2019 query
select distinct landmark
	, count(request_id) as num_reqs
	, date_part('hour', closed_date) as hour 
	, case 
		when date_part('hour', closed_date) = 1 then '1AM'
		when date_part('hour', closed_date) = 2 then '2AM'
		when date_part('hour', closed_date) = 3 then '3AM'
		when date_part('hour', closed_date) = 4 then '4AM'
		when date_part('hour', closed_date) = 5 then '5AM'
		when date_part('hour', closed_date) = 6 then '6AM'
		when date_part('hour', closed_date) = 7 then '7AM'
		when date_part('hour', closed_date) = 8 then '8AM'
		when date_part('hour', closed_date) = 9 then '9AM'
		when date_part('hour', closed_date) = 10 then '10AM'
		when date_part('hour', closed_date) = 11 then '11AM'
		when date_part('hour', closed_date) = 12 then '12PM'
		when date_part('hour', closed_date) = 13 then '1PM'
		when date_part('hour', closed_date) = 14 then '2PM'
		when date_part('hour', closed_date) = 15 then '3PM'
		when date_part('hour', closed_date) = 16 then '4PM'
		when date_part('hour', closed_date) = 17 then '5PM'
		when date_part('hour', closed_date) = 18 then '6PM'
		when date_part('hour', closed_date) = 19 then '7PM'
		when date_part('hour', closed_date) = 20 then '8PM'
		when date_part('hour', closed_date) = 21 then '9PM'
		when date_part('hour', closed_date) = 22 then '10PM'
		when date_part('hour', closed_date) = 23 then '11PM'
		when date_part('hour', closed_date) = 24 then '12AM'
	end as time 
from nyc_311_2019
where landmark is not null 
and date_trunc('hour', closed_date) is not null
group by 1,3
order by 2 desc 

-- 6. Seasonality with relation to number of tickets closed 

-- 2018 query
select date_part('month', closed_date) as month
	, count(request_id) as num_reqs
	, case 
		when date_part('month', closed_date) = 1 then 'January'
		when date_part('month', closed_date) = 2 then 'February'
		when date_part('month', closed_date) = 3 then 'March'
		when date_part('month', closed_date) = 4 then 'April'
		when date_part('month', closed_date) = 5 then 'May'
		when date_part('month', closed_date) = 6 then 'June'
		when date_part('month', closed_date) = 7 then 'July'
		when date_part('month', closed_date) = 8 then 'August'
		when date_part('month', closed_date) = 9 then 'September'
		when date_part('month', closed_date) = 10 then 'October'
		when date_part('month', closed_date) = 11 then 'November'
		when date_part('month', closed_date) = 12 then 'December'
	end as month
from nyc_311_2018
where status = 'Closed' and status is not null
group by 1,3 
order by 2 desc 


--2019 query
select date_part('month', closed_date) as month
	, count(request_id) as num_reqs
	, case 
		when date_part('month', closed_date) = 1 then 'January'
		when date_part('month', closed_date) = 2 then 'February'
		when date_part('month', closed_date) = 3 then 'March'
		when date_part('month', closed_date) = 4 then 'April'
		when date_part('month', closed_date) = 5 then 'May'
		when date_part('month', closed_date) = 6 then 'June'
		when date_part('month', closed_date) = 7 then 'July'
		when date_part('month', closed_date) = 8 then 'August'
		when date_part('month', closed_date) = 9 then 'September'
		when date_part('month', closed_date) = 10 then 'October'
		when date_part('month', closed_date) = 11 then 'November'
		when date_part('month', closed_date) = 12 then 'December'
	end as month
from nyc_311_2019
where status = 'Closed' and status is not null
group by 1,3 
order by 2 desc 


-- 7. Request detail with relation to number of closed tickets 

-- 2018 query
select request_details
	, count(request_id) as num_reqs
from nyc_311_2018
where status = 'Closed'
group by 1
order by 2 desc

-- 2019 query
select request_details
	, count(request_id) as num_reqs
from nyc_311_2019
where status = 'Closed'
group by 1
order by 2 desc

-- 8. Average response time in relation to number of closed tickets 

-- 2018 query
select extract('minute' from closed_date) as closed_req_min
	, count(request_id) as num_reqs 
	, request_details
from nyc_311_2018
where status = 'Closed'
group by 1,3
order by 2 desc 

-- 2019 query
select extract('minute' from closed_date) as closed_req_min
	, count(request_id) as num_reqs 
	, request_details
from nyc_311_2019
where status = 'Closed'
group by 1,3
order by 2 desc 




