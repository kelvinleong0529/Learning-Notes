# **Grafana Loki**
- `Loki` is a horizontally scalable, highly available, multi-tenant log aggregation solution
- rather than indexing the contents of the logs, it uses a set ot labels for each log stream
- was created in response to a request for an open-source tool that could easily choose and examine time-series logs that were kept stably
- log visualization technologies with querying capabilities, log aggregation, and distributed log tracing can all help identify system issues

# **Architecture**
- `Loki` service was created using a set of components, refer to the diagram below:
![Grafana Loki!](https://www.atatus.com/blog/content/images/size/w1000/2022/02/Grafana-Loki-s-Architecture.png)

## **1. Distributor**
- client data streams are handled and validated by distributor module
- valid data is chunked and transmitted to several ingesters for processing in parallel
- to check log data in the distributor and process it in different downstream modules, the distributor uses Prometheus-like labels
- grafana Loki cannot construct the index it needs for searching without labels

## **2. Ingester**
- data is written to long-term storage via the ingester module. Loki indexes metadata rather than storing the log data it ingests, eg:AWS S3, Apache Cassandra, or local file systems are examples of flexible object storage.
- for in-memory searches, the ingester also returns data
- unflushed data is lost when Ingester crashes, with poor user setup assuring redundancy, Loki can irreversibly lose logs from ingesters