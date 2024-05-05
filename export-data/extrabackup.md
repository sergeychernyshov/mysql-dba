Установка XtraBackup 8.0 - не работает в mysql 8.0.36
Скачать RPM пакет
>wget https://www.percona.com/downloads/XtraBackup/Percona-XtraBackup-8.0.4/binary/redhat/7/x86_64/percona-xtrabackup-80-8.0.4-1.el7.x86_64.rpm --no-check-certificate

Установка
>yum localinstall percona-xtrabackup-80-8.0.4-1.el7.x86_64.rpm

Получить backup
>xtrabackup --host=127.0.0.1 --target-dir=/tmp/backup --backup>
>xtrabackup --host=127.0.0.1 --target-dir=/tmp/backup --backup --user=root --password=Serka_1312  --no-version-check 


