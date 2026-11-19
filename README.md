# ctv-full

Orchestrator for CTV Repositories.

## Authors
- Elizabeth Gasañol
- Federico Martinez
- Pablo Pissi

## ERM (Data model)
[Link](https://github.com/unq-pdes-2c-2026-tp/backend/blob/main/ERM.md)

## How do I run it?

### Requirements
- Docker
- Docker compose

### 1. Generate your .env file or use our example

```bash
cp .env.example .env
```

### 2. Run the compose file

```bash
docker compose up -d --pull always
```

### 3. Configure grafana

- Go to http://localhost:3000
- Login using admin/admin
- Skip password change
- Go to connections / datasources on the left menu
- Add prometheus as data source
- As URL, put http://prometheus:9090
- On the top right side, import dashboard
- Paste the content of `dashboard.json`
- Refresh each chart to revalidate the datasource

### 4. Run load tests

With the services running, open a terminal at the root of `ctv-full`. The [backend repository](https://github.com/unq-pdes-2c-2026-tp/backend) must be checked out next to `ctv-full` so Compose can mount its load-test scripts. You do not need to install k6; Compose runs the `grafana/k6` image.

```bash
docker compose --profile load-tests run --rm k6 run --summary-export /results/sustained-load.json /scripts/sustained-load.js
docker compose --profile load-tests run --rm k6 run --summary-export /results/spike-load.json /scripts/spike-load.js
docker compose --profile load-tests run --rm k6 run --summary-export /results/gradual-load.json /scripts/gradual-load.js
```

Test summaries are written to `ctv-full/k6-results/`.

## How do I use it?

Our docker compose creates a test dataset.
Testing credentials:
| email | password |
| ----- | -------- |
| admin@gmail.com | admin |
| agency@gmail.com | agency |
| user@gmail.com | user |

## Project URLS:
| Service  | URL     |
| -------- | ------- |
| Frontend / Main application | http://localhost:80 |
| Backend API | http://localhost:4000/api/ [Swagger](http://localhost:4000/api/schema/swagger-ui/#/) |
| Flights API | http://localhost:8000/api/ [Swagger](http://localhost:8000/api/schema/swagger-ui/#/) |
| Backend Database | localhost:3706 |
| Flights Database | localhost:3707 |
| Grafana | http://localhost:3000 |
