# End-to-End Data Engineering Project: dbt, Snowflake & Apache Airflow

An end-to-end Data Engineering project demonstrating data transformation, data modeling, testing, and workflow orchestration using **dbt Core, Snowflake, and Apache Airflow**.

## Overview

This project demonstrates how to build a structured data pipeline using modern Data Engineering tools.

It uses dbt to transform and test data in Snowflake, while Apache Airflow is used to orchestrate the workflow.

The repository includes sample datasets, staging models, a business-level mart, configuration files, and an Airflow DAG.

<img width="1536" height="1024" alt="End-to-End Data Engineering Architecture" src="https://github.com/user-attachments/assets/47491230-77b8-4508-982c-e71222341d32" />


## Tech Stack

- **Python** – Scripting and automation
- **SQL** – Data transformation and modeling
- **dbt Core** – Data transformation, modular modeling, and testing
- **Snowflake** – Cloud data warehouse
- **Apache Airflow** – Workflow orchestration and scheduling
- **Git & GitHub** – Version control and project collaboration

## Architecture

```text
Sample CSV Data
      |
      v
  Data_Files/
      |
      v
   Snowflake
      |
      v
    dbt Core
      |
      v
 Staging Models
      |
      v
  Mart Models
      |
      v
 Data Validation
      ^
      |
 Apache Airflow
 (Workflow Orchestration)
```

*Note: This diagram illustrates the intended workflow. Data loading into Snowflake and Airflow integration must be configured according to your environment.*

## Project Structure

```text
end-to-end-data-engineering-dbt-snowflake-airflow-main/
│
├── Data_Files/
│   ├── customers.csv
│   ├── order_items.csv
│   ├── orders.csv
│   ├── products.csv
│   └── Data_Files.rar
│
├── models/
│   ├── example/
│   │   └── sources.yml
│   ├── staging/
│   │   ├── stg_customers.sql
│   │   ├── stg_order_items.sql
│   │   ├── stg_orders.sql
│   │   └── stg_products.sql
│   └── marts/
│       └── fct_daily_order_revenue.sql
│
├── analyses/
├── macros/
├── seeds/
├── snapshots/
├── tests/
│   └── snowflake_test.yml
│
├── dbt_core_dag.py
├── dbt_project.yml
├── .gitignore
├── .gitattributes
└── README.md
```

## Prerequisites

Before running the project, prepare the following:

- Python installed on your computer
- Git installed
- A Snowflake account with the required database, warehouse, schema, and permissions
- dbt Core and the dbt Snowflake adapter
- Apache Airflow installed in a supported Linux, WSL2, or Docker environment

**Windows note:** Apache Airflow is not officially supported for native Windows installation. Use WSL2 or Docker for the Airflow environment.

## Setup and Installation

### 1. Clone the Repository

Open Git Bash or your terminal and run:

```bash
git clone https://github.com/muhammedshehab1995/End-to-End-DataEngineering-Project-Dbt---Snowflake---Airflow-.git

cd End-to-End-DataEngineering-Project-Dbt---Snowflake---Airflow-
```

### 2. Create a Python Virtual Environment

On Windows PowerShell:

```powershell
python -m venv dbt-env
.\dbt-env\Scripts\Activate.ps1
```

If PowerShell blocks script execution, use an appropriate execution policy for your environment rather than changing system-wide security settings unnecessarily.

On Git Bash:

```bash
python -m venv dbt-env
source dbt-env/Scripts/activate
```

### 3. Install dbt and the Snowflake Adapter

With the virtual environment activated, run:

```bash
python -m pip install --upgrade pip
pip install dbt-core dbt-snowflake
```

Verify the installation:

```bash
dbt --version
```

### 4. Configure the Snowflake Connection

Create or edit the `profiles.yml` file in your dbt configuration directory.

On Windows, this is usually:

```text
C:\Users\<YOUR_USERNAME>\.dbt\profiles.yml
```

On Linux or WSL, it is usually:

```text
~/.dbt/profiles.yml
```

Use the following as a template:

```yaml
YOUR_DBT_PROFILE_NAME:
  target: dev
  outputs:
    dev:
      type: snowflake
      account: YOUR_SNOWFLAKE_ACCOUNT
      user: YOUR_SNOWFLAKE_USER
      password: YOUR_SNOWFLAKE_PASSWORD
      role: YOUR_SNOWFLAKE_ROLE
      database: YOUR_DATABASE
      warehouse: YOUR_WAREHOUSE
      schema: YOUR_SCHEMA
      threads: 4
```

Replace the placeholders with your own Snowflake details.

**Important:** The profile name at the top must match the `profile:` value in your `dbt_project.yml` file. Use an appropriately permissioned Snowflake role, and never commit real credentials to GitHub.

### 5. Test the dbt Connection

From the project root, activate the virtual environment and run:

```bash
dbt debug
```

This checks the dbt project configuration and the connection to Snowflake.

Resolve any reported errors before continuing.

### 6. Run the dbt Models

Once the connection is working, run:

```bash
dbt run
```

This executes the configured dbt models.

Then run:

```bash
dbt test
```

This executes the data tests defined in the project.

The models require their source data and Snowflake objects to be configured correctly before execution.

### 7. Configure Apache Airflow

Run Airflow in your supported Linux, WSL2, or Docker environment, using an environment compatible with your Airflow version and Python version.

For an appropriate Airflow installation, initialize and start Airflow with:

```bash
airflow standalone
```

This command initializes the local Airflow environment and starts its services.

Place `dbt_core_dag.py` in the Airflow DAGs directory configured by your environment. For a default Airflow home, this is typically:

```text
~/airflow/dags/
```

Ensure that the DAG's dbt project path, Python environment, Snowflake connection, and required dependencies are configured for the environment in which Airflow executes.

### 8. Verify the Airflow DAG

Open the Airflow web interface at:

```text
http://localhost:8080
```

Confirm that your DAG appears and that its tasks are configured correctly.

Enable and execute the DAG only after checking its configuration and dependencies.

## Key Learning Outcomes

- Organizing a dbt project using staging and mart models
- Transforming data using SQL
- Configuring dbt to connect to Snowflake
- Running dbt models and data tests
- Understanding workflow orchestration with Apache Airflow
- Managing a Data Engineering project using Git and GitHub

## Future Improvements

- Automate ingestion of source CSV files into Snowflake
- Expand data quality tests
- Add incremental models where appropriate
- Improve Airflow scheduling, retries, and monitoring
- Introduce CI/CD for automated project validation

## Author

**Muhammed Shehab**

Data Engineering | dbt | Snowflake | Apache Airflow | Python | SQL

GitHub: [muhammedshehab1995](https://github.com/muhammedshehab1995)
