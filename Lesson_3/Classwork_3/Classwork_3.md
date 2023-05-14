`docker pull ubuntu` - получение image <br>
`docker images` - список images <br>
`docker rmi ubuntu` - удаление конкретного image <br>
`docker images -aq` - вывод id images <br>
`docker rmi $(docker images -aq) --force` - удаление всех images принудительно, даже запущенные <br>
`docker ps -a` - вывод всех контейнеров <br>
`docker run -it ubuntu bash` - it(запустить интерактивно) , bash(запуск команды внутри контейнера) <br>
`docker run -d --publish 8080:80 nginx` - -d(запуск в режиме демона) 8080(порт снаружи), 80(внутри) <br>
`curl 127.0.0.1:8080` <br>
`docker rm CONTAINER_NAME` - удаление контейнера <br>
`docker rm $(docker ps -a -q)` - удаление всех контейнеров, кроме запущенных <br>
`docker stop CONTAINER ID` - остановка контейнера по ID <br>
`docker system df` - просмотр занятого места на диске <br>
`docker system prune -af` - удаление всех images и контейнеров, кроме запущенных <br>
`docker start -i CONTAINER_NAME` - запуск и вход в конкретный контейнер <br>
`docker exec -it CONTAINER_NAME bash` - выполнить bash внутри контейнера -it(интерактивно) <br>
`docker run -it -h GeekBrains --name GB_cont ubuntu:22.10 bash` - -h(хост нэйм) --name(имя контейнера) <br>
`docker run --name test-mariadb -e MARIADB_ROOT_PASSWORD=test123 -d mariadb:10.10.2` <br>
`docker run --name my-phpmyadmin -d --link test-mariadb:db -p 8081:80 phpmyadmin` <br>

