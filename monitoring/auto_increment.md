Проверка полей auto_increment
````
select 
	table_schema,
	table_name,
	column_name,
	data_type,
	column_type,
	if(LOCATE('unsigned',COLUMN_TYPE)>0,1,0) as is_unsigned,
	(case data_type
		when 'tinyint' then 255
		when 'smallint' then 65535
		when 'mediumint' then 16777215
		when 'int' then 4294967295
		when 'bigint' then 18446744073709551615 
	end >> if(LOCATE('unsigned',COLUMN_TYPE)>0,1,0)	
	) as max_value,
	AUTO_INCREMENT,
	AUTO_INCREMENT / (case data_type
		when 'tinyint' then 255
		when 'smallint' then 65535
		when 'mediumint' then 16777215
		when 'int' then 4294967295
		when 'bigint' then 18446744073709551615 
	end >> if(LOCATE('unsigned',COLUMN_TYPE)>0,1,0)	
	) as AUTO_INCREMENT_RATIO
from information_schema.columns
inner join information_schema.tables using(table_schema, table_name)
where table_schema not in ('mysql','information_schema','performance_schema')
and extra = 'auto_increment'
````