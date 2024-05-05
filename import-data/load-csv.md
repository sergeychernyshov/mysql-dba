#Загрузка данных из CSV

1) Создаем таблицу для хранения данных
````
create table facilities(
	center 					TEXT,
	center_search_status 	TEXT,
	facility 				TEXT,
	facility_url 			TEXT,
	occupied				TEXT,
	status 					TEXT,
	url_link 				TEXT,
	record_date 			DATETIME,
	last_update 			TIMESTAMP null,
	country 				TEXT,
	contact 				TEXT,
	phone 					TEXT,
	location 				TEXT,
	city 					TEXT,
	state 					TEXT,
	zipcode 				TEXT
)
 
````

2) Проверяем параметр secure_file_priv.
>show variables like 'secure%'

value = /var/lib/mysql-files/
В этой директории должен находится файл для загрузки.

Добавить в файл my.cnf в раздел [mysqld]
````
secure_file_priv=""
````
Перезагружаем сервер базы MySQL

3) Выполняем команду
````
load data infile 'NASA_Facilities.csv'
into table facilities fields TERMINATED BY ','
OPTIONALLY ENCLOSED BY '"'
IGNORE 1 LINES
(center,
center_search_status,
facility,
facility_url,
occupied,
status,
url_link,
@var_record_date,
@var_last_update,
country,
contact,
phone,
location,
city,
state,
zipcode)
set record_date = if(
CHAR_LENGTH(@var_record_date)=0, NULL,
str_to_date(@var_record_date, '%m/%d/%Y %h:%i:%s %p')),
last_update = if(
CHAR_LENGTH(@var_last_update)=0, NULL,
str_to_date(@var_last_update, '%m/%d/%Y %h:%i:%s %p'))
 ````

4) Проверяем загруженные данные.