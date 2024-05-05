Если таблица не существует или имеет другое определение пересоздаем таблицу
````
CREATE TABLE `city` (
`city_id` smallint unsigned NOT NULL AUTO_INCREMENT,
`city` varchar(50) NOT NULL,
`country_id` smallint unsigned NOT NULL,
`last_update` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
PRIMARY KEY (`city_id`)
) ENGINE=InnoDB AUTO_INCREMENT=601 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci
````

Отбрасываем табличное пространство созданной таблицы
>alter table city discard tablespace

Копируем файлы  city.cfg, city.ibd на сервер
>cp /var/lib/mysql/sakila/city.ibd /var/lib/mysql/nasa/city.ibd
>cp /var/lib/mysql/sakila/city.cfg /var/lib/mysql/nasa/city.cgf

Устанавливаем владельца
>chown mysql city.*

Устанавливаем табличное пространство для таблицы
>alter table city import tablespace

Проверяем
>select * from city c 
````
1	A Coruña (La Coruña)	87	2006-02-15 04:45:25
2	Abha	82	2006-02-15 04:45:25
3	Abu Dhabi	101	2006-02-15 04:45:25
4	Acuña	60	2006-02-15 04:45:25
5	Adana	97	2006-02-15 04:45:25
````