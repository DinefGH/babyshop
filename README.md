# Babyshop 

## Table of Contents 
1. [Description](#1-Description) 
2. [Prerequisites](#2-Prerequisites) 
3. [Quickstart](#3-Quickstart) 
4. [Usage](#4-Usage) 

## 1. Description

This guide shows you how to get the Babyshop Django app up and running in Docker. You’ll learn how to:

Clone the repository over SSH

Build the Docker image with all dependencies

Run the container, map port 8000, and auto-restart on failure

Configure hosts and environment variables for production

By the end, Babyshop will be accessible at http://<your-server-ip>:8025.

## 2. Prerequisites

- **Docker Engine** installed on your server (see Docker’s [installation guide](https://docs.docker.com/engine/install/))
- **Git** installed locally and an SSH key added to your GitHub account
- **Sudo** or root access on the host to install packages and manage Docker
- (Optional) **Docker Compose** if you plan to orchestrate multiple services
- Basic familiarity with **Django** (settings, migrations) and **environment variables**



## 3. Quickstart


### Clone the Repository   


```bash
git clone git@github.com:Developer-Akademie-GmbH/baby-tools-shop.git
cd babyshop
``` 


### Build the Docker Image


```bash
docker build -t babyshop:latest .
``` 


### Run the Container


```bash
docker run -d \
  --name babyshop-app \
  -p 8025:8025 \
  -v "$(pwd)/db.sqlite3":/app/db.sqlite3 \
  --restart unless-stopped \
  babyshop:latest
``` 

Maps port 8025 on your host to 8025 in the container

Mounts your local db.sqlite3 so data persists

## 4. Usage


### View Logs

```bash
docker logs -f babyshop-app
``` 

Keeps you tailing Django’s output (migrations, errors, requests).



### Run Django Management Commands

```bash
# Open a shell inside the running container
docker exec -it babyshop-app sh

# Once inside:
python manage.py createsuperuser
python manage.py collectstatic --noinput
``` 



### Stop and Restart

```bash
# Stop
docker stop babyshop-app

# Start again
docker start babyshop-app
``` 
