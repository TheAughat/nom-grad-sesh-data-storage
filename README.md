# nom-grad-sesh-data-storage

# Module 1: Real-time Market Data Ingestion
*By: Daniel Rodrigues*

Choice: InfluxDB

This is a NoSQL DB specifically designed for time-series data. From it's wikipedia page: "It is used for storage and retrieval of time series data in fields such as operations monitoring, application metrics, Internet of Things sensor data, and real-time analytics." It's also said to scale easily for high-volume data and real-time queries.

Additionally, it has:
- High-speed ingestion
- Built-in data retention policies
- Efficient compression for historical data
- Time-based partitioning
- Sub-millisecond query performance

Thus, from my findings, InfluxDB's columnar storage design and time-structured merge tree deliver sub-millisecond query performance while maintaining efficient compression ratios (often 10:1). Native features like continuous queries, retention policies, and downsampling make it ideal for high-frequency trading data management, while its query language (InfluxQL) simplifies complex time-series analytics. The enterprise version offers clustering for high availability and horizontal scaling, critical for our 5M records/sec requirement.

---

# Module 2: Client Portfolio Management
*By: Molly Guinan*

Database type: RDBSM
Reasons why:

Structured Data:
Client transactions are structured, which aligns well with the tabular format.

Complex Joins:
There's a requirement for complex joins across client portfolios — a strength of relational databases.

GDPR Compliance:
GDPR requires auditing and traceability; RDBMSs support detailed logs, triggers, and user roles for tracking changes and access.

Hint about Eventual Consistency:
The hint implies strong consistency is necessary — RDBMSs offer this natively, unlike other databases.

---

# Module 3: Research & Analytics
*By: Angelina Rodrigues*

We recommend using Elasticsearch or MongoDB as the main database.
Why Elasticsearch?

Great for searching text quickly
Flexible for different types of data
Works well with Python and R
Fast and can handle lots of data
MongoDB is a good alternative:

Stores documents easily
Can search text (not as well as Elasticsearch)
Flexible for different data types
Works well with Python and R
We don't recommend just using a regular database (like MySQL) because:

It's not as good at searching text
It's harder to use with different types of data
It's not as good for big data analysis
Best setup:

Use Elasticsearch for searching research reports
Use MongoDB for storing different types of data
You could add a regular database for some structured data if needed
You5:07 PM

---

# Module 4: Regulatory Reporting
*By: Brianna Wang*

1. Database chosen

A NoSQL database could work best for this scenario with a combination of a Data Warehouse

2. Why did you choose the database type?

A NoSQL database can be used for handling the real-time alerts and providing quick responses for auditors since this is regulatory data. The data warehouse can be used to store and process the transaction reports and compliance logs especially since they will exist on a petabyte-scale.

3. What structure do you suggest?

Use NoSQL to store real-time AML alerts. Use Data Warehouse to store MiFID II transaction reports and FATCA compliance logs

4. Why did you choose the particular structure?

This structure will balance the need to store a large amount of data while providing the ability to quickly retrieve results

---

# Module 5: Fraud Detection
*By: Samiha Fansur*

Recommended database architecture:

Primary Recommendation: A Multi-Database Approach

Apache Cassandra (Time-series data)

For employee access patterns

Why:

- Excellent for time-series data
- Handles high-velocity writes
- Linear scalability for 1B+ data points
- Built-in timestamp handling
- Strong performance for time-based queries

Neo4j (Graph Database)

For dark web scraping feeds

Why:
- Native graph storage for relationship analysis
- Efficient pattern matching
- Cypher query language for complex relationship queries
- Good for detecting fraud patterns and networks
- Built-in graph algorithms

PostgreSQL (RDBMS)

For trade reconciliation logs

Why:

- ACID compliance for financial data
- Strong data integrity
- Complex JOIN operations
- Mature ecosystem for financial systems
- Built-in JSON support for flexibility

Integration Layer:

1. Apache Kafka for real-time data streaming

2. Apache Spark for cross-database analytics

Why Not Single Database:

- Different data types need specialized handling
- Real-time requirements need distributed processing
- Complex relationships need graph capabilities
- Time-series data needs optimized storage

This architecture allows:

- Real-time anomaly detection across all data sources
- Scalable processing of 1B+ data points
- Flexible integration of different data types
- Quick alert generation for suspicious patterns
- Historical analysis capabilities

