# Примеры команды INSERT

Команда ```insert ignore into``` игнорирует ошибки, которые возникают при вставке 
````
insert ignore into `language` (language_id,name) values(6 , 'German')
````

Команда insert с возможностью именования
````
insert into country
set
    country_id = null,
    country='Bahams',
    last_update=now()
```