Объем баз данных MySQL
````
select
table_schema,
round(sum(t.data_length + t.index_length)/ 1073741842 , 2) as size_gb
FROM information_schema.tables t
group by table_schema
````

Объем таблиц MySQL
````
select
table_schema,
table_name,
round((t.data_length + t.index_length)/ 1073741842 , 2) as size_gb
FROM information_schema.tables t
where t.table_type = 'BASE TABLE'
and table_schema !='performance_schema'
````