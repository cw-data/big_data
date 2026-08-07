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
```

```bash
docker-compose up -d --build
```

```bash
docker-compose exec mongo1 /usr/bin/mongo --eval "if (rs.status()['ok'] == 0) { rsconf = { _id : 'rs0', members: [ { _id : 0, host : 'mongo1:27017', priority: 1.0 }, { _id : 1, host : 'mongo2:27017', priority: 0.5 }, { _id : 2, host : 'mongo3:27017', priority: 0.5 } ] }; rs.initiate(rsconf); } rs.conf();"
```

```bash
docker-compose exec mongo1 apt-get update && apt-get install -y wget
docker-compose exec mongo1 wget [https://github.com/RWaltersMA/mongo-spark-jupyter/raw/master/Source.bson](https://github.com/RWaltersMA/mongo-spark-jupyter/raw/master/Source.bson)
docker-compose exec mongo1 /usr/bin/mongorestore Source.bson -h rs0/mongo1:27017,mongo2:27018,mongo3:27019 -d Stocks -c Source --drop
```

Author
Charles Wainright

[GitHub Profile](https://github.com/cw-data)

