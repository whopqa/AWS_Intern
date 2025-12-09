---
title: "Worklog Tuần 6"
date: 2025-09-10
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6:

* Hoàn thành toàn bộ lý thuyết Module 6 (Database Concepts, RDS/Aurora, Redshift, ElastiCache).
* Nghiên cứu kiến trúc AI chatbot trên AWS.
* Cài đặt và sử dụng Amazon Q CLI.
* Tham gia workshop Data Science on AWS.
* Bắt đầu phác thảo kiến trúc bằng Amazon Q CLI.

---

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2 | **Hoàn thành lý thuyết Module 6** <br> - Redshift: Data warehouse, OLAP, MPP, columnar storage <br> - ElastiCache: Redis/Memcached, giảm latency, session caching <br> - Database Concepts: OLTP vs OLAP, SQL vs NoSQL, ACID vs BASE, vertical/horizontal scaling, sharding, replication | 12/10/2025 | 12/10/2025 | AWS StudyGroup |
| 3 | **Cài đặt Amazon Q CLI trên VMWare** | 13/10/2025 | 13/10/2025 | AWS Docs |
| 4 | **Nghiên cứu blog và phân tích code** <br> - Đọc [“Building AI Chatbots using Amazon Lex & Amazon Kendra”](https://aws.amazon.com/vi/solutions/guidance/conversational-chatbots-using-retrieval-augmented-generation-on-aws/) và [“Guidance for Conversational Chatbots Using RAG on AWS”](https://builder.aws.com/content/2eBsTWhvFFPUtzh2secQlNRBgta/prototype-a-rag-chatbot-with-amazon-bedrock-kendra-and-lex) <br> - LangChain Agent + Kendra indexing <br> - Lưu session bằng DynamoDB <br> - RAG with Bedrock | 14/10/2025 | 14/10/2025 | AWS Blogs |
| 5 | **Tham gia Workshop:** “Data Science on AWS” <br> - Ghi chú các dịch vụ AWS hỗ trợ phân tích dữ liệu và dịch vụ AI/ML | 15/10/2025 | 15/10/2025 | Sự kiện AWS |
| 6 | **Vẽ sơ bộ kiến trúc bằng Amazon Q CLI** | 16/10/2025 | 16/10/2025 | [Pre-Architecture](https://www.notion.so/pre-archi-28fd23b23efb808b978dfb3f9a20389d?v=268d23b23efb8088ba76000ca96674ea) |

---

### Kết quả đạt được tuần 6:

* Hiểu rõ Module 6:
  * Redshift: OLAP, MPP, columnar storage, phù hợp BI & big data analytics.
  * ElastiCache: Redis/Memcached, caching session, giảm tải DB, tăng throughput.
  * Database Concepts: OLTP/OLAP, SQL/NoSQL, ACID vs BASE, scaling strategies.

* Cài đặt và thử nghiệm Amazon Q CLI:
  * Tạo project
  * Gọi lệnh generate diagram
  * Chạy các câu lệnh Q Builder cơ bản

* Nghiên cứu sâu kiến trúc chatbot AI trên AWS:
  * Lex làm conversational interface
  * Kendra indexing đa nguồn dữ liệu
  * LangChain agent workflow
  * DynamoDB lưu session
  * Bedrock dùng trong pipeline RAG

* Tham gia Workshop Data Science on AWS:
* Hiểu quy trình ETL → Transform → Load → ML Training → Deployment
* Nắm được các dịch vụ: S3, Glue, Redshift, Athena, SageMaker

* Vẽ được sơ bộ các kiến trúc đầu tiên với Amazon Q CLI:
  * Kiến trúc chatbot
  * Kiến trúc data pipeline
  * Kiến trúc RAG cơ bản trên AWS

