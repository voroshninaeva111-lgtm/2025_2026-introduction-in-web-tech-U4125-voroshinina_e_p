University: [ITMO University](https://itmo.ru/ru/)  
Faculty: [FICT](https://fict.itmo.ru)  
Course: [Введение в веб технологии](https://itmo-ict-faculty.github.io/introduction-in-web-tech/)  
Year: 2025/2026  
Group: U4125  
Author: Popov Mark Alexandrovich  
Lab: Lab2  
Date of create: 17.03.2026  
Date of finished: 17.03.2026  

---

# Лабораторная работа №2  
## Настройка CI/CD пайплайна с GitHub Actions

## Цель работы

Целью лабораторной работы является изучение принципов CI/CD и настройка автоматического пайплайна для сборки и публикации Docker-образа с использованием GitHub Actions.

---

# Ход работы

## Подготовка проекта

Для выполнения лабораторной работы был использован проект из предыдущей лабораторной работы.  
В проекте присутствуют следующие файлы:

- `app.py` — приложение на Flask
- `requirements.txt` — файл зависимостей Python
- `Dockerfile` — файл для сборки Docker-образа

Также был создан аккаунт на **Docker Hub** для хранения Docker-образа.

---

## Настройка GitHub Actions

В корне репозитория была создана директория:


.github/workflows


В данной директории был создан файл:


docker-build.yml


В этом файле был описан CI/CD пайплайн.

---

# Описание пайплайна

Пайплайн запускается автоматически при каждом **push в ветку main**.

Workflow состоит из следующих шагов.

### 1. Получение исходного кода

Используется action для получения кода из репозитория:

```yaml
uses: actions/checkout@v4
2. Настройка Docker Buildx

Для сборки Docker-образа используется Docker Buildx:

uses: docker/setup-buildx-action@v3
3. Авторизация в Docker Hub

Для доступа к Docker Hub используются секреты GitHub:

DOCKER_USERNAME

DOCKER_PASSWORD

uses: docker/login-action@v3
4. Сборка и публикация Docker-образа

Docker образ собирается из Dockerfile и публикуется в Docker Hub.

uses: docker/build-push-action@v6

Образ публикуется с тегом:

voroshnina/my-flask-app:latest
5. Шаг деплоя

Для демонстрации деплоя добавлен тестовый шаг:

run: echo "Deploy step completed"
Тестирование пайплайна

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

Результат

Docker-образ был успешно собран и опубликован в Docker Hub.

Образ доступен по адресу:

voroshnina/my-flask-app:latest

Pipeline успешно выполняется при каждом push в ветку main.

Вывод

В ходе лабораторной работы был настроен CI/CD пайплайн с использованием GitHub Actions.
Была реализована автоматическая сборка Docker-образа и его публикация в Docker Hub при каждом обновлении репозитория.

Получены практические навыки работы с GitHub Actions, Docker и настройкой CI/CD процессов.
