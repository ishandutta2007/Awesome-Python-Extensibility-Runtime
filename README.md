# Awesome-Python-Extensibility-Runtime

## Top Python Extensibility & Runtime Ecosystem



**Curated List of SaaS Products & Open-Source GitHub Projects**  

*Focused on Python UDF Runtimes, Serverless GPU Compute & Self-Hosted Function Platforms*  

**Last updated: November 2026**



This repository tracks notable **SaaS platforms** and **open-source projects** for **Python Extensibility & Runtime**. These tools enable organizations to execute Python code in managed environments—running UDFs inside databases, deploying serverless functions on GPUs, and building extensible applications with plugin architectures—without managing the underlying infrastructure.



**Examples** include Snowflake Python UDFs, Databricks PySpark, AWS Lambda Python, Google Cloud Functions Python, Azure Functions Python, Ray on Anyscale, Modal, Replicate, Streamlit Cloud, and Coiled (the category leaders).



**Open-source emphasis**: Python Extensibility & Runtime is a domain where open-source tooling is **genuinely competitive but requires matching the runtime to the workload**. **Ray** is the foundational distributed compute engine—Apache 2.0 licensed, with Ray Serve for scalable model serving and Ray Train for distributed training, running on any cloud or Kubernetes . **Beam (Beta9)** is the leading open-source Modal alternative, explicitly built for serverless GPU inference, background jobs, and agent sandboxes with gVisor isolation, GPU checkpoint restore, and 100% self-hostable code . For database UDFs, **TiDB Cloud Lake** provides a Python UDF server with decorator-based function registration and SQL integration . **vincta** auto-discovers Python functions and serves them over HTTP with a built-in RAM object store—zero config, single command . The critical caveat: **Modal's managed simplicity (zero infrastructure, per-second billing) remains a commercial advantage**—open-source alternatives like Beam require self-hosting and operational ownership .



Contributions welcome! Open a PR to add/update entries. Keep descriptions factual and link to official sites.



## Table of Contents

- [SaaS/Hosted Platforms](#saas-products)

- [Open-Source GitHub Projects](#open-source-github-projects)

- [How to Contribute](#how-to-contribute)

- [Disclaimer](#disclaimer)



## SaaS/Hosted Platforms



- **[Snowflake Python UDFs](https://docs.snowflake.com/)**  

  Python UDFs within Snowflake; write handlers in Python and call from SQL. Supports in-line or staged packages; fully managed with Snowflake's sandboxing.



- **[Databricks PySpark](https://docs.databricks.com/)**  

  Python UDFs and Pandas UDFs within Databricks Runtime; integrates with Unity Catalog and Delta Lake for governed execution.



- **[AWS Lambda Python](https://aws.amazon.com/lambda/)**  

  The pioneering serverless platform; runs Python functions in response to events with automatic scaling and pay-per-invocation pricing.



- **[Google Cloud Functions Python](https://cloud.google.com/functions)**  

  Google's FaaS offering with Python support for event-driven and HTTP triggers; integrates with Pub/Sub, Cloud Storage, and Firestore.



- **[Azure Functions Python](https://azure.microsoft.com/en-us/products/functions)**  

  Microsoft's serverless compute with Python support; triggers and bindings across Azure services.



- **[Ray on Anyscale](https://www.anyscale.com/)**  

  Managed Ray platform from the creators of Ray; powers distributed model training, data processing, and inference across GPU clusters .



- **[Modal](https://modal.com/)**  

  Serverless compute for Python functions and containers on GPUs, billed per second with scale-to-zero and fast cold starts; Python-native developer experience .



- **[Replicate](https://replicate.com/)**  

  Platform for running and fine-tuning open-source models via API; deploy custom models with `cog` and pay per prediction .



- **[Streamlit Cloud](https://streamlit.io/)**  

  Managed hosting for Streamlit apps; deploy Python data apps directly from a GitHub repository.



- **[Coiled](https://coiled.io/)**  

  Managed Dask cluster platform for Python; handles cluster creation and management on AWS, GCP, and Azure .



## Open-Source GitHub Projects



### Distributed Compute & Serverless (Ray, Beam)



- **[Ray](https://github.com/ray-project/ray)**  

  The **foundational open-source distributed AI compute engine** (Apache 2.0, ~35k GitHub stars) . Simple Python decorators to execute functions on a cluster with fine-grained hardware allocation (CPUs, GPUs, TPUs); **Ray Serve** for scalable model serving with dynamic batching; **Ray Train** for distributed training; **Ray Data** for scalable datasets. Runs on any machine, cluster, cloud provider, or Kubernetes . **Best for scaling Python AI workloads from laptop to cluster**—but it is an orchestration layer, not a managed service.



- **[Beam (Beta9)](https://github.com/beam-cloud/beta9)**  

  The **leading open-source Modal alternative** for serverless GPU compute (100% open source and self-hostable) . Features: **GPU support** with fast image builds; **memory/file system snapshotting** and **GPU checkpoint restore** (stop and resume sandboxes preserving running processes); long-running sessions (24h+); **gVisor isolation**; simple Python decorator API (`@function`, `@endpoint`) with no YAML . Used by Coca-Cola, Magellan AI, and Shippabo for serverless inference and sandboxes . **Best for AI teams wanting Modal-like serverless GPU compute** without vendor lock-in—but requires self-hosting infrastructure (k3d for local, Helm for K8s) .



### Database UDF Runtimes



- **[TiDB Cloud Lake Python UDF](https://pypi.org/project/tidbcloudlake-udf/)**  

  Open-source **Python UDF server** for TiDB Cloud Lake . Write functions with `@udf` decorator, run a UDFServer, and register in SQL via `CREATE FUNCTION ... LANGUAGE python HANDLER = 'add' ADDRESS = 'http://...'`. Supports complex types (ARRAY, MAP, TUPLE, VECTOR) with automatic type mapping between SQL and Python . **Best for TiDB users** wanting Python UDFs in their SQL workflows—but it is database-specific and requires a running UDF server.



### Function-as-a-Service (Auto-Discovery)



- **[vincta](https://pypi.org/project/vincta/)**  

  Open-source **auto-discovering Python function server** with a built-in RAM object store . Drop `.py` files in a folder, point vincta at it, and every public function becomes a callable HTTP endpoint with auto-generated Swagger docs. **Heavy objects (DataFrames, arrays) stored by reference**—pass ref strings between functions instead of serializing large data over HTTP . CLI: `vincta --dir ./my_functions --port 8000`. **Best for rapidly exposing Python functions as APIs** without FastAPI/Flask boilerplate—but it is a lightweight server, not a production FaaS platform.



- **[SnapServe](https://pypi.org/project/snapserve/)**  

  Open-source **lightweight framework** to serve Python functions, classes, and stateful objects as remote services . Single command: `snapserve serve calculator:add,subtract`. Features worker threads, concurrency limits, timeouts, and optional result caching . **Best for simple function-serving** without writing server code—but less feature-rich than vincta for data-heavy workloads.



### Extensible Application Frameworks



- **[XCore](https://github.com/traoreera/xcore)**  

  Open-source **plugin-first orchestration framework** built on FastAPI (October 2025) . Features: **AST-based scanning, resource restriction, and C++ security core** for sandboxing plugins; **hot-reloading** of plugins without server restart; native multi-tenancy with resource isolation; service container (SQLAlchemy, Redis, schedulers); CLI for plugin management, signing, and health checks . **Best for building extensible applications** where features are dynamically added/removed—but it is a framework for building your own product, not a runtime platform.



### Additional Strong Open-Source Options



- **Modal Client (SDK)** — Modal's official Python SDK is open-source (Apache 2.0) , but the platform itself is proprietary. **Not a self-hosted runtime**—the SDK is for interacting with Modal's managed service.

- **BentoML** — Open-source model serving framework (Apache 2.0) with a "Bento" packaging model; complements Ray for serving but is inference-focused rather than general Python runtime .



**Frameworks for building custom systems**: For **distributed Python compute with GPU scaling**, Ray is the foundational open-source engine . For **serverless GPU compute without Modal lock-in**, Beam (Beta9) provides the closest open-source alternative . For **database UDFs**, TiDB Cloud Lake provides a Python UDF server . For **auto-discovering function APIs**, vincta offers zero-config serving . For **extensible plugin architectures**, XCore provides sandboxed plugin orchestration . No open-source project matches Modal's **managed simplicity and per-second billing**—self-hosting means owning infrastructure and operational responsibility.



## How to Contribute



1. Fork the repo.

2. Add/edit entries in `README.md` (follow existing format).

3. Include: name, link, 1–2 sentence description, and whether it's SaaS or open-source.

4. Submit PR with a short explanation.



Star the repo if you find it useful!



## Disclaimer



- This is a **community-curated** list — not exhaustive and not an endorsement.

- Python runtime platforms handling production code and data must comply with organizational security policies; **self-hosted solutions place full responsibility for sandboxing, resource isolation, and patching on the operator**.

- **Open-source Python runtimes are mature at the compute and serving layers but require operational investment**—Ray provides distributed compute , and Beam provides serverless GPU compute . However, **no open-source project matches Modal's managed simplicity** (zero infrastructure, per-second billing, fast cold starts) —self-hosting means owning Kubernetes clusters, GPU provisioning, and scaling policies. Choose based on whether you need managed convenience (Modal) or self-hosted control (Ray, Beam).

- Verify license terms for commercial use; Ray uses Apache 2.0 , Beam is open-source (check repository) , and Modal's SDK is Apache 2.0 but the platform is proprietary .



---



**Made for Python developers, platform engineers, and organizations choosing their runtime and extensibility stack.**  

Let's make Python runtimes more open, but with clear eyes about the managed simplicity and operational ownership trade-offs that define each path.
