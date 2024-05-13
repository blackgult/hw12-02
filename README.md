# Домашнее задание к занятию «Работа с данными (DDL/DML)» - Михайлов Дмитрий

---

Задание можно выполнить как в любом IDE, так и в командной строке.

### Задание 1
1.1. Поднимите чистый инстанс MySQL версии 8.0+. Можно использовать локальный сервер или контейнер Docker.

1.2. Создайте учётную запись sys_temp. 

1.3. Выполните запрос на получение списка пользователей в базе данных. (скриншот)

1.4. Дайте все права для пользователя sys_temp. 

1.5. Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)

1.6. Переподключитесь к базе данных от имени sys_temp.

Для смены типа аутентификации с sha2 используйте запрос: 
```sql
ALTER USER 'sys_test'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```
1.6. По ссылке https://downloads.mysql.com/docs/sakila-db.zip скачайте дамп базы данных.

1.7. Восстановите дамп в базу данных.

1.8. При работе в IDE сформируйте ER-диаграмму получившейся базы данных. При работе в командной строке используйте команду для получения всех таблиц базы данных. (скриншот)

*Результатом работы должны быть скриншоты обозначенных заданий, а также простыня со всеми запросами.*

### Решение 1
1.3. Выполните запрос на получение списка пользователей в базе данных. (скриншот)
![1-1-3](https://github.com/blackgult/hw12-02/blob/main/1-1-3.PNG)

1.5. Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)
![1-1-5](https://github.com/blackgult/hw12-02/blob/main/1-1-5.PNG)

1.8. При работе в IDE сформируйте ER-диаграмму получившейся базы данных. При работе в командной строке используйте команду для получения всех таблиц базы данных. (скриншот)
![1-1-81](https://github.com/blackgult/hw12-02/blob/main/1-1-81.PNG)

![1-1-82](https://github.com/blackgult/hw12-02/blob/main/1-1-82.PNG)

*Результатом работы должны быть скриншоты обозначенных заданий, а также простыня со всеми запросами.*

## ПРОСТЫНЯ СО ВСЕМИ ЗАПРОСАМИ

sudo apt install mysql-server

mysql –version

sudo mysql

SHOW VARIABLES LIKE 'validate_password%';

select plugin_name, plugin_status from information_schema.plugins where plugin_name like 'validate%';

install plugin validate_password soname 'validate_password.so';

select plugin_name, plugin_status from information_schema.plugins where plugin_name like 'validate%';

SET GLOBAL validate_password_policy=LOW;

FLUSH PRIVILEGES;

sudo systemctl restart mysql.service

CREATE USER 'sys_temp'@'localhost' IDENTIFIED BY '!Dmitrym2024';

FLUSH PRIVILEGES;

GRANT ALL PRIVILEGES ON *.* TO 'sys_temp'@'localhost';

FLUSH PRIVILEGES;

SHOW GRANTS FOR 'sys_temp'@'localhost';

exit

mysql -u sys_temp –p

ALTER USER 'sys_temp'@'localhost' IDENTIFIED WITH mysql_native_password BY '!Dmitrym2024';

FLUSH PRIVILEGES;

SHOW DATABASES;

CREATE DATABASE sakila;

FLUSH PRIVILEGES;

SHOW DATABASES;

exit

mysql -u sys_temp -p sakila < /home/dmitrym/s-db/sakila-db/sakila-schema.sql

mysql -u sys_temp -p sakila < /home/dmitrym/s-db/sakila-db/sakila-data.sql

mysql -u sys_temp –p 

SHOW TABLES FROM sakila;

exit

### Задание 2
Составьте таблицу, используя любой текстовый редактор или Excel, в которой должно быть два столбца: в первом должны быть названия таблиц восстановленной базы, во втором названия первичных ключей этих таблиц. Пример: (скриншот/текст)
```
Название таблицы | Название первичного ключа
customer         | customer_id
```

### Решение 2

```
actor         | actor_id 
address       | address_id 
category      | category_id 
city          | city_id     
country       | country_id  
customer      | customer_id 
film          | film_id     
film_actor    | actor_id, film_id 
film_category | film_id, category_id 
film_text     | film_id     
inventory     | inventory_id
language      | language_id
payment       | payment_id  
rental        | rental_id    
staff         | staff_id     
store         | store_id  
```

![2-1](https://github.com/blackgult/hw12-02/blob/main/2-1.PNG)

## Дополнительные задания (со звёздочкой*)
Эти задания дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже шире разобраться в материале.

### Задание 3*
3.1. Уберите у пользователя sys_temp права на внесение, изменение и удаление данных из базы sakila.

3.2. Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)

*Результатом работы должны быть скриншоты обозначенных заданий, а также простыня со всеми запросами.*
