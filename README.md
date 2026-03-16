
# Flask ToDo List with MongoDB (Dockerized)

## Overview
This project is a simple **ToDo List web application** built using **Flask** and **MongoDB**.  
The application is containerized using **Docker** and orchestrated with **Docker Compose** to demonstrate a simple multi-container architecture.

The application container communicates with the MongoDB container through a custom Docker network.

---

## Technologies Used
- Python 3.9
- Flask
- MongoDB 4.4
- Docker
- Docker Compose

---

## Project Architecture

The project consists of two services:

1. **myapp**
   - Flask web application
   - Runs on port `5000`

2. **mydb**
   - MongoDB database
   - Stores ToDo tasks

Docker Compose connects both services using a shared network.

```
User Browser
      |
      v
Flask App (myapp)
      |
      v
MongoDB (mydb)
```

---

## Project Structure

```
ToDo-List-using-Flask-and-MongoDB
│
├── app.py
├── requirements.txt
├── Dockerfile
├── docker-compose.yml
├── README.md
└── images/
        ├── todo_app_screenshot.jpg
        └── docker_ps_screenshot.png
```

---

## Dockerfile

The Dockerfile builds the Flask application image.

```
FROM python:3.9

COPY . /app

WORKDIR /app

RUN pip install -r requirements.txt

ENTRYPOINT ["python", "app.py"]
```

---

## Docker Compose Configuration

The `docker-compose.yml` defines two services:

- Flask application container
- MongoDB database container

It also creates a shared network and a persistent volume for MongoDB data.

---

## How to Run the Project

Make sure **Docker** and **Docker Compose** are installed.

### 1. Build and start containers

```
docker-compose up --build
```

### 2. Run in detached mode (optional)

```
docker-compose up -d
```

---

## Access the Application

Open your browser and go to:

```
http://localhost:5000
```

You should see the **ToDo List application interface**.
---

## Environment Variables

The Flask application connects to MongoDB using:

```
MONGO_HOST=mydb
MONGO_PORT=27017
```

Docker Compose automatically resolves the service name `mydb` as the database hostname.

---

## Persistent Storage

MongoDB data is stored using a Docker volume:

```
myvol:/data/db
```

This ensures the database data persists even if the container is restarted.

---

## Stop the Containers

```
docker-compose down
```
