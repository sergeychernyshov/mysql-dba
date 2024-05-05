Поиск не используемых индексов возможен запросом
````
SELECT * FROM sys.schema_unused_indexes
where object_schema not in ('performance_schema')
````
