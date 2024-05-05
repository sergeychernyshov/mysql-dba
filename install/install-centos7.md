# Установка MySQL 8

Установка MySQL 8.0 на сервере OC Centos 7 выполняется под пользователем ROOT.

Добавляем репозиторий

>rpm -Uvh https://repo.mysql.com/mysql80-community-release-el7.rpm

Устанавливаем MySQL 8.0

>yum --enablerepo=mysql80-community install mysql-community-server

Заупуск MySQL

>systemctl start mysqld

Поиск временного пароля для коннекта MySql

>grep "A temporary password" /var/log/mysqld.log

``` 2024-02-23T18:48:36.926479Z 6 [Note] [MY-010454] [Server] 
A temporary password i                        s generated for 
root@localhost: hIdfxON*-9x3 
```

В файле /etc/my.cnf находим ```socket```.
Выдаем права на файл и каталог /var/lib/mysql/mysql.sock /var/lib/mysql

>chmod 755 /var/lib/mysql


Скрипт для безопасного использования БД MySQL

>mysql_secure_installation

Пароль для входа ```hIdfxON*-9x3```

Скрипт задает следующие вопросы:
 - смена пароля root@localhost --создал пароль Serka_1312
 - сменить пароль для root?
 - удалить анонимны пользователей?
 - запретить заходить под root удаленно?
 - удалить тестовую базу?
 - обновить привилегии для таблиц?
 
Пробуем подключиться к БД

> mysql -u root -p

Пароль Serka_1312

Проверяем версию MySQL

```
mysql> select @@version;
+-----------+
| @@version |
+-----------+
| 8.0.36    |
+-----------+
1 row in set (0.00 sec)
```

Сделаем настройку для запуска БД MySQL после запуска OC.

>systemctl enable mysqld

Для входа под учетной записью root без пароля в файл ````my.cnf```` нужно добавить 

````
[client]
user=root
password=Serka_1312
````