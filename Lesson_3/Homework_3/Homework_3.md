# ФИ: Василакий Вячеслав. Группа: Программирование 6 | 3325 / 3424 | 21.09.2022. Урок №2

### Урок 3. Введение в Docker

__Задание:__
1) запустить контейнер с БД, отличной от mariaDB, используя инструкции на сайте: https://hub.docker.com/ <br>
2) добавить в контейнер hostname такой же, как hostname системы через переменную <br>
3) заполнить БД данными через консоль <br>
4) запустить phpmyadmin (в контейнере) и через веб проверить, что все введенные данные доступны <br>

### Solution:

1) Пулю latest релиз `docker pull mysql` <br>
2) Создаю контейнер и задаю имя хоста такое же как в системе <br> 
`docker run --name homework3 -e MYSQL_ROOT_PASSWORD=123 -h $HOSTNAME -d mysql` <br>
![HOSTNAME.jpeg](img%2FHOSTNAME.jpeg)
<br>

   Захожу в контейнер `docker exec -it homework3 bash` <br>
   Проваливаюсь в DB `mysql -u root -p` <br>
3) Создаю DB `CREATE DATABASE homework3;`, `use homework3;` <br>
Заполнение DB:

<br>

```MySQL
CREATE TABLE classmates (id INTEGER PRIMARY KEY AUTO_INCREMENT,name TEXT NOT NULL,age TINYINT NOT NULL,address TEXT NOT NULL);
   
INSERT INTO classmates (name, age, address)VALUES('Stepan Sergeev',42,'Volzhskii,ul. Himikov, 1'),('Anna Andrianovna',38,'Surgut,ul. Mira, 9');
```

Проверяем данные `SELECT name, age FROM classmates;` <br>

![DB_data.jpeg](img%2FDB_data.jpeg) 

<br>

4) Запускаем контейнер `docker run --name my-phpmyadmin -d --link homework3:db -p 8081:80 phpmyadmin`
указываем линк на DB и порт по которому будет доступна DB <br>

![PHP_myadmin.jpeg](img%2FPHP_myadmin.jpeg)