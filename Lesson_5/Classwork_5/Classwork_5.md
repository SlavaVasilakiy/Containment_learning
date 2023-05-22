`docker-compose build` - сборка по конфиг файлу yaml <br>
`docker-compose up` - запуск проекта <br>
`docker-compose start` - запуск сервисов (уже созданных) <br>
`docker-compose down` - остановка и удаление всех сервисов проекта <br>
`docker-compose stop` - остановка сервисов без удаления <br>
`docker-compose logs -f "service-name"` - просмотр логов сервиса <br>
`docker-compose exec` - выполнение команды <br>
`docker-compose images` - список образов <br>

`docker swarm init` - инициализация <br>
`docker swarm leave` - вывод ноды из кластера <br>
`docker node ls` - список нод в кластере <br>
`docker node rm "id"` - удаленик ноды <br>
`docker node promote "name"` - назначить менеджмент ноде <br>
`docker node demote "name"` - убрать менеджмент <br>
