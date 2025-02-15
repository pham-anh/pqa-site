---
title: GCP Application Development
menu:
  notes:
    name: GCP Application Development
    identifier: gcp
    weight: 401
---

{{< note title="Best practice for application development" >}}

{{< alert type="info">}}
Global reach, scalability and high availability - Secure, loosely coupled, scalable, resilient - Cloud Storage, Cloud Firestore, Cloud SQL, Spanner
{{< /alert >}}

Microservices

- Each service is independent from each other, if one fails, others should work normally

Perform asynchronous operations

- Cloud function trigger

Design for loose coupling

- Cloud Pub/Sub
- Serverless

Implement stateless component for scalability

- Don’t save state internally

Cache content

- Backend: Memcached, Redis (Memorystore)
- Frontend: Cloud CDN

Implement API gateways to make backend functionality available to consumer applications

- Cloud Endpoints, apigee

Use federated identity management

- Identity Platform: sign in with Google, Facebook, Twitter, GitHub, email

Implement health-check endpoints

- Cloud Monitoring → check to /heath

Setup logging and monitor your application’s performance

- print log to stdout or stderr → it will be streamed to Cloud Logging.

Handle transient and log-lasting errors gracefully

- **Retry with exponential backoff**
- Fail gracefully if the error persists (save the CPU cycle)
- Hide the integrated microservice if it is down (instead of showing an error message)

Test , develop DR plan

- Canary testing, blue/green deployments

CI CD

Use the strangler pattern to re-architecture applications

- Incrementally replace components of the old application with the new services

![](../attachments/image-20221224-114214.png)

{{< /note >}}

{{< note title="Getting Started With Application Development" >}}

Cloud APIs

- Interact with compute, networking, storage, machine learning by code
- Make calls through HTTP, JSON, and gRPC interfaces

Google Cloud SDK

- Command line tools
- Language-specific Cloud Client libraries
-   Simpler then calling API
-   Recommended for making Cloud API requests from applications
-   Provide an optimized developer experience (handling low level communication with the server, including authentication; provide retry logic for transient network failures)
-   Receive performance benefits from gRPC APIs

gcloud CLI

- gcloud, gsutil, bq

Emulators for Google Cloud services

- gcloud beta emulators
- Available for: Cloud Bigtable, Datastore, Firestore, Pub/Sub, Cloud Spanner

{{< /note >}}

{{< note title="Storage overview" >}}

![](../attachments/image-20221224-215347.png)

![](../attachments/image-20221225-062357.png)

![](../attachments/image-20221225-062804.png)

{{< /note >}}

{{< note title="Cloud Storage" >}}

- Storing images and videos (e.g. user upload), object and blobs, unstructured data
- Can GET data via HTTP with the key is the object name
{{< /note >}}

{{< note title="Firestore" >}}

#### Native mode

* Fully managed, serverless, NoSQL<br>- Autoscaling in and out<br>- Native and web client libraries<br>- Read-time updates and offline features
* Ideal for<br>- Native mobile and web clients<br>- Document-oriented data<br>- Durable key-value data<br>- Hierarchical data<br>- Managing multiple indexes<br>- Transactions<br>- Large collections of small documents

#### Datastore mode

* Fully manage NoSQL<br>- Scalable<br>- No mobile and web client libraries<br>- No real-time and offline features
* Ideal for<br>- Server applications<br>- Semi-structured application data<br>- Durable key-value data<br>- Hierarchical data<br>- Managing multiple indexes<br>- Transaction<br><br>Example: product catalog, user profile<br>Not relational DB, and not for analytics

{{< /note >}}

{{< note title="Cloud Bigtable" >}}

- High performance wide column NoSQL database service
- Sparsely populate table
- Can scale to billions of rows and thousands of columns
- Can store TB to PB of data
- Built for fast key-value look up and scanning over a defined key range
- Update to individual row is atomic

Ideal for

- Operational applications
- Analytical applications
- Storing large amount of single-keyed data
- MapReduce operations

Latency: sub 10ms, seamless scaling, changes in deployment configuration are immediate (no downtime during reconfiguration)

Support HBase API

{{< /note >}}

{{< note title="Cloud SQL" >}}

- Managed service (replication, failover, backups)
- MySQL, PostgreSQL, SQL Server
- Relational database service
- Proxy for secure access (2nd generation only)
-   Must enable Cloud SQL API
-   Must provide the proxy with a valid user account

Ideal for

- Web frameworks
- Structured data
- OLTP workloads
- Application using MySQL, PostgreSQL

`99.95% SLA` three and a half nines, max downtime 4.38 hour a year

{{< /note >}}

{{< note title="Cloud Spanner" >}}

- Mission-critical relational database
- Transaction consistency
- Global scale
- High availability
-   Automatic synchronous replication
- Multi-region replication

`99.999% SLA` Five 9 SLA (max downtime 5 minutes 15 seconds a year)

Ideal for

- Relational, structured and semi-structured data that require hight availability, strong consistency, and transactional reads and writes

Diff from Cloud SQL

- Requires every table to have a primary key
- Supports interleaved tables where child rows are inserted into the table adjacent to the parent row
-   Improve query performance when joining between parent and child

{{< /note >}}

{{< note title="BigQuery" >}}

- Data warehouse for analytics
- Fully-managed
- Petabyte scale
- Fast response time
- Serverless

Ideal for

- OLAP workloads
- Big data exploration and processing
- Report via BI tools

{{< /note >}}

{{< note title="MSSQL" >}}

- Can use Compute Engine with MSQQL image preload (SQL server standard, web, enterprise)
- Not a managed service like Cloud SQL or Spanner

{{< /note >}}

{{< note title="Storage for mobile" >}}

- Cloud storage for Firebase
- Firebase
- Firebase hosting

{{< /note >}}

{{< note title="Memorystore" >}}

- Cache application data (backend?)
- For Redis and Memcached caching engines
- Ideal for high-performance, scalable web application, gaming and stream processing
- Fully managed service
- Can be protected from the internet in the VPC network and private IP
- Integrated with Cloud Identity and Access Management
{{< /note >}}
