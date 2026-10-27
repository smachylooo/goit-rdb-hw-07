# Домашнє завдання №7 — Смачило Богдан Андрійович

## Тема
Time-series ML features, PostgreSQL JSONB, GIN / expression indexes та EXPLAIN ANALYZE.

## Файли
- `https://colab.research.google.com/drive/1_FBjXcdWMa6kJwoW9_YLVxj6KwJP1C-0?usp=sharing` — Google Colab notebook з п’ятьма завданнями та Reflection.

## Джерело даних
Основний набір: **NYC TLC Yellow Taxi, березень 2024**, офіційний Parquet: https://d37ci6vzurychx.cloudfront.net/trip-data/yellow_tripdata_2024-03.parquet

Notebook автоматично завантажує Parquet через `urllib.request.urlretrieve`, вибирає до 500 000 записів, очищує аномальні значення й завантажує їх до PostgreSQL. Якщо завантаження неможливе, використовує **stub-schema fallback**: 60 днів × 5 зон = 300 рядків. Після запуску notebook друкує, який саме варіант використано.

## Завдання
1. Налаштування PostgreSQL у Colab і daily aggregation `t7_hw_taxi_daily`.
2. Lag (1/7/30), rolling AVG 7d, rolling STDDEV 30d, expanding SUM/AVG, view `v_t7_hw_taxi_features`.
3. JSONB event-log `t7_hw_events` з п’ятьма event-type; `@>`, `?`, `?|`, JSONPath.
4. Порівняння `EXPLAIN (ANALYZE, BUFFERS)` до/після GIN і expression B-tree індексів.
5. Нормалізована `t7_hw_checkouts_norm`, порівняння запитів, Reflection, MongoDB-псевдокод.

## Як запустити
1. Відкрийте `.ipynb` у Google Colab.
2. Оберіть **Runtime → Restart session and run all**.
3. Дочекайтеся встановлення PostgreSQL, завантаження даних і виконання всіх SQL-клітинок.
4. Збережіть notebook **разом з output**, особливо планами EXPLAIN.
5. Для здачі додайте notebook і README до репозиторію `goit-rdb-hw-07`.

> Примітка: пакет `pgserver` недоступний через pip у звичайному Colab, тому використано системний PostgreSQL через apt і SQLAlchemy. Результати EXPLAIN залежать від фактичного запуску та не підставляються штучно.
