# Full-Stack FastAPI and React Template

Welcome to the Full-Stack FastAPI and React template repository. This repository serves as a demo application for interns, showcasing how to set up and run a full-stack application with a FastAPI backend and a ReactJS frontend using ChakraUI.

## Project Structure

The repository is organized into two main directories:

- **frontend**: Contains the ReactJS application.
- **backend**: Contains the FastAPI application and PostgreSQL database integration.

Each directory has its own README file with detailed instructions specific to that part of the application.

## Getting Started

To get started with this template, please follow the instructions in the respective directories:

- [Frontend README](./frontend/README.md)
- [Backend README](./backend/README.md)
Certainly! Here are the updated README files along with the frontend and backend Dockerfiles included. You can copy and paste each section into the appropriate README file and Dockerfile in your repository.

### Main README.md

```markdown
# Full-Stack FastAPI and React Template

Welcome to the Full-Stack FastAPI and React template repository. This repository serves as a demo application for interns, showcasing how to set up and run a full-stack application with a FastAPI backend and a ReactJS frontend using ChakraUI.

## Project Structure

The repository is organized into two main directories:

- **frontend**: Contains the ReactJS application.
- **backend**: Contains the FastAPI application and PostgreSQL database integration.

Each directory has its own README file with detailed instructions specific to that part of the application.

## Getting Started

To get started with this template, please follow the instructions in the respective directories:

- [Frontend README](./frontend/README.md)
- [Backend README](./backend/README.md)

## Manual Deployment

### Backend

1. **Navigate to the backend directory:**
   ```sh
   cd backend
   ```

2. **Install dependencies using Poetry:**
   ```sh
   poetry install
   ```

3. **Run database migrations:**
   ```sh
   poetry run alembic upgrade head
   ```

4. **Start the FastAPI server:**
   ```sh
   poetry run uvicorn app.main:app --host 0.0.0.0 --port 8000
   ```

### Frontend

1. **Navigate to the frontend directory:**
   ```sh
   cd frontend
   ```

2. **Install dependencies using npm:**
   ```sh
   npm install
   ```

3. **Start the React development server:**
   ```sh
   npm run dev -- --host 0.0.0.0
   ```

### Database

1. **Start PostgreSQL:**
   ```sh
   docker run --name postgresdb -e POSTGRES_USER=app -e POSTGRES_PASSWORD=database -e POSTGRES_DB=app -p 5432:5432 -d postgres:latest
   ```

### Adminer

1. **Start Adminer:**
   ```sh
   docker run --name adminer -p 8080:8080 --link postgresdb:db -d adminer:latest
   ```

## Docker Deployment

1. **Build and start the Docker containers:**
   ```sh
   docker-compose up --build -d
   ```

2. **Access the services:**
   - Frontend: `http://bestbuy.crabdance.com:5173`
   - Backend API: `http://bestbuy.crabdance.com:8000/api`
   - Backend Docs: `http://bestbuy.crabdance.com:8000/docs`
   - Backend Redoc: `http://bestbuy.crabdance.com:8000/redoc`
   - Adminer: `http://db.bestbuy.crabdance.com:8080`

## Environment Variables

### Backend `.env`

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

### Frontend `.env`

```env
VITE_API_URL=http://bestbuy.crabdance.com:8000
```

## Nginx Proxy Manager Configuration

1. **Login to Nginx Proxy Manager** at `http://18.116.74.34:81`.
2. **Navigate to "Hosts" -> "Proxy Hosts"**.
3. **Click "Add Proxy Host"**.
4. **For `bestbuy.crabdance.com`**:
   - **Domain Names**: `bestbuy.crabdance.com`
   - **Scheme**: `http`
   - **Forward Hostname / IP**: `frontend`
   - **Forward Port**: `5173`
   - **Custom Locations**:
     - **Location**: `/api`
       - **Scheme**: `http`
       - **Forward Hostname / IP**: `backend`
       - **Forward Port**: `8000`
     - **Location**: `/docs`
       - **Scheme**: `http`
       - **Forward Hostname / IP**: `backend`
       - **Forward Port**: `8000`
     - **Location**: `/redoc`
       - **Scheme**: `http`
       - **Forward Hostname / IP**: `backend`
       - **Forward Port**: `8000`
   - **Options**:
     - **Websockets Support**: Enable
     - **Block Common Exploits**: Enable
     - **HTTP/2 Support**: Enable
   - **SSL**:
     - **SSL Certificate**: Request a new SSL certificate using Let's Encrypt
     - **Force SSL**: Enable

5. **For `db.bestbuy.crabdance.com`**:
   - **Domain Names**: `db.bestbuy.crabdance.com`
   - **Scheme**: `http`
   - **Forward Hostname / IP**: `adminer`
   - **Forward Port**: `8080`
   - **Options**:
     - **Websockets Support**: Enable
     - **Block Common Exploits**: Enable
     - **HTTP/2 Support**: Enable
   - **SSL**:
     - **SSL Certificate**: Request a new SSL certificate using Let's Encrypt
     - **Force SSL**: Enable

6. **For `proxy.bestbuy.crabdance.com`**:
   - **Domain Names**: `proxy.bestbuy.crabdance.com`
   - **Scheme**: `http`
   - **Forward Hostname / IP**: `nginx`
   - **Forward Port**: `81`
   - **Options**:
     - **Websockets Support**: Enable
     - **Block Common Exploits**: Enable
     - **HTTP/2 Support**: Enable
   - **SSL**:
     - **SSL Certificate**: Request a new SSL certificate using Let's Encrypt
     - **Force SSL**: Enable

## Conclusion

By following these detailed instructions, you should be able to deploy the full-stack application manually or using Docker. Ensure that all environment variables are correctly set and that the services are accessible through the configured domains.
```

### Frontend README.md

```markdown
# Frontend - ReactJS with ChakraUI

This directory contains the frontend of the application built with ReactJS and ChakraUI.

## Prerequisites

- Node.js (version 14.x or higher)
- npm (version 6.x or higher)

## Setup Instructions

1. **Navigate to the frontend directory**:
    ```sh
    cd frontend
    ```

2. **Install dependencies**:
    ```sh
    npm install
    ```

3. **Run the development server**:
    ```sh
    npm run dev -- --host 0.0.0.0
    ```

4. **Configure API URL**:
   Ensure the API URL is correctly set in the `.env` file.

## Docker Deployment

1. **Build and start the Docker container:**
   ```sh
   docker-compose up --build -d frontend
   ```

## Environment Variables

Set the following environment variables in the `.env` file:

```env
VITE_API_URL=http://bestbuy.crabdance.com:8000
```

## Frontend Dockerfile

Create a `Dockerfile` in the `frontend` directory with the following content:

```dockerfile
FROM node:18-alpine

WORKDIR /var/www/app

# Install specific npm version globally
RUN npm install -g npm@10.8.1

COPY package*.json ./

RUN npm install

# Update npm packages
RUN npm update

COPY . .

COPY .env .env

EXPOSE 5173

# Start the application with --host flag to expose it on all network interfaces
CMD ["npm", "run", "dev", "--", "--host", "0.0.0.0"]
```
```

### Backend README.md

```markdown
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
    poetry run

 bash ./prestart.sh
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

You can now copy and paste the content into the respective README.md files and Dockerfiles in your repository and push the changes to your remote repository.
