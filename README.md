Deployment of data engineering pipelines
========================================

# Overview
[This project](https://github.com/data-engineering-helpers/data-pipeline-deployment)
intends to develop and maintain a command-line (CLI) utility to help deploy
data engineering pipelines on modern data stack (MDS).

Even though the members of the GitHub organization may be employed by
some companies, they speak on their personal behalf and do not represent
these companies.

## References
* [GitHub - Architecture principles for data engineering pipelines on the Modern Data Stack (MDS)](https://github.com/data-engineering-helpers/architecture-principles)
* [GitHub - `dpcctl`, the Data Processing Pipeline (DPP) CLI utility](https://github.com/data-engineering-helpers/dppctl),
  a Minimal Viable Product (MVP) in Go
* [GitHub - Material for the Data platform - Data contracts](https://github.com/data-engineering-helpers/data-contracts/blob/main/README.md)
* [GitHub - Material for the Data quality - Data contracts](https://github.com/data-engineering-helpers/data-quality/blob/main/README.md)
* [tobiko blog - Why Data Teams Are Adopting Declarative Pipelines](https://tobikodata.com/why-data-teams-are-adopting-declarative-pipelines.html),
  Nov. 2023, by [Iaroslav Zeigerman](https://www.linkedin.com/in/izeigerman/)
* [Substack - We Need a Data Engineering-Specific Language](https://juhache.substack.com/p/we-need-a-data-engineering-specific),
  Feb. 2024, by [Julien Hurault](https://www.linkedin.com/in/julienhuraultanalytics/)

# Specifications

## Needs
* Input: software artifacts (_e.g._, Python wheels, Scala JAR, R packages, SQL dbt packages,
  Airflow DAGs) corresponding to libraries of business models (like the
  [BOM4V libraries](https://github.com/bom4v/metamodels)).
  Let us call that business oriented software the payload/workload.
  The libraries rely on some lower level data processing engines like Spark, Pandas, R
  or dbt
  
* Expected delivery: deployment of that business-oriented payload on to
  a modern data stack (MDS) infrastructure, _e.g._, Spark cluster,
  dbt core/cloud, Kubernetes pods or Lambda/serverless functions

* The data pipelines may optionally be orchestrated, _e.g._, by Airflow;
  the Airflow DAGs are then themselves packaged as Python wheels

* The various deployment environments are specified with a specification-friendly language
  such as YAML or JSON. The specification will typically state the payload (which version
  of which library has to be deployed) and where to deploy it (_e.g._, specific DataBricks
  devevelopment Spark job cluster, Kubernetes pre-production pod in some specific namespace,
  production dbt cloud)

* The specification files (for the deployment of data engineering tasks) are to be maintained
  by the data engineers themselves, not by DevOps/DataOps. Pachyderm model (with specification
  files in JSON) is much better than Chef recipes, for that matter

## Inspiration - Similar tools
* Compared to Apache Beam, we would like something where we do not have to abstract away
  from Spark or Pandas

* Compared to Apache Calcite, something more flexible than just SQL

* Compared to Pachyderm (`pachctl`), where the specification is written in JSON
  and the execution engine is Kubernetes, we would like to accept more
  execution engines (like Spark clusters or dbt cloud) and allowing
  the orchestration by Airflow

* Compared to Flux (`fluxctl`), we would like more frameworks than just Kubernetes. Of course,
  most of the targeted frameworks (_e.g._, Airflow, Spark) may be operated on top of Kubernetes.
  But when we use managed services (_e.g._, DataBricks, AWS MWAA), it is often not an option
  to have them operated on top of Kubernetes in a way allowing to control it

* Infrastructure-as-Code (IaC) is similar in spirit to what we need.
  The main difference is that the infrastructure already exists in our case (managed
  by IaC by the way): DataBricks is already there, as well as all the data-related services
  of AWS (_e.g._, S3, Glue, EMR (for Spark), CodeArtifact, ECR, OpenSearch, RDS, Redshift).
  So, Chef, as the provisional tool in addition to Terraform seems good.
  We were wondering whether Rust would not be a more modern fit?

* Rust or Go could be useful if we have to write such a deployment tool.
  For instance, `pachctl`, `fluxctl` and `kubectl` are written in Go;
  but Rust seems to us right now slightly more fit to the purpose

* In spirit, it should be something like Chef or Puppet: we specify a deployment target,
  and the tool tries to reach the target. Compared to Chef, we would like something simpler
  to use, limited to deployment of only data engineering jobs/tasks on modern data stacks

* That seems rather a task for a tool/utility than for a template

* If no such tool exists today, we may find some combination of simpler tools that
  can make it. The goal is to avoid writing thousands of lines of code/reinventing
  the wheel

## Architecture - Principles

![Data Platform - Principles - Data Engineering](https://github.com/data-engineering-helpers/architecture-principles/blob/main/diagrams/snapshots/Data%20Platform%20-%20Principles%20-%20Data%20Lake%20In%20and%20Out%20-%202023-04%20-%20v2.0.png)

