# Практическое задание с самопроверкой `«Система мониторинга Zabbix»` `Салмин Евгений`




### Задание 1

`Установите Zabbix Server с веб-интерфейсом.`

Процесс выполнения

Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
Установите PostgreSQL. Для установки достаточна та версия, что есть в системном репозитороии Debian 11.
Пользуясь конфигуратором команд с официального сайта, составьте набор команд для установки последней версии Zabbix с поддержкой PostgreSQL и Apache.
Выполните все необходимые команды для установки Zabbix Server и Zabbix Web Server.
Требования к результатам

Прикрепите в файл README.md скриншот авторизации в админке.
Приложите в файл README.md текст использованных команд в GitHub.

### Решение 1

```
sudo apt install -y postgresql postgresql-contrib
```
```
wget https://repo.zabbix.com/zabbix/7.4/release/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest_7.4+ubuntu24.04_all.deb
dpkg -i zabbix-release_latest_7.4+ubuntu24.04_all.deb
apt update
```
```
apt install zabbix-server-pgsql zabbix-frontend-php php8.3-pgsql zabbix-apache-conf zabbix-sql-scripts
```
```
sudo -u postgres createuser --pwprompt zabbix
sudo -u postgres createdb -O zabbix zabbix
```
```
zcat /usr/share/zabbix/sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix
```
```
sudo sed -i 's/# DBPassword=/DBPassword=zabbix_pass/' /etc/zabbix/zabbix_server.conf
```
```
sudo systemctl restart zabbix-server zabbix-agent apache2
sudo systemctl enable zabbix-server zabbix-agent apache2
```

<img width="1920" height="952" alt="image" src="https://github.com/user-attachments/assets/64fcad71-8fc5-42b3-a17b-ea42d3931d92" />

---

### Задание 2


### Решение 2

# 1. Добавление репозитория (аналогично серверу)
wget https://repo.zabbix.com/zabbix/7.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest_7.0+ubuntu24.04_all.deb
sudo dpkg -i zabbix-release_latest_7.0+ubuntu24.04_all.deb
sudo apt update

# 2. Установка только агента 
sudo apt install -y zabbix-agent

# 3. Настройка подключения к серверу
sudo nano /etc/zabbix/zabbix_agent.conf

# 4. Запуск
sudo systemctl restart zabbix-agent2
sudo systemctl enable zabbix-agent2

### Задание 3



### Задание 4

