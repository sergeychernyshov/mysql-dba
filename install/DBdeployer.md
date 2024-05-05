# DBdeployer 
Инструмент для развертывания БД MySQL в различных конфигурациях.
Позволяет создавать песочницы. Настраивать репликацию.
Разворачивать кластеры (например, кластер Galera).

1) Скачать последнюю версию DBdeployer

```
wget https://github.com/datacharmer/dbdeployer/releases/download/v1.73.0/dbdeployer-1.73.0.linux.tar.gz
```

2) Разархивируем архив

````
 tar -xvf dbdeployer-1.73.0.linux.tar.gz
````

3) Перемещаем бинарные файлы

````
mv dbdeployer-1.73.0.linux /usr/local/bin/dbdeployer
````

4) Выдаем права на запуск

````
chmod 775 dbdeployer
````

5) Проверяем версию

````
dbdeployer --version

dbdeployer version 1.73.0
````

