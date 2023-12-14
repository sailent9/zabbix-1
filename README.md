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



