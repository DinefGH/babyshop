# Babyshop 

## Table of Contents 
1. [Description](#1-Description) 
2. [Prerequisites](#2-Prerequisites) 
3. [Quickstart](#3-Quickstart) 
4. [Usage](#4-Usage) 

## 1. Description

In this guide, you’ll get the Babyshop Django app up and running in Docker by first cloning the repository over SSH, then building the Docker image with all dependencies, next running the container—mapping container port 8000 to host port 8025 and enabling automatic restart on failure—and finally configuring your hosts and environment variables for production; once complete, Babyshop will be accessible at http://<your-server-ip>:8025.


## 2. Prerequisites

- **Docker Engine** installed on your server (see Docker’s [installation guide](https://docs.docker.com/engine/install/))
- **Git** installed locally and an SSH key added to your GitHub account
- Basic familiarity with **Django** (settings, migrations) and **environment variables**



## 3. Quickstart


1. Clone the Repository   


```bash
git clone git@github.com:Developer-Akademie-GmbH/baby-tools-shop.git
cd babyshop
``` 


2. Build the Docker Image


```docker
docker build -t babyshop .
``` 


3. Run the Container


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


1. View Logs

```bash
docker logs -f babyshop-app
``` 

Keeps you tailing Django’s output (migrations, errors, requests).



2. Run Django Management Commands

```bash
# Open a shell inside the running container
docker exec -it babyshop-app sh

# Once inside:
python manage.py createsuperuser
``` 



3. Stop and Restart

```bash
# Stop
docker stop babyshop-app

# Start again
docker start babyshop-app
``` 
