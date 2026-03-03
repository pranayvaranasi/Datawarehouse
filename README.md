# Built a Data Warehouse using AWS Glue, S3, and Amazon Redshift

## Introduction

This project demonstrates  a scalable cloud-based data
warehouse using AWS Glue, Amazon S3, and Amazon Redshift.\
The pipeline extracts raw data, transforms it using AWS Glue, stores
intermediate data in Amazon S3, and loads structured datasets into
Amazon Redshift for analytics and reporting.

------------------------------------------------------------------------

## Table of Contents

-   [Architecture Overview](#architecture-overview)
-   [Project Structure](#project-structure)
-   [Prerequisites](#prerequisites)
-   [Installation & Setup](#installation--setup)
-   [Data Pipeline Workflow](#data-pipeline-workflow)
-   [Usage](#usage)
-   [Features](#features)
-   [Configuration](#configuration)
-   [Example Queries](#example-queries)
-   [Troubleshooting](#troubleshooting)
-   [Future Improvements](#future-improvements)
-   [Contributors](#contributors)
-   [License](#license)

------------------------------------------------------------------------

## Architecture Overview

Source Data → S3 (Raw) → AWS Glue (Transform) → S3 (Processed) →
Redshift → Analytics
<img width="775" height="612" alt="image" src="https://github.com/user-attachments/assets/769155ac-36c8-48fb-8ad8-9235a6f97275" />
<img width="3583" height="2216" alt="image" src="https://github.com/user-attachments/assets/15a5347c-7039-4604-972c-0d8d212f123b" />


------------------------------------------------------------------------

## Project Structure

    ├── scripts/
    │   ├── glue_jobs/
    │   ├── sql/
    │   └── utilities/
    ├── data/
    │   ├── raw/
    │   └── processed/
    ├── architecture/
    ├── README.md

------------------------------------------------------------------------

## Prerequisites

-   AWS Account
-   IAM roles configured for Glue, S3, and Redshift
-   Amazon Redshift cluster provisioned
-   AWS CLI configured (optional)

------------------------------------------------------------------------

## Installation & Setup

### 1. Create an S3 Bucket

Create folders: - /raw - /processed

### 2. Configure AWS Glue

-   Create a Glue Database
-   Create Crawlers for raw and processed data
-   Create ETL Jobs

### 3. Set Up Amazon Redshift

-   Create cluster
-   Configure security groups
-   Create target schema and tables

------------------------------------------------------------------------

## Data Pipeline Workflow

1.  Upload raw data to S3
2.  Run Glue Crawler
3.  Execute Glue ETL job
4.  Load transformed data into Redshift
5.  Run analytical queries

------------------------------------------------------------------------

## Usage

1.  Run Glue job
2.  Validate processed data in S3
3.  Connect to Redshift
4.  Execute SQL queries

------------------------------------------------------------------------

## Features

-   Serverless ETL with AWS Glue
-   Scalable storage using Amazon S3
-   Columnar analytics with Amazon Redshift
-   Automated schema detection

------------------------------------------------------------------------

## Configuration

Example environment variables:

    S3_BUCKET=your-bucket-name
    REDSHIFT_HOST=your-redshift-endpoint
    REDSHIFT_DB=dev
    REDSHIFT_USER=admin

------------------------------------------------------------------------

## Example Queries

### Total Sales by Region

``` sql
SELECT region, SUM(total_sales)
FROM sales_fact
GROUP BY region;
```

### Top 10 Products

``` sql
SELECT product_name, SUM(quantity_sold) AS total_qty
FROM sales_fact
GROUP BY product_name
ORDER BY total_qty DESC
LIMIT 10;
```

------------------------------------------------------------------------

## Troubleshooting

  ------------------------------------------------------------------------
  Issue           Possible Cause                    Solution
  --------------- --------------------------------- ----------------------
  Glue job fails  IAM role missing permission       Attach required
                                                    policies

  Redshift COPY   Incorrect IAM role                Verify cluster IAM
  error                                             role

  Crawler not     Incorrect S3 path                 Validate bucket
  detecting                                         structure
  schema                                            
  ------------------------------------------------------------------------

------------------------------------------------------------------------

## Future Improvements

-   Add CI/CD for Glue jobs
-   Implement orchestration with Step Functions
-   Integrate BI tools
-   Add data quality validation
-   Implement incremental loads

------------------------------------------------------------------------

## Contributors

Pranay Varanasi

------------------------------------------------------------------------

