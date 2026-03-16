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

<img width="480" height="30" alt="Снимок экрана 2026-03-17 в 1 12 56 AM" src="https://github.com/user-attachments/assets/592a8df2-efa3-4e90-a2e2-c0fb54572ad7" />


---

## 2. Запуск тестового контейнера

Для проверки работы Docker был запущен тестовый контейнер:


docker run hello-world


Результат: Docker успешно скачал образ и вывел сообщение о корректной работе Docker.

<img width="573" height="276" alt="Снимок экрана 2026-03-17 в 1 13 14 AM" src="https://github.com/user-attachments/assets/1ba1af55-4a2f-4e03-a078-f5f7807f2608" />


---

## 3. Основные команды Docker

Были изучены базовые команды:


docker images
docker ps
docker ps -a


- `docker images` — список локальных образов  
- `docker ps` — список запущенных контейнеров  
- `docker ps -a` — список всех контейнеров  

<img width="573" height="204" alt="Снимок экрана 2026-03-17 в 1 14 52 AM" src="https://github.com/user-attachments/assets/0f6f0aa4-3d5e-425d-8200-0219bf2b56b5" />


---

## 4. Работа с образом Ubuntu

Был скачан образ Ubuntu:


docker pull ubuntu:latest


Контейнер был запущен в интерактивном режиме:


docker run -it ubuntu bash

<img width="572" height="122" alt="Снимок экрана 2026-03-17 в 1 19 47 AM" src="https://github.com/user-attachments/assets/e0fc3ede-f20b-4603-a0ab-913642d05904" />


Внутри контейнера был установлен пакет `curl`:


apt update

<img width="569" height="240" alt="Снимок экрана 2026-03-17 в 1 26 26 AM" src="https://github.com/user-attachments/assets/1cb91732-a9b8-4330-935e-e37a132b3f2b" />

apt install -y curl

<img width="564" height="74" alt="Снимок экрана 2026-03-17 в 1 27 00 AM" src="https://github.com/user-attachments/assets/f89cc365-7ff9-44ad-bd02-58a37b1b68e0" />


Проверка установки:


curl --version


После завершения работы был выполнен выход из контейнера:


exit

<img width="574" height="185" alt="Снимок экрана 2026-03-17 в 1 27 45 AM" src="https://github.com/user-attachments/assets/8e7dc527-04f6-42b4-bc8b-7dff90fb7e8b" />


---

## 5. Запуск веб-сервера nginx

Был запущен контейнер с веб-сервером nginx:


docker run -d -p 8080:80 --name web-server nginx:alpine

<img width="571" height="156" alt="Снимок экрана 2026-03-17 в 1 21 04 AM" src="https://github.com/user-attachments/assets/e8789e4b-2bda-42e8-bae0-5356d2c419a2" />


После запуска контейнера была выполнена проверка:


docker ps

<img width="569" height="163" alt="Снимок экрана 2026-03-17 в 1 21 24 AM" src="https://github.com/user-attachments/assets/1a8d1a19-2e3b-4d15-8357-e6790e2458cb" />


Также были просмотрены логи контейнера:


docker logs web-server

<img width="570" height="111" alt="Снимок экрана 2026-03-17 в 1 21 59 AM" src="https://github.com/user-attachments/assets/1e330279-1423-4f09-883f-b123138cf6ef" />


В контейнер было выполнено подключение:


docker exec -it web-server sh

<img width="579" height="248" alt="Снимок экрана 2026-03-17 в 1 23 08 AM" src="https://github.com/user-attachments/assets/c74d9e51-341f-4584-9bb6-93e0a3ba3ee6" />

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

<img width="573" height="226" alt="Снимок экрана 2026-03-17 в 1 24 29 AM" src="https://github.com/user-attachments/assets/d739c099-5829-4387-b2df-b6cb41351350" />


---

## 7. Работа с volumes

Был создан Docker volume:


docker volume create my-volume


Контейнер был запущен с подключённым volume:


docker run -it --name volume-test -d -v my-volume:/data ubuntu bash


Внутри контейнера был создан файл:


echo "Hello from volume" > /data/test.txt

<img width="565" height="265" alt="Снимок экрана 2026-03-17 в 1 25 09 AM" src="https://github.com/user-attachments/assets/81f29e80-491f-4c65-9aba-bbf01a5183d5" />

Файл был проверен:


cat /data/test.txt

<img width="548" height="73" alt="Снимок экрана 2026-03-17 в 1 25 34 AM" src="https://github.com/user-attachments/assets/446d1b70-6022-4d94-a7be-7d90a29d48fd" />


После удаления контейнера был создан новый контейнер с тем же volume.

Файл сохранился, что подтверждает работу Docker volumes.

---

# Вывод

В ходе лабораторной работы были изучены основные возможности Docker.  
Были освоены операции работы с образами, контейнерами и томами, а также запуск веб-сервера внутри контейнера.
