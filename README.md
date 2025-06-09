<h1 align="center">Всем привет!<img src="https://github.com/blackcater/blackcater/raw/main/images/Hi.gif" height="32"/> 
<h2 align="center">Здесь вы найдете мои решения заданий от SQL-academy (https://sql-academy.org/) </h2>
</h1>



### Задание 1. Вывести имена всех людей, которые есть в базе данных авиакомпаний
<details> 
SELECT name
FROM Passenger
</details> 


### Задание 2. Вывести названия всеx авиакомпаний
<details> 
SELECT name
from Company
</details>  


### Задание 3. Вывести все рейсы, совершенные из Москвы
<details> 
SELECT *
FROM trip
WHERE town_from = 'Moscow'
</details> 


### Задание 4. Вывести имена людей, которые заканчиваются на "man"
<details> 
SELECT name
FROM passenger
WHERE name LIKE '%man'
</details> 


### Задание 5. Вывести количество рейсов, совершенных на TU-134
<details>  
SELECT COUNT(*) AS COUNT
FROM Trip
WHERE plane = 'TU-134'
</details> 


### Задание 6. Какие компании совершали перелеты на Boeing
<details> 
SELECT DISTINCT name
FROM Company
	JOIN Trip ON Company.id = Trip.company
WHERE Trip.plane = 'Boeing'
</details> 


### Задание 7. Вывести все названия самолётов, на которых можно улететь в Москву (Moscow)
<details> 
SELECT DISTINCT plane
FROM Trip
WHERE town_to = 'Moscow'
</details> 


### Задание 8. В какие города можно улететь из Парижа (Paris) и сколько времени это займёт?

<details> 
	
#### вариант 1
SELECT town_to,
	TIMEDIFF(time_in, time_out) AS flight_time
FROM Trip
WHERE town_from = 'Paris'


#### вариант 2
SELECT town_to,
	sec_to_time(TIMESTAMPDIFF(SECOND, time_out, time_in)) AS flight_time
FROM Trip
WHERE town_from = 'Paris'
</details> 


### Задание 9. Какие компании организуют перелеты из Владивостока (Vladivostok)?
<details> 
SELECT name
FROM Company
	JOIN Trip ON Company.id = Trip.company
WHERE town_from = 'Vladivostok'
</details> 


### Задание 10. Вывести вылеты, совершенные с 10 ч. по 14 ч. 1 января 1900 г.
<details> 
SELECT *
FROM Trip
WHERE time_out BETWEEN '1900-01-01 10:00:00' AND '1900-01-01 14:00:00'
</details> 


### Задание 11. Выведите пассажиров с самым длинным ФИО. Пробелы, дефисы и точки считаются частью имени.
<details> 
SELECT name
FROM Passenger
WHERE LENGTH(name) = (
		SELECT MAX(LENGTH(name))
		FROM Passenger
	)
 </details> 
 

### Задание 12. Выведите идентификаторы всех рейсов и количество пассажиров на них. Обратите внимание, что на каких-то рейсах пассажиров может не быть. В этом случае выведите число "0".
<details> 
SELECT trip,
	COUNT(passenger) AS COUNT
FROM Pass_in_trip
GROUP BY trip
</details> 


### Задание 13. Вывести имена людей, у которых есть полный тёзка среди пассажиров
<details>
SELECT name
FROM passenger
GROUP BY name
HAVING COUNT(name) > 1
</details>

### Задание 14. В какие города летал Bruce Willis
<details>
SELECT town_to
FROM trip
	JOIN Pass_in_trip ON Trip.id = Pass_in_trip.trip
	JOIN Passenger ON Pass_in_trip.passenger = Passenger.id
WHERE Passenger.name = 'Bruce Willis'
</details>

### Задание 15. Выведите идентификатор пассажира Стив Мартин (Steve Martin) и дату и время его прилёта в Лондон (London)
<details>
SELECT Passenger.id,
	time_in
FROM Trip
	JOIN Pass_in_trip ON Trip.id = Pass_in_trip.trip
	JOIN Passenger ON Pass_in_trip.passenger = Passenger.id
WHERE Passenger.name = 'Steve Martin'
	AND town_to = 'London'
</details>

### Задание 16. Вывести отсортированный по количеству перелетов (по убыванию) и имени (по возрастанию) список пассажиров, совершивших хотя бы 1 полет.
<details>
	
#### вариант 1
	SELECT name,
	COUNT(Pass_in_trip.id) AS COUNT
FROM Pass_in_trip
	JOIN Passenger ON Pass_in_trip.passenger = Passenger.id
WHERE Pass_in_trip.passenger = Passenger.id
GROUP BY Passenger.name
ORDER BY COUNT(Pass_in_trip.id) DESC, name

#### вариант 2
SELECT name,
	COUNT(*) AS count
FROM Passenger
	JOIN Pass_in_trip on Pass_in_trip.passenger = Passenger.id
GROUP BY passenger
HAVING COUNT(trip) > 0
ORDER by COUNT(trip) DESC, name
</details>


