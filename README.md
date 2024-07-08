## Установка с использованием docker compose

1. Скопировать **.env.dist** в **.env** и актуализировать все параметры

2. Развернуть контейнера выполнив скрипт:
```sh
docker compose -p boxes down --remove-orphans && \
docker build --target=common-tools \
	-t localhost/boxes-common-tools:latest -f ./docker/Dockerfile . && \
docker build --target=fpm \
	--build-arg USER=1000 \
	--build-arg GROUP=1000 \
	-t localhost/boxes-fpm:latest -f ./docker/Dockerfile . && \
docker build --target=nginx \
	-t localhost/boxes-nginx:latest -f ./docker/Dockerfile . && \
docker compose -p boxes up -d && \
docker compose -p boxes run --rm php-fpm composer install --no-cache
```


- установка php-зависимостей из регистра зависимостей composer.json
```sh
docker compose -p boxes run --rm php-fpm composer install --no-cache
```