Knowledge Sharing (KS) - Deploying of data processing pipelines (DPP)
=====================================================================

# Overview
This page references some material about deploying Data processing pipelines (DPP).
It is part of the [Data Engineering Helpers - Data pipeline deployment GitHub repository](https://github.com/data-engineering-helpers/data-pipeline-deployment).

# Projects / frameworks

## Kestra
* Home page: https://kestra.io/
* GitHub home page: https://github.com/kestra-io/kestra
* Description: Workflow Automation Platform. Orchestrate & Schedule code in any language, run anywhere, 500+ plugins. Alternative to Zapier, Rundeck, Camunda, Airflow...

## DataPi
* Home page: https://getdatapi.com/
* GitHub home page: https://github.com/velascoluis/datapi-core
* Creator: Luis Velasco
  ([Luis Velasco on LinkedIn](https://www.linkedin.com/in/luisvelascouk/))
* See also [Luis' article on LinkedIn](https://www.linkedin.com/posts/luisvelascouk_thinking-on-implementing-a-distributed-data-activity-7246161112948215808-xuzp),
  posted in October 2024
* Description: open source Python package to streamline the deployment and management of "dataPods": isolated but complete execution environments for Data Products.
  * What's inside a dataPod?
  * => API Rest + Local engine with DuckDB plus semantic layer with malloydata, connected to Apache Polaris (Incubating),
    which offers direct integration to GCS, S3 and ADLS hosting Apache Iceberg tables

## Analytics Engineering Framework (AEF) - Orchestration framework
* GitHub home page: https://github.com/oscarpulido55/aef-orchestration-framework
* Description:
  * Analytics engineers lay the foundation for others to organize, transform, and document data using software engineering principles.
    Providing easy to use data platforms that empower data practitioners to independently build data pipelines in a standardized and scalable way, and answer their own data-driven questions.
  * Data orchestration plays a vital role in enabling efficient data access and analysis, this repository deploys the core artifacts of a streamlined serverless data orchestration framework
    using generic executors as Google Cloud Functions. And deployed via Terraform.
* This Orchestration Framework is the core integrator of the Analytics Engineering Framework comprised of:
  * (This repository) Orchestration Framework: Maintained by Analytics Engineers to provide seamless, extensible orchestration and execution infrastructure.
  * Data Model: Directly used by end data practitioners to manage data models, schemas, and Dataplex metadata.
  * Data Orchestration: Directly used by end data practitioners to define and deploy data pipelines using levels, threads, and steps.
  * Data Transformation: Directly used by end data practitioners to define, store, and deploy data transformations.

# Articles
