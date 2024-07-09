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

