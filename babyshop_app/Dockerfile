# Start with Python 3.11 slim
FROM python:3.11-slim

ENV PYTHONUNBUFFERED=1

WORKDIR /app

# Install system deps (e.g., sqlite3 if needed) in one layer
RUN apt-get update \
    && apt-get install -y --no-install-recommends sqlite3 \
    && rm -rf /var/lib/apt/lists/*

# Copy requirements first for layer caching
COPY requirements.txt /app/
RUN pip install --no-cache-dir -r requirements.txt

# Copy project code
COPY . /app

# Create SQLite file (if using SQLite); in production you'd use external DB
RUN touch /app/db.sqlite3 && chmod 666 /app/db.sqlite3

# Expose port
EXPOSE 8025

# Entrypoint script: run migrations then start server
# Create a small shell script
RUN printf '#!/bin/sh\npython manage.py migrate --noinput\nexec python manage.py runserver 0.0.0.0:8025' > /app/entrypoint.sh \
    && chmod +x /app/entrypoint.sh

CMD ["/app/entrypoint.sh"]