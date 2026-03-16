University: [ITMO University](https://itmo.ru/ru/)  
Faculty: [FICT](https://fict.itmo.ru)  
Course: [Введение в веб технологии](https://itmo-ict-faculty.github.io/introduction-in-web-tech/)  
Year: 2025/2026  
Group: U4125  
Author: Voroshnina Eva Pavlovna  
Lab: Lab2  
Date of create: 17.03.2026  
Date of finished:  

---

# Лабораторная работа №2  
## Настройка CI/CD пайплайна с GitHub Actions

## Цель работы

Целью лабораторной работы является изучение принципов CI/CD и настройка автоматической сборки и публикации Docker-образа с использованием GitHub Actions.

---

# Ход работы

## Подготовка проекта

Для выполнения лабораторной работы был использован проект из предыдущей лабораторной работы.

В проекте присутствуют следующие файлы:

- `app.py` — Flask приложение
- `requirements.txt` — файл зависимостей Python
- `Dockerfile` — файл для сборки Docker-образа

Также был создан аккаунт на **Docker Hub** для хранения Docker-образа.

---

## Настройка GitHub Actions

В корне репозитория была создана директория:.github/workflows
В данной директории был создан файл: docker-build.yml

В этом файле был описан CI/CD pipeline.

---

# Описание пайплайна

Пайплайн запускается автоматически при каждом **push в ветку main**.

Pipeline состоит из следующих шагов.

## 1. Checkout кода

Получение исходного кода из репозитория GitHub.

uses: actions/checkout@v4

## 2. Настройка Docker Buildx

Docker Buildx используется для сборки Docker-образов в CI среде.

uses: docker/setup-buildx-action@v3

## 3. Авторизация в Docker Hub

Для публикации Docker-образа требуется авторизация в Docker Hub.
Для этого используются секреты GitHub:

DOCKER_USERNAME

DOCKER_PASSWORD

В workflow используется следующий шаг:

uses: docker/login-action@v3

## 4. Сборка и публикация Docker-образа

Docker-образ собирается на основе Dockerfile и публикуется в Docker Hub.

uses: docker/build-push-action@v6

Образ публикуется с тегом:

voroshnina/my-flask-app:latest

## 5. Шаг деплоя

Для демонстрации деплоя добавлен тестовый шаг:

run: echo "Deploy step completed"

# Тестирование пайплайна

После настройки workflow был выполнен коммит и отправка изменений в репозиторий:

git commit
git push origin main

После этого GitHub Actions автоматически запустил CI/CD pipeline.

В разделе Actions было проверено выполнение всех шагов пайплайна.

Были успешно выполнены следующие этапы:

Checkout code

Setup Docker Buildx

Login Docker Hub

Build Docker image

Push Docker image

Deploy step

<img width="708" height="625" alt="Снимок экрана 2026-03-17 в 1 31 14 AM" src="https://github.com/user-attachments/assets/52f9ef80-19e3-4fc3-8997-0349a07fab06" />


# Результат

Docker-образ был успешно собран и опубликован в Docker Hub.

Образ доступен по адресу:

voroshnina/my-flask-app:latest

<img width="749" height="498" alt="Снимок экрана 2026-03-17 в 1 11 06 AM" src="https://github.com/user-attachments/assets/24b245e8-be7c-4970-a2bc-96cd62fd8c3f" />


Pipeline успешно выполняется при каждом push в ветку main.

# Вывод

В ходе лабораторной работы был настроен CI/CD пайплайн с использованием GitHub Actions.
Была реализована автоматическая сборка Docker-образа и его публикация в Docker Hub при каждом обновлении репозитория.

Получены практические навыки работы с GitHub Actions, Docker и настройкой CI/CD процессов.

