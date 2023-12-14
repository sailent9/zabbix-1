Задание 1
Установите Zabbix Server с веб-интерфейсом.

Процесс выполнения
Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
Установите PostgreSQL. Для установки достаточна та версия, что есть в системном репозитороии Debian 11.
Пользуясь конфигуратором команд с официального сайта, составьте набор команд для установки последней версии Zabbix с поддержкой PostgreSQL и Apache.
Выполните все необходимые команды для установки Zabbix Server и Zabbix Web Server.
Требования к результаты
Прикрепите в файл README.md скриншот авторизации в админке.
Приложите в файл README.md текст использованных команд в GitHub.
Решение 1

Установите и сконфигурируйте Zabbix для выбранной платформы

a. Установите репозиторий Zabbix

Документация
``` # wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_6.0-4+debian11_all.deb ```
``` # dpkg -i zabbix-release_6.0-4+debian11_all.deb # apt update ```

b. Установите Zabbix сервер, веб-интерфейс и агент
``` # apt install zabbix-server-pgsql zabbix-frontend-php php7.4-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-agentc  ```

 Создайте базу данных

Документация
Установите и запустите сервер базы данных.

Выполните следующие комманды на хосте, где будет распологаться база данных.

``` # sudo -u postgres createuser --pwprompt zabbix ```
``` # sudo -u postgres createdb -O zabbix zabbix ```

На хосте Zabbix сервера импортируйте начальную схему и данные. Вам будет предложено ввести недавно созданный пароль.

``` # zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix ```

d. Настройте базу данных для Zabbix сервера
Отредактируйте файл /etc/zabbix/zabbix_server.conf

DBPassword=password
e. Запустите процессы Zabbix сервера и агента
Запустите процессы Zabbix сервера и агента и настройте их запуск при загрузке ОС.

``` # systemctl restart zabbix-server zabbix-agent apache2 ```
``` # systemctl enable zabbix-server zabbix-agent apache2 ```


скриншоты задания 1
![установил забикс023-12-14 181208](https://github.com/sailent9/zabbix-1/assets/130309754/ce092843-a5e0-4392-80fb-9852b4fa3c6a)
![веб-интерфейс2023-12-14 182058](https://github.com/sailent9/zabbix-1/assets/130309754/60c9182b-87f7-4ac6-8add-bd85ff07bc6e)



Задание 2
Установите Zabbix Agent на два хоста.

Процесс выполнения
Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
Установите Zabbix Agent на 2 вирт.машины, одной из них может быть ваш Zabbix Server.
Добавьте Zabbix Server в список разрешенных серверов ваших Zabbix Agentов.
Добавьте Zabbix Agentов в раздел Configuration > Hosts вашего Zabbix Servera.
Проверьте, что в разделе Latest Data начали появляться данные с добавленных агентов.
Требования к результаты
Приложите в файл README.md скриншот раздела Configuration > Hosts, где видно, что агенты подключены к серверу
Приложите в файл README.md скриншот раздела Configuration > Hosts, где видно, что агенты подключены к серверу
Приложите в файл README.md скриншот раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные.
Приложите в файл README.md текст использованных команд в GitHub

Решение 2
все работает скриншот раздела Configuration > Hosts, где видно, что агенты подключены к серверу
![image](https://github.com/sailent9/zabbix-1/assets/130309754/27f51777-c61a-4134-ae79-adb664d82b66)
здесь видно что пытается забрать логи у сервака 158.160.11.105 скриншот раздела Configuration > Hosts, где видно, что агенты подключены к серверу
![image](https://github.com/sailent9/zabbix-1/assets/130309754/68a76c59-3186-4563-810e-458315faf955)
скриншот раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные
![image](https://github.com/sailent9/zabbix-1/assets/130309754/043f67fe-08a3-48ef-b5a6-d6366a4291e9)



