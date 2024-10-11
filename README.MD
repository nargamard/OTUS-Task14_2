# Задание: Разобраться с основами docker, с образом, эко системой docker в целом;

## Решение:

---
### Установлен Docker на хост машине:

```bash
[andrej@home-srv OTUS-Task14_2]$ docker --version
Docker version 27.1.1, build 59a4d52
[andrej@home-srv OTUS-Task14_2]$ docker-compose --version
docker-compose version 1.29.2, build unknown
```

```bash
[andrej@home-srv OTUS-Task14_2]$ docker run -it -p 8088:80 nginx_custom
```
Смотрим запущенные контейнеры:
```bash
CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS         PORTS                                   NAMES
c5e06b3a1d40   nginx_custom   "nginx -g 'daemon of…"   5 seconds ago   Up 5 seconds   0.0.0.0:8088->80/tcp, :::8088->80/tcp   laughing_kepler
```
Открываем в браузере `http://localhost:8088/`:
![Alt text](%D0%A1%D0%BA%D1%80%D0%B8%D0%BD_html.png)

---

## Отправляем образ в репозиторий
```bash
[andrej@home-srv OTUS-Task14_2]$ docker tag nginx_custom:latest nargamard/nargamard:nginx_custom
[andrej@home-srv OTUS-Task14_2]$ docker push nargamard/nargamard:nginx_custom 
The push refers to repository [docker.io/nargamard/nargamard]
0af5f8d77339: Pushed 
ad221c441b84: Pushed 
00663bcfa3bd: Pushed 
63ca1fbb43ae: Mounted from library/alpine 
nginx_custom: digest: sha256:59959afe52cb41dec76f6c5a6375984a3bfe081b7d6694c2c3f190c0bd662e6b size: 1155
```

Ссылка на репозиторий: 'https://hub.docker.com/layers/nargamard/nargamard/nginx_custom/images/sha256-59959afe52cb41dec76f6c5a6375984a3bfe081b7d6694c2c3f190c0bd662e6b?context=rep'

---

## Определите разницу между контейнером и образом. Вывод опишите в домашнем задании.

Образ - это набор файлов (программ, библиотек, файлов конфигураций), которые представляю собой среду для работы приложения и само приложение. То есть образ - это шаблон для создания контейнера.
Контейнер - это излированная среда, в которой запускается образ, или контейнер - это запущенный экземпляр образа. Данные хранятся контейнере до тех пор, пока он существует. С точки зрения операционной системы контейнер - это процесс.

---

## Ответьте на вопрос: Можно ли в контейнере собрать ядро?
Ничего не мешает собрать в контейнере ядро. Во всяком случае, не нашел информации, что нельзя. То есть, можно.

---

# Задание со звездочкой
Написать Docker-compose для приложения Redmine, с использованием опции build.
Добавить в базовый образ redmine любую кастомную тему оформления.
Убедиться что после сборки новая тема доступна в настройках.
Настроить вольюмы, для сохранения всей необходимой информации

## Решение

1. Docker-compose использует образ postgres10 и пробрасывает каталог ./storage/postgresql-data, чтобы данные хранились вне контейнера.
2. Docker-compose готовит измененный образ на базе стандартного образа с redmine (добавлена команда 'ADD  PurpleMine2-2.16.2.tar.gz /usr/src/redmine/public/themes', которая распаковывает архив с темой).

Результат: можно выбрать тему `PurpleMine2`
![Alt text](%D0%A1%D0%BA%D1%80%D0%B8%D0%BD_Redmine.png)