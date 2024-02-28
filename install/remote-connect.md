# Подключение к MySQL с удаленного хоста

Открываем порт 3306 на сервере MySQL
````
firewall-cmd --zone=public --add-port=3306/tcp
````

В файле /etc/my.cnf указываем 
````
bind-address=0.0.0.0
````

Перезапускаем MySQL
````
systemctl restart mysqld
````

Создаем пользователя для соединения, выдаем права.
Выполнить FLUSH PRIVILEGES чтобы сервер перезагрузил все таблицы предоставления привилегий.
````
mysql> CREATE USER 'root'@'192.168.31.92' IDENTIFIED BY 'Serka_1312';
mysql> GRANT ALL PRIVILEGES ON *.* TO 'root'@'192.168.31.92' WITH GRANT OPTION;
mysql> FLUSH PRIVILEGES;
````

Установить свойство драйвера allowPublicKeyRetrieval=true если потребуется.