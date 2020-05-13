Docker and docker-compose class
===============================

Note about working user variables: you should export two variables at host machine — `DUID` (docker user id), variable with your current user ID and `DGID` (docker group id), variable with your current group.

These variables are uses for launch php-process in a container.

For example:    
```shell script
export DUID=$(id -u) && export DGID=$(id -g)
```

## Run project locally

1. Build project: 
    ```shell script
    docker-compose build
    ```
1. Launch project:
    ```shell script
    docker-compose up -d
    ```
1. Install packages:
    ```shell script
    docker-compose exec app composer install
    ```
1. Run tests:
    ```shell script
    docker-compose exec app vendor/bin/phpunit
    ```
	
История 13-05-2020
1. Стянуть реп - я скачала зип папку 
т.к. пытаясь клонировать он запросил логин/пароль/ключ привязки
я не совсем понимаю как мне стянуть реп вживую
*Думаю это моя первая проблема*

Поэтому я просто скачиваю архив
и вручную восстанавливаю репо у себя
(а именно залила мастер с комментом - 1 -,
залила ветку conflict с комментом - 2 - причем эта ветка идет от master
а потом поменяла на файлы ветки)

2. После того как мой текущий репозиторий залит с 2мя ветками.
Создаю от мастера ветку dev.

3. Тут я решила сначала собрать докер,
чтобы посмотреть как все работает до того как я что то добавлю
делаю
docker-compose build (собираем)
docker-compose up -d (-d - это чтоб был фоновый режим)
docker-compose exec app composer install (устанавливаем)
docker-compose exec app vendor/bin/phpunit (собираем все вместе уже)
docker-machine ip default (вспоминаю что за localhost у меня)

На странице ошибка, точнее предупреждение о файле
"Warning: require(/var/www/app/vendor/autoload.php): failed to open stream"
*Думаю это моя вторая проблема*
Спустя пару мин поиска и думаний делаю
docker-compose exec app composer install (еще раз)

Все получилось! урашки!

4. Нужно добавить "ФИО студента"
сначала просто для теста добавлю строки
APP_FIOS: 'sibgatulinara' в docker-compose.yml
$_SERVER['APP_FIOS'] = ($_ENV['APP_FIOS'] ?? $_SERVER['APP_FIOS'] ?? null) ?? 'fio'; в index.php
В консоли после изменений делаю
docker-compose stop app (остановить)
docker-compose build (очень важно пересобрать)
docker-compose up -d (pfgecnbnm в фоновом режиме)
Появилась.
Делаю коммит в ветку с комментом "add fios"

5. Теперь надо "выполнить merge ветки conflicted в ветку dev"
*вижу что это моя третья проблема*
конфликта нету - а значит я не правильно выполнила предыдущие задание

6. Очевидно, что переменная QUOTE в контроллере должна стать ФИО студом
ок создам конфликт

7. Из истории гита легко понять, что моя попытка была косячная
*моя третья проблема стала очень жирной - тепеь я совсем запуталась*
*пропускаю тогда этот момент*

8. Собираю и загружаю образ.
docker commit s_web_1 rasibgatulina/srez_1_web:v1
docker push rasibgatulina/srez_1_web:v1
docker commit s_app_1 rasibgatulina/srez_1_app:v1
docker push rasibgatulina/srez_1_app:v1

Проверяю https://hub.docker.com/repositories - они там есть

9. Сливаю dev в master через интерфейс 
Делаю compare & pull request
(если бы это был реалити проект
еще обновила бы ветку - но тут ничего не будет)