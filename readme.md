🚀 Apache Airflow on Docker

This project sets up Apache Airflow using Docker & Docker Compose, and demonstrates running your first DAG.

📌 What I Did

Created a Dockerfile

Based on apache/airflow:latest

Installed git inside the container

FROM apache/airflow:latest

USER root
RUN apt-get update && \
    apt-get -y install git && \
    apt-get clean

USER airflow


Built a Custom Docker Image

docker build -t sleek-airflow:latest .


Set Up Docker Compose
Configured docker-compose.yml to run Airflow locally:

services:
  sleek-airflow:
    build: .
    image: sleek-airflow:latest
    volumes:
      - ./airflow:/opt/airflow
    ports:
      - "8080:8080"
    command: airflow standalone


Note: Removed version: '3' since it’s deprecated.

Start Airflow

docker compose up -d --build


Airflow web UI available at: http://localhost:8080

Default username/password: airflow / airflow

🎥 Learning Source

This setup was inspired by the YouTube tutorial:
Write and Run Your First DAG | Apache Airflow on Windows Docker

Key Takeaways from the Video

Run Airflow inside Docker on Windows.

Mount a dags folder into the container.

Write a simple Python DAG and place it inside the mounted folder.

Access Airflow Web UI to trigger and monitor DAG execution.

📂 Project Structure
.
├── airflow/            # Local folder mounted into container (/opt/airflow)
│   └── dags/           # Place your DAG files here
├── Dockerfile          # Custom Airflow image
├── docker-compose.yml  # Service configuration
└── README.md           # Project documentation

✅ Next Steps

Add your first DAG under ./airflow/dags/.

Run it from the Airflow web UI.

Extend the Dockerfile with additional dependencies if needed.