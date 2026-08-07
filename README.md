# Containerized Big Data Architecture: MongoDB, PySpark & JupyterLab

This repository implements a fully containerized distributed data processing pipeline and analytical workflow. The project combines Docker containerization, a multi-node MongoDB replica set, Apache Spark for distributed computation, and JupyterLab for interactive data wrangling and time-series visualization.

---

## Architecture & Technology Stack
* **Containerization:** [Docker Desktop](https://www.docker.com/products/docker-desktop/) & Docker Compose (running via WSL)
* **NoSQL Database:** MongoDB (configured as a 3-node replica set for high availability)
* **Distributed Processing:** Apache Spark / PySpark (integrated via the MongoDB Spark Connector)
* **Interactive Environment:** JupyterLab
* **Visualization & Reporting:** Matplotlib, Pandas, and custom-styled HTML report outputs

---

## Project Workflow
1. **Infrastructure Provisioning:** Spins up containerized services and initiates a primary-secondary MongoDB replica set.
2. **Data Ingestion:** Seeds distributed collections with high-frequency stock transaction records (`Source.bson`).
3. **Data Wrangling & Type Casting:** Connects PySpark to MongoDB, casts raw string timestamps to native timestamp objects, and formats schema attributes.
4. **Time-Series Window Engineering:** Constructs precise time-based window frames using Unix epoch casting to compute accurate rolling moving averages.
5. **Visualization & Export:** Generates clean chronological Matplotlib trend analysis charts and exports structured views into CSV, JSON, and Parquet formats.

---

## Getting Started

### 1. Clone the Repository
```bash
git clone [https://github.com/cw-data/big_data.git](https://github.com/cw-data/big_data.git)
cd big_data
