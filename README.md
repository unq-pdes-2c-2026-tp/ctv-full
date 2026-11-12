# ctv-full

Orchestrator for CTV Repositories.

## Authors

- Elizabeth Gasañol
- Federico Martinez
- Pablo Pissi

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

## How do I use it?

Our docker compose already runs the commands with a test dataset.

These are the URLs that form the project:

| Service  | URL     |
| -------- | ------- |
| Frontend / Main application | http://localhost:80 |
| Backend API | http://localhost:4000/api/ [Swagger](http://localhost:4000/api/schema/swagger-ui/#/) |
| Flights API | http://localhost:8000/api/ [Swagger](http://localhost:8000/api/schema/swagger-ui/#/) |
| Backend Database | localhost:3706 |
| Flights Database | localhost:3707 |
