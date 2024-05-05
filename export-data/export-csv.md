#Выгрузка данных в файл managers.csv
````
select
emp_no,
first_name,
last_name,
title,
from_date
from employees e
join titles t using(emp_no)
where title = 'Manager'
and to_date = '9999-01-01'
into outfile 'managers.csv'
fields terminated by ','
````

Данные в файле /var/lib/mysql/employees/managers.csv

````
select 
	emp_no, 
	first_name, 
	last_name, 
	title, 
	from_date
from employees e 
join titles t using(emp_no)
where title = 'Manager'
and to_date = '9999-01-01'
into outfile 'managers2.csv'
fields terminated by ',' ENCLOSED  by '"'
````
Данные в файле /var/lib/mysql/employees/managers2.csv