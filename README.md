# SteelCalculator

Веб-приложение для оптимизации состава инструментальной легированной стали по критерию минимальной стоимости.

Приложение подбирает содержание легирующих элементов с учётом заданных ограничений на свойства стали, рассчитывает стоимость полученного состава и позволяет сохранять и сравнивать результаты.

## Возможности

* подбор оптимального состава стали;
* минимизация стоимости легирующих элементов;
* учёт ограничений на механические и технологические характеристики;
* сохранение результатов расчётов в PostgreSQL;
* визуализация результатов;
* экспорт данных;
* запуск приложения в Docker-контейнерах;
* автоматическая проверка и сборка проекта;
* мониторинг приложения.

## Технологии

**Backend**

* Python 3.11
* Flask
* SQLAlchemy
* NumPy
* SciPy

**Database**

* PostgreSQL
* Flask-Migrate / Alembic

**Infrastructure**

* Docker
* Docker Compose
* Jenkins
* GitHub Actions

**Monitoring**

* Prometheus
* Grafana

**Дополнительно**

* Matplotlib
* Openpyxl

## Оптимизация

Подбор состава реализован как задача условной оптимизации.

Целевая функция — минимизация стоимости легирующих элементов при соблюдении заданных ограничений на состав и характеристики стали.

Для решения используется алгоритм **SLSQP** из `scipy.optimize`.

## Структура проекта

```text
SteelCalculator/
├── .github/             # workflows GitHub Actions
├── app/                 # Flask-приложение
├── deploy/              # конфигурация развёртывания
├── jenkins/             # конфигурация Jenkins
├── migrations/          # миграции базы данных
├── monitoring/          # Prometheus и Grafana
├── docker-compose.yml
├── Dockerfile
├── Jenkinsfile
├── pyproject.toml
├── requirements.txt
└── README.md
```

## Запуск проекта

### 1. Клонировать репозиторий

```powershell
git clone https://github.com/dislikke/steel-composition-optimizer.git
cd steel-composition-optimizer
```

### 2. Настроить переменные окружения

Создать `.env` на основе файла `.env.example`.

Пример:

```env
POSTGRES_DB=steel_db
POSTGRES_USER=steel_user
POSTGRES_PASSWORD=your_password
DATABASE_URL=postgresql://steel_user:your_password@db:5432/steel_db
SECRET_KEY=your_secret_key
```

Файл `.env` содержит локальные настройки и не хранится в репозитории.

### 3. Запустить приложение

```powershell
docker compose up -d --build
```

### 4. Применить миграции

```powershell
docker compose exec web flask db upgrade
```

После запуска приложение доступно по адресу:

```text
http://localhost:5002
```

## CI/CD

В проекте настроены:

* **GitHub Actions** — автоматические проверки при изменениях в репозитории;
* **Jenkins Pipeline** — автоматизация сборки и запуска проекта с использованием `Jenkinsfile`.

## Мониторинг

Для мониторинга приложения используются **Prometheus** и **Grafana**.

При локальном запуске сервисы доступны по адресам:

```text
Prometheus — http://localhost:9090
Grafana    — http://localhost:3000
```

## Автор

**Федотова Диана**

Проект разработан в рамках выпускной квалификационной работы по направлению «Программная инженерия».
