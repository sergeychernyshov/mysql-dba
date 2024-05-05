Посмотреть параметры для старта MySql
>mysql --print-defaults | sed 's/--/\n--/g'
>mysqld --print-defaults | sed 's/--/\n--/g' 

Просмотр раздела параметров или нескольких
>my_print_defaults mysqld
>my_print_defaults mysqld client
 
Поиск команды запуска MySql
>ps auxf | grep mysqld | grep -v grep
mysql     2646  2.5 10.5 2512452 410380 ?      Ssl  14:44   5:13 /usr/sbin/mysqld
>ps -p 2646 -ocommand ww | sed 's/--/\n--/g'
COMMAND
/usr/sbin/mysqld
