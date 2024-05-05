#Параметры MySQL
Просмотр значений параметров
на уровне сервера
>show global variables like '%connectio%'

на уровне сессии
>show session variables like '%connectio%'
>show variables like '%connectio%'

<table>
    <thead>
        <tr>
            <th>Параметр</th>
            <th>Значение</th>
            <th>Описание</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan="3" align="center">lower_case_table_names</td>
            <td>0</td>
            <td>Имена таблиц сохраняются как указано. 
                <br>При сравнении учитывается регистр.
                <br>В Linux принудительное значение.
            </td>
        </tr>
        <tr>
            <td>1</td>
            <td>Имена таблиц сохраняются в нижнем регистре. 
                <br>При сравнении не учитывается регистр.
                <br>В Windows по умолчанию.
            </td>
        </tr>
        <tr>
            <td>2</td>
            <td>Имена таблиц сохраняются как указано.
                <br>При сравнении используется нижний регистр.
                <br>В MacOS по умолчанию.
            </td>
        </tr>
         <tr>
            <td align="center">innodb_lock_wait_timeout</td>
            <td>50, секунд</td>
            <td>Время для ожидания COMMIT при уровне изоляции SERIALIZABLE
            </td>
        </tr>
        <tr>
            <td align="center">lock_wait_timeout</td>
            <td>31536000, секунд</td>
            <td>Время для ожидания замка для сессии
            </td>
        </tr>
        <tr>
            <td align="center">innodb_deadlock_detect</td>
            <td>ON</td>
            <td>Автоматическое разрешения deadlock
            </td>
        </tr>
        <tr>
            <td align="center">innodb_print_all_deadlocks</td>
            <td>ON</td>
            <td>сохранять записи о всех deadlock в журнале
            </td>
        </tr>
        <tr>
            <td align="center">innodb_print_ddl_logs</td>
            <td>ON</td>
            <td>сохранять записи о ddl deadlock в журнале
            </td>
        </tr>
        <tr>
            <td align="center">transaction_isolation</td>
            <td>READ COMMITTED</td>
            <td>уровень изоляции
            </td>
        </tr>
        <tr>
            <td align="center">secure_file_priv</td>
            <td>/var/lib/mysql-files/</td>
            <td>Путь для файлов, которые можно загружать в БД.
                Файл должен быть доступен для чтения.
                Если параметр пустой, то загружать можно из любой директории.
            </td>
        </tr>
        <tr>
            <td align="center">foreign_key_checks</td>
            <td>1</td>
            <td>Проверка вторичных ключей
            </td>
        </tr>
        <tr>
            <td align="center">default_authentication_plugin</td>
            <td>caching_sha2_password</td>
            <td>Плагин для аутентификации пользователей по умолчанию
            </td>
        </tr>
        <tr>
            <td align="center">mandatory_roles</td>
            <td></td>
            <td>Список ролей доступный пользователям
            </td>
        </tr>
        <tr>
            <td align="center">activate_all_roles_on_login</td>
            <td>OFF</td>
            <td>Активация всех ролей при входе (set role all).
                Активируются все роли доступные пользователям как явно так и через параметр mandatory_roles.
            </td>
        </tr>
        <tr>
            <td align="center">slow_query_log</td>
            <td>OFF</td>
            <td>Журнал медленных запросов</td>
        </tr>
        <tr>
            <td align="center">slow_query_log_file</td>
            <td>/var/lib/mysql/MiWiFi-R3-srv-slow.log</td>
            <td>Расположение файла журнала медленных запросов</td>
        </tr>
        <tr>
            <td align="center">long_query_time</td>
            <td>10.0000</td>
            <td>Время ограничения длительности запросов, при превышении которого запрос попадает в журнал медленных запросов</td>
        </tr>
        <tr>
            <td align="center">log_queries_not_using_indexes</td>
            <td>OFF</td>
            <td>Параметр отвечает за запись запросов без индексов в журнал медленных запросов</td>
        </tr>
        <tr>
            <td align="center">log_slow_admin_statements</td>
            <td>OFF</td>
            <td>Параметр отвечает за запись DDL запросов в журнал медленных запросов</td>
        </tr>
    </tbody>
</table>


