University: [ITMO University](https://itmo.ru/ru/)  
Faculty: [FICT](https://fict.itmo.ru)  
Course: [Введение в веб технологии](https://itmo-ict-faculty.github.io/introduction-in-web-tech/)  
Year: 2025/2026  
Group: U4125  
Author: Voroshnina Eva Pavlovna  
Lab: Lab1  
Date of create: 16.03.2026  
Date of finished: -

---

# Lab1 — Основы работы с Docker

## Цель работы

Изучить основы контейнеризации с использованием Docker, научиться работать с образами, контейнерами и томами (volumes).

---

# Ход работы

## 1. Установка Docker

Docker Desktop был установлен на компьютер.  
После установки была проверена корректность установки.

Команда:


docker --version


Результат: отображена версия Docker.

<img width="568" height="297" alt="Снимок экрана 2026-03-17 в 12 21 06 AM" src="https://github.com/user-attachments/assets/f52a5417-0d49-4934-bcaa-7450d40db600" />


---

## 2. Запуск тестового контейнера

Для проверки работы Docker был запущен тестовый контейнер:


docker run hello-world


Результат: Docker успешно скачал образ и вывел сообщение о корректной работе Docker.

---

## 3. Основные команды Docker

Были изучены базовые команды:


docker images
docker ps
docker ps -a


- `docker images` — список локальных образов  
- `docker ps` — список запущенных контейнеров  
- `docker ps -a` — список всех контейнеров  

---

## 4. Работа с образом Ubuntu

Был скачан образ Ubuntu:


docker pull ubuntu:latest


Контейнер был запущен в интерактивном режиме:


docker run -it ubuntu bash


Внутри контейнера был установлен пакет `curl`:


apt update
apt install -y curl


Проверка установки:


curl --version


После завершения работы был выполнен выход из контейнера:


exit


---

## 5. Запуск веб-сервера nginx

Был запущен контейнер с веб-сервером nginx:


docker run -d -p 8080:80 --name web-server nginx:alpine


После запуска контейнера была выполнена проверка:


docker ps


Также были просмотрены логи контейнера:


docker logs web-server


В контейнер было выполнено подключение:


docker exec -it web-server sh


---

## 6. Управление контейнерами

Были выполнены команды управления контейнерами:

Остановка контейнера:


docker stop web-server


Запуск контейнера:


docker start web-server


Удаление контейнера:


docker rm web-server


Удаление образа:


docker rmi nginx:alpine


---

## 7. Работа с volumes

Был создан Docker volume:


docker volume create my-volume


Контейнер был запущен с подключённым volume:


docker run -it --name volume-test -d -v my-volume:/data ubuntu bash


Внутри контейнера был создан файл:


echo "Hello from volume" > /data/test.txt


Файл был проверен:


cat /data/test.txt


После удаления контейнера был создан новый контейнер с тем же volume.

Файл сохранился, что подтверждает работу Docker volumes.

---

# Вывод

В ходе лабораторной работы были изучены основные возможности Docker.  
Были освоены операции работы с образами, контейнерами и томами, а также запуск веб-сервера внутри контейнера.
