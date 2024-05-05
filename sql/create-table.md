

create table if not exists actor(
actor_id 	smallint unsigned not null auto_increment,
first_name 	varchar(45) not null,
last_name 	varchar(45) not null,
last_update timestamp not null default current_timestamp on UPDATE current_timestamp,
primary key (actor_id),
key idx_actor_last_name (last_name)
);

show create table actor 

````
CREATE TABLE `actor` (
  `actor_id` smallint unsigned NOT NULL AUTO_INCREMENT,
  `first_name` varchar(45) COLLATE utf8mb4_ru_0900_as_cs NOT NULL,
  `last_name` varchar(45) COLLATE utf8mb4_ru_0900_as_cs NOT NULL,
  `last_update` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
  PRIMARY KEY (`actor_id`),
  KEY `idx_actor_last_name` (`last_name`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_ru_0900_as_cs
````

DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP - авто добавление даты при вставке и обновлении
DEFAULT CURRENT_TIMESTAMP  - авто добавление даты при вставке
DEFAULT ON UPDATE CURRENT_TIMESTAMP - авто обновление даты при обновлении

AUTO_INCREMENT - счетчик ID в таблице. Должен быть один в таблице.
Обязательно поле  NOT NULL. 