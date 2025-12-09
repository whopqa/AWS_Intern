---
title: "Worklog Tuần 5"
date: 2025-09-10
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---
###  Mục tiêu tuần 5:
* Hoàn thành toàn bộ nội dung lý thuyết Module 5: Shared Responsibility, IAM, Cognito, Organizations, Identity Center và KMS.
* Nắm chắc kiến thức nền tảng về Database: PK/FK, Index, Partition, Execution Plan, Log, Buffer.
* Hiểu mô hình Data Lake và cách sử dụng Athena, Glue, QuickSight cho phân tích dữ liệu.
* Thực hành triển khai Data Lake và ứng dụng sử dụng Amazon RDS.
* Nâng cao kỹ năng đọc — dịch tài liệu AWS thông qua Blog 3 của BMW.

---

### Các công việc triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2 | - Hoàn thành lý thuyết Module 5:<br>&emsp; + Shared Responsibility Model<br>&emsp; + IAM: Users, Roles, Policies<br>&emsp; + Cognito<br>&emsp; + Organizations + SCP<br>&emsp; + AWS Identity Center (SSO)<br>&emsp; + AWS KMS<br><br> - Dịch Blog 3: BMW – Giải pháp AI tạo sinh phân tích sự cố đám mây | 6/10/2025 | 6/10/2025 | https://docs.google.com/document/d/1HuxyNcXIRpHRY_IEPkBqbSQ4jgbWUMSoetDqe1IPd2o/edit?usp=sharing |
| 3 | - Tìm hiểu Database Concepts:<br>&emsp; + Database, Session<br>&emsp; + Primary Key, Foreign Key<br>&emsp; + Index, Partition<br>&emsp; + Execution Plan, DB Log, Buffer<br><br> - Phân biệt RDBMS vs NoSQL<br> - Ôn lại câu lệnh SQL cơ bản | 7/10/2025 | 7/10/2025 | RDS Docs |
| 4 | - Tìm hiểu các chủ đề Data Analytics:<br>&emsp; + Data Lake: lưu dữ liệu thô, phục vụ phân tích<br>&emsp; + Amazon Athena: truy vấn SQL trên S3<br>&emsp; + AWS Glue: ETL service<br>&emsp; + Amazon QuickSight: BI & Dashboard | 8/10/2025 | 8/10/2025 | Analytics Docs |
| 5 | - Hoàn thành Lab 35 – Data Lake on AWS | 9/10/2025 | 9/10/2025 | Data Lake Lab |
| 6 | - Hoàn thành Lab 05 – Triển khai ứng dụng dùng RDS:<br>&emsp; + Tạo VPC + Private Subnet<br>&emsp; + Tạo DB Subnet Group (≥ 2 AZ)<br>&emsp; + Tạo RDS Instance: engine, compute, storage, backup<br>&emsp; + Cấu hình bảo mật: Security Group, Parameter Group, Encryption (KMS)<br>&emsp; + Kết nối ứng dụng qua RDS Endpoint<br>&emsp; + Thiết lập HA & Scaling: Multi-AZ + Read Replicas<br>&emsp; + Monitoring bằng CloudWatch & Performance Insights<br>&emsp; + Test failover & tối ưu hiệu năng | 10/10/2025 | 10/10/2025 | RDS Lab |

---

###  Kết quả đạt được tuần 5:

#### **1. Hoàn thành toàn bộ nội dung lý thuyết Module 5**
* Hiểu rõ ranh giới trách nhiệm AWS – khách hàng.
* Nắm chắc IAM, Cognito, Organizations, Identity Center và vai trò của KMS.
* Hiểu mô hình SSO và bảo mật doanh nghiệp trên AWS.

#### **2. Thành thạo kiến thức nền tảng về Database**
* Hiểu PK/FK, Index, Partition và cách tối ưu truy vấn qua Execution Plan.
* Nắm cơ chế hoạt động của Log, Buffer và kiến trúc của RDBMS.
* Biết so sánh và chọn lựa giữa RDBMS vs NoSQL.
* Thành thạo lại các lệnh SQL cơ bản.

#### **3. Làm chủ kiến trúc Data Lake**
* Hiểu Data Lake và vai trò trong hệ thống phân tích dữ liệu.
* Sử dụng Athena để truy vấn dữ liệu thô trên S3.
* Dùng Glue để xử lý, ETL và quản lý metadata.
* Dùng QuickSight để trình bày và trực quan hóa dữ liệu.

#### **4. Hoàn thành 2 lab thực hành quan trọng**
* Lab 35: Xây dựng Data Lake từ đầu đến cuối.
* Lab 05: Triển khai ứng dụng kết nối RDS với HA, bảo mật và giám sát đầy đủ.

#### **5. Nâng cao khả năng đọc – dịch tài liệu chuyên ngành**
* Dịch Blog 3 của BMW, hiểu cách doanh nghiệp lớn dùng GenAI để xử lý sự cố cloud.

---

###  Tổng kết tuần 5:
Tuần 5 tập trung vào **bảo mật, danh tính, cơ sở dữ liệu và phân tích dữ liệu**, kết hợp lý thuyết và thực hành.  
Việc hoàn thành Module 5 + Data Lake + RDS triển khai giúp xây nền tảng vững chắc cho các hệ thống hiện đại trên AWS:  
**secure – scalable – data-driven**.
