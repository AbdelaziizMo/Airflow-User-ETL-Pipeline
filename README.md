# Airflow-User-ETL-Pipeline 🚀

## 📌 Project Description

This project implements an automated **Data Engineering Pipeline** using **Apache Airflow**. The workflow is designed to verify API availability, extract random user data, process the raw information, and store it into a structured database.

The pipeline ensures data integrity by performing pre-checks (sensors) and schema validation (DDL) before any data movement occurs.

---

## 🏗 Workflow Architecture (DAG)

The Directed Acyclic Graph (DAG) consists of 5 main tasks:

1. **`CREATE_TABLE`**:
* **Type:** `PostgresOperator` (or Database Operator)
* **Purpose:** Ensures the destination table exists in the database. It executes a SQL script to create the schema if it’s missing.


2. **`IS_API_AVAILABLE`**:
* **Type:** `HttpSensor`
* **Purpose:** A "Sensor" task that pings the external API (e.g., RandomUser API). The pipeline only proceeds if the API returns a successful status.


3. **`EXTRACT_USER`**:
* **Type:** `SimpleHttpOperator`
* **Purpose:** Fetches the raw JSON data from the API endpoint.


4. **`PROCESS_USER`**:
* **Type:** `PythonOperator`
* **Purpose:** Parses the raw JSON, cleans the data, and transforms it into a flattened format (e.g., CSV or Dictionary) ready for loading.


5. **`STORE_USER`**:
* **Type:** `PostgresOperator` / `PythonOperator`
* **Purpose:** The **Load** phase. It inserts the processed user record into the database table.



---

## 🛠 Tech Stack

* **Orchestration:** Apache Airflow
* **Language:** Python 3.x
* **Database:** PostgreSQL (or SQLite)
* **API:** [Random User Generator](https://randomuser.me/)

---

## 📂 Project Structure

```text
├── dags/
│   └── user_processing.py      # The main Airflow DAG definition
├── sql/
│   └── create_table.sql        # SQL script for table initialization
├── logs/                       # Airflow execution logs
└── README.md                   # Project documentation

```

---

## ⚙️ Setup & Installation

1. **Clone the Repository:**
```bash
git clone https://github.com/your-username/airflow-user-processing.git
cd airflow-user-processing

```


2. **Initialize Airflow:**
Make sure Airflow is installed locally or running via Docker.
3. **Configure Connections (Airflow UI):**
* **HTTP Connection:** Create a connection named `user_api` pointing to `https://randomuser.me/`.
* **Postgres Connection:** Create a connection named `postgres` with your DB credentials.


4. **Trigger the DAG:**
Toggle the DAG to `On` in the Airflow dashboard and trigger a manual run to test.

---

## 📈 Future Enhancements

* [ ] Containerize the entire environment using **Docker Compose**.
* [ ] Implement **Slack/Email Notifications** on task failure.
* [ ] Add **Unit Testing** for the transformation logic using Pytest.

---

Would you like me to generate the **Python code** for any specific task (like the processing logic) or help you with the **Docker Compose** file to make it run easily?
