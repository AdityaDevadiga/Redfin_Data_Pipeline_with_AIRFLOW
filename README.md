# Automate the Redfin Data Analytics Pipeline

This repository contains scripts and configurations for setting up a data analytics pipeline using Apache Airflow, AWS EMR, and Spark for analyzing Redfin data. The following steps assume you are working inside an AWS EC2 instance.

## Prerequisites

Before you begin, make sure you have the following prerequisites installed and configured:

- AWS EC2 instance
- Python 3.x
- AWS CLI
- Apache Airflow
- Spark
- Boto3 (Python library for AWS interactions)

## Setting Up the Environment on EC2

### 1. Connect to your EC2 instance:

   ```bash
   ssh -i <path-to-your-key.pem> ec2-user@<your-ec2-public-ip>


Purpose: Creates a virtual environment for isolating Python project dependencies.

### 2. Install Required Python Packages:

pip install boto3 apache-airflow apache-airflow-providers-amazon


Purpose: Installs necessary Python packages, including Boto3 for AWS interactions and Apache Airflow.


### 3. Configure AWS CLI:

aws configure

Purpose: Configures the AWS CLI with AWS access key, secret key, region, and output format.

### 4. Install Apache Airflow and Configure:

pip install apache-airflow
airflow initdb

Purpose: Installs Apache Airflow and initializes its database.

### 5. Install Apache Airflow and Configure:

pip install apache-airflow
airflow initdb

Purpose: Installs Apache Airflow and initializes its database.

### 6. Install Spark on Your EC2 Instance:

# Commands to install Spark on your EC2 instance

Purpose: Spark is a requirement for data processing in the analytics pipeline.


### 7. Set Up Necessary IAM Roles on AWS for EMR and S3 Access:

# Commands to set up IAM roles on AWS
Purpose: IAM roles are required for AWS EMR (Elastic MapReduce) and S3 access.

Running the Redfin Data Analytics Pipeline
## Step 1: Download Redfin Data
Run the following command to download Redfin data and upload it to S3:
wget -O - https://redfin-public-data.s3.us-west-2.amazonaws.com/redfin_market_tracker/city_market_tracker.tsv000.gz | aws s3 cp - s3://redfin-data-project-adi/store-raw-data-yml/city_market_tracker.tsv000.gz
Purpose: Downloads Redfin data from a URL and uploads it to an S3 bucket.

## Step 2: Execute Spark Transformation
Run the provided Spark transformation script (transform_redfin_data.py) to clean and transform the Redfin data:

spark-submit transform_redfin_data.py
Purpose: Executes a Spark script to clean and transform the downloaded Redfin data.

## Step 3: Execute Airflow DAG
Copy Airflow DAG Script:

cp redfin_analytics_spark_job_dag.py <AIRFLOW_DAGS_FOLDER_PATH>
Purpose: Copies the provided Airflow DAG script to the Airflow DAGs folder.
Start Airflow Webserver and Scheduler:

airflow webserver -p 8080
airflow scheduler
Purpose: Starts the Airflow webserver and scheduler.
Access Airflow Web UI:

Open your web browser and go to http://localhost:8080. Trigger the redfin_analytics_spark_job_dag DAG.

Purpose: Accesses the Airflow web UI to trigger the DAG for running the analytics pipeline.
