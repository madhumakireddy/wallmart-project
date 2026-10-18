Walmart Data Engineering | Apache Airflow, Databricks & dbt

Project Overview

An end-to-end Walmart Data Engineering project designed to demonstrate modern data ingestion, workflow orchestration, data transformation, and data quality validation.

The project combines Apache Airflow, Databricks, dbt, Docker, Python, SQL, and Delta Lake to build a data engineering pipeline using a Walmart retail dataset.

This implementation is based on the original Walmart Airflow & dbt project, with additional local environment configuration and Databricks validation work.

Technology Stack

Technology

Purpose

Python

Data processing and automation

Apache Airflow

Workflow orchestration

Databricks

Cloud data processing and analytics

Apache Spark

Distributed data processing

dbt

SQL transformations and data testing

Delta Lake

Databricks table storage

Docker & Docker Compose

Containerized Airflow environment

PostgreSQL

Airflow metadata database

Redis & Celery

Distributed task execution

SQL

Data querying and validation

Git & GitHub

Version control

Data Pipeline Architecture

           WALMART DATASET
                 |
         CSV Source Files
                 |
                 v
       DATABRICKS / SPARK
                 |
        Raw Source Tables
                 |
                 v
      APACHE AIRFLOW DAG
                 |
                 v
         dbt Transformations
                 |
       +---------+---------+
       |                   |
       v                   v
   Silver Layer         Gold Layer
  Cleaned Data       Analytical Models
       |                   |
       +---------+---------+
                 |
                 v
        Data Quality Tests
                 |
                 v
       Analytics-Ready Data

Dataset

The project uses six Walmart retail datasets.

Table

Records

customers

2,000

employees

250

order_items

30,021

orders

10,000

products

500

stores

25

Total

42,796

The datasets include customer information, employee records, store details, product details, order transactions, and purchased items.

Databricks Setup

The dataset was uploaded into Databricks using Unity Catalog.

Catalog: workspace

Schema: walmart

Tables:

workspace.walmart.customers
workspace.walmart.employees
workspace.walmart.order_items
workspace.walmart.orders
workspace.walmart.products
workspace.walmart.stores

Data Validation

A Python notebook named walmart_data_validation validates the source tables.

tables = [
    "customers",
    "employees",
    "order_items",
    "orders",
    "products",
    "stores"
]

for table in tables:
    count = spark.table(
        f"workspace.walmart.{table}"
    ).count()
    print(f"{table}: {count} records")

print("Walmart data validation completed!")

Validation result: All six tables were successfully read, with 42,796 total records.

The notebook was also executed as a Databricks serverless Job, which completed successfully.

Apache Airflow Workflow

The Airflow DAG is named orchestrate.

It defines the following tasks:

ingest_cdc

clean_target

source_freshness

silver_technical

silver_technical_tests

silver_business

silver_business_tests

gold_ephemeral

gold_dimensions

gold_facts

The graph represents a sequential workflow beginning with ingestion and continuing through data preparation, freshness validation, Silver transformations, testing, and Gold analytical models.

Airflow Dashboard

Once Docker services are running, the dashboard is accessible at:

http://localhost:8080

Running Airflow Locally

Prerequisites

Docker Desktop with WSL 2 on Windows

Git

VS Code

Databricks workspace

Adequate system RAM for the Airflow services
