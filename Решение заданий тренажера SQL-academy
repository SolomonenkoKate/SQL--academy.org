# Задание 1. Вывести имена всех людей, которые есть в базе данных авиакомпаний

SELECT name
FROM Passenger

# Задание 2. Вывести названия всеx авиакомпаний

SELECT name
from Company

# Задание 3. Вывести все рейсы, совершенные из Москвы

SELECT *
FROM trip
WHERE town_from = 'Moscow'

# Задание 4. Вывести имена людей, которые заканчиваются на "man"

SELECT name
FROM passenger
WHERE name LIKE '%man'

# Задание 5. Вывести количество рейсов, совершенных на TU-134

SELECT COUNT(*) AS COUNT
FROM Trip
WHERE plane = 'TU-134'

# Задание 6. Какие компании совершали перелеты на Boeing

SELECT DISTINCT name
FROM Company
	JOIN Trip ON Company.id = Trip.company
WHERE Trip.plane = 'Boeing'

# Задание 7. Вывести все названия самолётов, на которых можно улететь в Москву (Moscow)

SELECT DISTINCT plane
FROM Trip
WHERE town_to = 'Moscow'

# Задание 8. В какие города можно улететь из Парижа (Paris) и сколько времени это займёт?

SELECT town_to,
	TIMEDIFF(time_in, time_out) AS flight_time
FROM Trip
WHERE town_from = 'Paris'

SELECT town_to,
	sec_to_time(TIMESTAMPDIFF(SECOND, time_out, time_in)) AS flight_time
FROM Trip
WHERE town_from = 'Paris'

# Задание 9. Какие компании организуют перелеты из Владивостока (Vladivostok)?

SELECT name
FROM Company
	JOIN Trip ON Company.id = Trip.company
WHERE town_from = 'Vladivostok'

# Задание 10. Вывести вылеты, совершенные с 10 ч. по 14 ч. 1 января 1900 г.

SELECT *
FROM Trip
WHERE time_out BETWEEN '1900-01-01 10:00:00' AND '1900-01-01 14:00:00'

# Задание 11. Выведите пассажиров с самым длинным ФИО. Пробелы, дефисы и точки считаются частью имени.

SELECT name
FROM Passenger
WHERE LENGTH(name) = (
		SELECT MAX(LENGTH(name))
		FROM Passenger
	)

# Задание 12. Выведите идентификаторы всех рейсов и количество пассажиров на них. Обратите внимание, что на каких-то рейсах пассажиров может не быть. В этом случае выведите число "0".

SELECT trip,
	COUNT(passenger) AS COUNT
FROM Pass_in_trip
GROUP BY trip

# Задание 13. Вывести имена людей, у которых есть полный тёзка среди пассажиров

SELECT name
FROM passenger
GROUP BY name
HAVING COUNT(name) > 1
