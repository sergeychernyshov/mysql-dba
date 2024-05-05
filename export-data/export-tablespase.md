Экспорт табличного пространства
````
show create table city

CREATE TABLE `city` (
`city_id` smallint unsigned NOT NULL AUTO_INCREMENT,
`city` varchar(50) NOT NULL,
`country_id` smallint unsigned NOT NULL,
`last_update` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
PRIMARY KEY (`city_id`),
KEY `idx_fk_country_id` (`country_id`),
CONSTRAINT `fk_city_country` FOREIGN KEY (`country_id`) REFERENCES `country` (`country_id`) ON DELETE RESTRICT ON UPDATE CASCADE
) ENGINE=InnoDB AUTO_INCREMENT=601 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci

flush table city for export
````

После выполнения команд появится файл
/var/lib/mysql/sakila/city.cfg
таблица будет заблокирована до конца сеанса.
После закрытия сеанса файл city.cgf исчезнет