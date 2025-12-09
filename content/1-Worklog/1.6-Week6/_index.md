---
title: "Week 6 Worklog"
date: 2025-09-10
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---
### Week 6 Objectives:

* Complete all theory content in Module 6 (Database Concepts, RDS/Aurora, Redshift, ElastiCache).
* Research AI chatbot architecture on AWS.
* Install and use Amazon Q CLI.
* Attend the “Data Science on AWS” workshop.
* Start drafting cloud architectures using Amazon Q CLI.

---

### Tasks to carry out this week:

| Day | Tasks | Start Date | Completion Date | References Meterial |
| --- | ------ | ----------- | ---------------- | ----------- |
| 2 | **Complete Module 6 theory** <br> - Redshift: Data warehouse, OLAP, MPP, columnar storage <br> - ElastiCache: Redis/Memcached, reduce latency, session caching <br> - Database Concepts: OLTP vs OLAP, SQL vs NoSQL, ACID vs BASE, vertical/horizontal scaling, sharding, replication | 12/10/2025 | 12/10/2025 | AWS StudyGroup |
| 3 | **Install Amazon Q CLI on VMWare** | 13/10/2025 | 13/10/2025 | AWS Docs |
| 4 | **Research blogs and analyze code** <br> - Read [“Building AI Chatbots using Amazon Lex & Amazon Kendra”](https://aws.amazon.com/vi/solutions/guidance/conversational-chatbots-using-retrieval-augmented-generation-on-aws/) and [“Guidance for Conversational Chatbots Using RAG on AWS”](https://builder.aws.com/content/2eBsTWhvFFPUtzh2secQlNRBgta/prototype-a-rag-chatbot-with-amazon-bedrock-kendra-and-lex) <br> - LangChain Agent + Kendra indexing <br> - Store session data using DynamoDB <br> - RAG with Bedrock | 14/10/2025 | 14/10/2025 | AWS Blogs |
| 5 | **Attend Workshop:** “Data Science on AWS” <br> - Take notes on data analytics services, and AI/ML services | 15/10/2025 | 15/10/2025 | AWS Event |
| 6 | **Draft initial architecture diagrams using Amazon Q CLI** | 16/10/2025 | 16/10/2025 | [Pre-Architecture](https://www.notion.so/pre-archi-28fd23b23efb808b978dfb3f9a20389d?v=268d23b23efb8088ba76000ca96674ea)|

---

### Week 6 Achievements:

* Gained strong understanding of Module 6:
  * Redshift: OLAP, MPP, columnar storage, suitable for BI & big data analytics.
  * ElastiCache: Redis/Memcached, caching sessions, offloading DB load, increasing throughput.
  * Database Concepts: OLTP/OLAP, SQL/NoSQL, ACID vs BASE, scaling strategies.

* Installed and tested Amazon Q CLI:
  * Created Q CLI projects
  * Generated architecture diagrams
  * Executed basic Q Builder commands

* Conducted deep research on AI chatbot architecture on AWS:
  * Amazon Lex for conversational interface
  * Kendra for multi-source data indexing
  * LangChain agent workflow
  * DynamoDB for session storage
  * Bedrock for RAG pipelines

* Attended Data Science on AWS Workshop:
* Learned full ETL → Transform → Load → ML Training → Deployment pipeline
* Understood key AWS data and ML services: S3, Glue, Redshift, Athena, SageMaker

* Drafted initial cloud architectures using Amazon Q CLI:
  * Chatbot architecture
  * Data pipeline architecture
  * Basic RAG architecture on AWS
