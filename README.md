# 📝 Todo List App — Flask + MongoDB + Docker

A simple Todo List web application built with **Flask** and **MongoDB**, containerized using **Docker** and orchestrated with **Docker Compose**.

---

## Project Structure

```
ToDo-List-using-Flask-and-MongoDB/
├── app.py                  # Main Flask application
├── requirements.txt        # Python dependencies
├── Dockerfile              # Docker image build instructions
├── docker-compose.yml      # Multi-container orchestration
└── README.md
```

---

## Prerequisites

Make sure you have the following installed:

- [Docker](https://docs.docker.com/get-docker/) (v20+)


##  Getting Started

### 1. Clone the Repository

```bash
git clone 
cd ToDo-List-using-Flask-and-MongoDB
```

### 2. Build the Docker Image

```bash
docker build -t myimgg .
```

### 3. Run with Docker Compose

```bash
docker compose up -d
```

The app will be available at: **http://localhost:5000**

### 4. Stop the Containers

```bash
docker compose down
```

## 🐳 Docker Configuration

### Dockerfile

```dockerfile
FROM python:3.9

WORKDIR /app

COPY . /app

RUN pip install -r requirements.txt

EXPOSE 5000

ENTRYPOINT ["python", "app.py"]
```

### docker-compose.yml

```yaml
services:
  myapp:
    image: myimgg
    networks:
      - mynet
    volumes:
      - appvol:/app
    depends_on:
      - mydb
    ports:
      - "5000:5000"
    environment:
      - MONGO_HOST=mydb
      - MONGO_PORT=27017

  mydb:
    image: mongo:4.4
    networks:
      - mynet
    volumes:
      - dbvol:/data/db
    ports:
      - "27017:27017"

volumes:
  appvol:
  dbvol:

networks:
  mynet:
```

> **Note:** `appvol` and `dbvol` are separate named volumes to prevent data conflicts between the app and the database.

---


##  Development

To view logs:

```bash
# All services
docker compose logs -f

# Specific service
docker compose logs -f myapp
docker compose logs -f mydb
```