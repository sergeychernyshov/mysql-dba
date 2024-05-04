# Получение и загрузка данных для тестов

### База SAKILA

Скачиваем архив
````
wget https://downloads.mysql.com/docs/sakila-db.tar.gz
````

Распаковка архива
````
tar -xvf sakila-db.tar.gz
````

Заходим в MySQL
````
mysql -u root
````

Создаем базу
````
mysql>CREATE DATABASE sakila;
````

Посмотреть базы можно командой
````
mysql> show databases;
````
Выходим
````
mysql>quit;
````

Создаем объекты
````
mysql -u root -p sakila < sakila-schema.sql
````

Вставляем данные
````
mysql -u root -p sakila < sakila-data.sql
````

### База WORLD
Скачиваем архив
````
wget https://downloads.mysql.com/docs/world-db.tar.gz
````
Распаковка архива
````
tar -xvf world-db.tar.gz
````
Заходим в MySQL
````
mysql -u root
````
Создаем базу
````
mysql>CREATE DATABASE world;
````
Выходим
````
mysql>quit;
````
Создаем объекты и данные
````
mysql -u root -p world < world.sql
````

### База EMPLOYEES
Скачиваем репозиторий
````
git clone https://github.com/datacharmer/test_db.git
````
Загружаем структуры и данные
````
cat employees.sql | mysql -u root -p
````

### База banks
Скачать модель для MyDQS Workbench
````
git clone https://github.com/vgrippa/learning_mysql.git
````
