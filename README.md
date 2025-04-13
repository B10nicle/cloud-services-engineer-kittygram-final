# 🐈‍⬛ Kittygram

## 🚀 Tech Stack

- **Docker/Docker Compose**
- **Nginx** (gateway)
- **PostgreSQL**
- **Terraform** (Yandex.Cloud)
- **GitHub Actions**
- **Python/Django (backend)**
- **React (frontend)**

## 📁 Project Structure

```
kittygram-final
├── backend/                   # Django app
├── frontend/                  # React app
├── nginx/                     # Nginx config
├── infra/                     # Terraform configuration
├── .github/workflows/         # CI/CD workflows
└── docker-compose.production.yml
```

## ⚙️ Setup and Local Run

1. Start containers:

```bash
docker compose -f docker-compose.production.yml up --build
```

2. Collect static files and apply migrations:

```bash
docker compose exec backend python manage.py collectstatic --noinput
docker compose exec backend python manage.py migrate
```

## ☁️ Deploy to Yandex.Cloud

1. Init Terraform:

```bash
cd infra/
terraform init
```

2. Apply configuration:

```bash
terraform apply -auto-approve
```

Once done, Terraform outputs the VM external IP and VM name.

## 🤖 GitHub Actions Automation

Includes:

- 🔍 Django code linting (`flake8`)
- ✅ Frontend tests (`npm test`)
- 🛠 Docker image build & push
- 🚀 Server deployment
- 🧪 Post-deploy auto tests
- 📩 Telegram notifications

## 🔐 GitHub Secrets Required

| Secret | Description |
|--------|-------------|
| `DOCKER_USERNAME`, `DOCKER_PASSWORD` | DockerHub credentials |
| `SSH_PRIVATE_KEY`, `SERVER_HOST`, `SERVER_USER` | For remote server deployment |
| `POSTGRES_USER`, `POSTGRES_PASSWORD`, `POSTGRES_DB`, `POSTGRES_HOST`, `POSTGRES_PORT` | Database settings |
| `YC_CLOUD_ID`, `YC_FOLDER_ID`, `YC_KEY_JSON`, `SSH_KEY` | Yandex.Cloud credentials |
| `ACCESS_KEY`, `SECRET_KEY` | Terraform backend access |
| `TELEGRAM_TOKEN`, `TELEGRAM_TO` | Telegram notification credentials |

## 🔗 URLs After Deploy

- Main: `http://<EXTERNAL_IP>/`
- Django Admin: `http://<EXTERNAL_IP>/admin/`
