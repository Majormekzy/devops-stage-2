# Backend - FastAPI with PostgreSQL

This directory contains the backend of the application built with FastAPI and a PostgreSQL database.

## Prerequisites

- Python 3.8 or higher
- Poetry (for dependency management)
- PostgreSQL (ensure the database server is running)

### Installing Poetry

To install Poetry, follow these steps:

```sh
curl -sSL https://install.python-poetry.org | python3 -
```

Add Poetry to your PATH (if not automatically added):

## Setup Instructions

1. **Navigate to the backend directory**:
    ```sh
    cd backend
    ```

2. **Install dependencies using Poetry**:
    ```sh
    poetry install
    ```

3. **Set up the database with the necessary tables**:
    ```sh
    poetry run bash ./prestart.sh
    ```

4. **Run the backend server**:
    ```sh
    poetry run uvicorn app.main:app --reload
    ```

5. **Update configuration**:
   Ensure you update the necessary configurations in the `.env` file, particularly the database configuration.

## Docker Deployment

1. **Build and start the Docker container:**
   ```sh
   docker-compose up --build -d backend
   ```

## Environment Variables

Set the following environment variables in the `.env` file:

```env
DOMAIN=bestbuy.crabdance.com
ENVIRONMENT=local
PROJECT_NAME="Full Stack FastAPI Project"
STACK_NAME=full-stack-fastapi-project
BACKEND_CORS_ORIGINS="http://bestbuy.crabdance.com,http://bestbuy.crabdance.com:5173,https://bestbuy.crabdance.com,https://bestbuy.crabdance.com:5173"
SECRET_KEY=backend
FIRST_SUPERUSER=devops@hng.tech
FIRST_SUPERUSER_PASSWORD=devops#HNG11
USERS_OPEN_REGISTRATION=True
SMTP_HOST=
SMTP_USER=
SMTP_PASSWORD=
EMAILS_FROM_EMAIL=info@example.com
SMTP_TLS=True
SMTP_SSL=False
SMTP_PORT=587
POSTGRES_SERVER=bestbuy.crabdance.com
POSTGRES_PORT=5432
POSTGRES_DB=app
POSTGRES_USER=app
POSTGRES_PASSWORD=database
```

## Backend Dockerfile

Create a `Dockerfile` in the `backend` directory with the following content:

```dockerfile
FROM python:3.10-slim

ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1
ENV PYTHONPATH "${PYTHONPATH}:/app"

# Install required dependencies
RUN apt-get update && apt-get install -y \
    libpq-dev

# Set working directory
WORKDIR /app

# Install Poetry
RUN pip install poetry

# Copy and install dependencies
COPY pyproject.toml poetry.lock /app/
RUN poetry config virtualenvs.create true \
    && poetry install --no-dev --no-interaction --no-ansi

# Copy the application code
COPY . /app/

# Make prestart script executable
RUN chmod +x /app/prestart.sh

# Expose the backend port
EXPOSE 8000

# Define the entrypoint
ENTRYPOINT ["poetry", "run", "bash", "-c", "/app/prestart.sh && uvicorn app.main:app --host 0.0.0.0 --port 8000"]
```
```
