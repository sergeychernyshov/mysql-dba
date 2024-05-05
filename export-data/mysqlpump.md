Утилита mysqlpump улучшенная версия mysqldump.

Получить полный дамп всех баз MySql
>mysqlpump > pump.sql

Параллельное выполнение дампа
>mysqlpump --compress-output=zlib --include-users=bob,root --include-databases=sakila,nasa --parallel-schemas=2:sakila --parallel-schemas=nasa > pump2.sql


mysqlpump не позволяет делать реконструкцию параллельно!