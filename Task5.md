# Урок 5. Docker Compose и Docker Swarm

Устанавливаем docker-compose - `sudo apt install docker-compose`

![Alt text](/images/image18.png)

Запускаем контейнер с базой данных - `docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=1234 -d --network host mysql:8.0.31`

![Alt text](/images/image19.png)

Запускаем контейнер с PHP, просоединяем к БД открываем порт 8081 - `docker run --name myphp -d --link some-mysql:db -p 8081:80 phpmyadmin/phpmyadmin`

![Alt text](/images/image20.png)

Проверяем работу в браузере по адресу `localhost:8081`

![Alt text](/images/image21.png)

Создаем файл `nano docker-compose.yml` (Соблюдать отсупы и синтаксис!)

`version: '3.1'`\
`services:`\
`db:`\
  `image: mariadb:10.10.2`\
  `restart: always`\
  `environment:`\
   `MESQL_ROOT_PASSWORD:12345`\
 `adminer`:\
  `image: adminer:4.8.1`\
  `ports:`\
   `- 6080:8080`

   ![Alt text](/images/image22.png)

Создаем контейнер - `sudo docker-compose up -d`

![Alt text](/images/image23.png)

Проверяем работу в боаузере по адресу `localhost:6080`

![Alt text](/images/image24.png)





