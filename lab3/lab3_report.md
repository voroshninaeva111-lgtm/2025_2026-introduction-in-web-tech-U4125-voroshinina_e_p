# Лабораторная работа №3  
## Настройка мониторинга с Prometheus и Grafana

---

## Цель работы

Настроить систему мониторинга с использованием Prometheus и Grafana для сбора и визуализации метрик системы.

---

## Используемые инструменты

- Docker
- Prometheus
- Node Exporter
- Grafana

---

## Архитектура решения

Система мониторинга состоит из следующих компонентов:

- **Node Exporter** — собирает системные метрики (CPU, память, диск)
- **Prometheus** — собирает и хранит метрики
- **Grafana** — визуализирует метрики

Схема работы:


---

## 1. Создание конфигурации Prometheus

Создана папка `prometheus` и файл конфигурации `prometheus.yml`:

global:
  scrape_interval: 15s

scrape_configs:
  - job_name: 'prometheus'
    static_configs:
      - targets: ['localhost:9090']

  - job_name: 'node-exporter'
    static_configs:
      - targets: ['node-exporter:9100']
   
  ## 2. Запуск Node Exporter

  docker run -d \
  --name node-exporter \
  --network monitoring \
  --restart=unless-stopped \
  -p 9100:9100 \
  -v "/proc:/host/proc:ro" \
  -v "/sys:/host/sys:ro" \
  -v "/:/rootfs:ro" \
  prom/node-exporter \
  --path.procfs=/host/proc \
  --path.rootfs=/rootfs \
  --path.sysfs=/host/sys \
  --collector.filesystem.mount-points-exclude="^/(sys|proc|dev|host|etc)($$|/)"

  Проверка работы:

http://localhost:9100/metrics

 ## 3. Запуск Prometheus

Создан том и сеть:

docker volume create prometheus-data
docker network create monitoring

Запуск контейнера:

docker run -d \
  --name prometheus \
  --network monitoring \
  --restart=unless-stopped \
  -p 9090:9090 \
  -v prometheus-data:/prometheus \
  -v $(pwd)/prometheus:/etc/prometheus \
  prom/prometheus \
  --config.file=/etc/prometheus/prometheus.yml

Проверка:

http://localhost:9090

В разделе Targets все сервисы имеют статус UP.

<img width="1457" height="829" alt="Снимок экрана 2026-03-17 в 2 29 08 AM" src="https://github.com/user-attachments/assets/c598587b-8abb-4e71-b223-d3d8488a363c" />

 ## 4. Запуск Grafana

Создан том:

docker volume create grafana-data

Запуск:

docker run -d \
  --name grafana \
  --network monitoring \
  --restart=unless-stopped \
  -p 3000:3000 \
  -v grafana-data:/var/lib/grafana \
  -e "GF_SECURITY_ADMIN_PASSWORD=admin" \
  grafana/grafana

Доступ:

http://localhost:3000

Логин/пароль:

admin / admin

## 5. Настройка Grafana

Добавлен источник данных:

Тип: Prometheus

URL: http://prometheus:9090

Проверка подключения: успешно выполнена.

## 6. Создание дашборда

Создан дашборд с визуализацией метрик:

CPU
node_cpu_seconds_total
RAM
node_memory_MemAvailable_bytes
Disk

<img width="1470" height="956" alt="Снимок экрана 2026-03-17 в 2 32 05 AM" src="https://github.com/user-attachments/assets/a44325ab-392a-466b-b04d-eca1dec10eef" />


## 7. Тестирование

В ходе тестирования проверено:

Контейнеры запущены (docker ps)

Prometheus собирает метрики

Grafana отображает графики

Все сервисы доступны

# Результат

Настроена система мониторинга

Метрики успешно собираются и отображаются

Создан дашборд с основными показателями системы

# Вывод

В ходе лабораторной работы была настроена система мониторинга на основе Prometheus и Grafana.
Реализован сбор метрик с помощью Node Exporter и их визуализация в Grafana.

Получены практические навыки работы с:

Docker

Prometheus

Grafana

мониторингом систем



 
