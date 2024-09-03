# BitrixDockerWin
WEB-сервер для Bitrix на Docker. 
BDW - это готовый набор Dockerfile для быстрого развертывания dev сервера.
BDW работает в 2-х вариантах:
- Classic - классический вариант (apache, nginx, php, mariadb, redis).
  Настроен сервер согласно [официальной инструкции](https://dev.1c-bitrix.ru/learning/course/index.php?COURSE_ID=32&CHAPTER_ID=05360&LESSON_PATH=3903.4862.20866.5360).
- PHP-FPM - вариант без apache (nginx, php, mariadb, redis).
  Настройка через связь nginx с php через PHP-FPM.

Для новичков:
**Коротко о CGI, FastCGI, PHP-FPM и mod_php - [читать тут](https://tokmakov.msk.ru/blog/item/92).**

**Все необходимые настройки (конфиги) пакетов вынесены в ``volumes``,
что позволяет изменять настройки в любое время не пересоздавая образы Docker.**

Так же для удобства отладки в ``volumes`` вынесены log файлы.

## Образы
### Classic версия
- PHP+Apache ``(php:8.3-apache-bookworm)``
- nginx ``(nginx:stable)``
- SQL ``(mariadb:latest)``
- Redis ``(redis:bookworm)`` \
  Дополнительно:
- phpMyAdmin ``(phpmyadmin:latest)``

### PHP-FPM версия (в разработке)
- PHP ``(php:8.3-fpm-bookworm)``
- nginx ``(nginx:stable)``
- SQL ``(mariadb:latest)``
- Redis ``(redis:bookworm)`` \
  Дополнительно:
- phpMyAdmin ``(phpmyadmin:latest)``

### Требования к системе
- ОС: `Windows`
- Docker Desktop `>= 4.33.1`
- Docker Compose `>= v2.28.1-desktop.1`

## Настройка



## Запуск
### Classic версия

Запуск сборки образов (build):
```shell
docker-compose -f src/classic/docker-compose.build.yaml build
```

Запуск контейнеров (up):
```shell
docker-compose -p "bitrix_classic" -f src/classic/docker-compose.run.yaml up
```

Остановка контейнеров (down):
```shell
docker-compose -p "bitrix_classic" -f src/classic/docker-compose.run.yaml down
```

### PHP-FPM версия

Запуск сборки образов (build):
```shell
docker-compose -f src/fpm/docker-compose.build.yaml build
```

Запуск контейнеров (up):
```shell
docker-compose -p "bitrix_fpm" -f src/fpm/docker-compose.run.yaml up
```

Остановка контейнеров (down):
```shell
docker-compose -p "bitrix_fpm" -f src/fpm/docker-compose.run.yaml down
```