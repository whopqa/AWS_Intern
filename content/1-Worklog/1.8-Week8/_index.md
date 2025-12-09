---
title: "Week 8 Worklog"
date: 2025-09-10
weight: 1
chapter: false
pre: " <b> 1.8. </b> "
---
### Week 8 Objectives:

* Finalize the preliminary components and technologies to be used in the project.
* Review and improve the architecture and technology choices.
* Study AWS theory through videos and documentation.
* Systematize knowledge of core AWS services.
* Practice for AWS Practitioner & AWS SAA-C03 certifications.
* Complete the midterm exam 

---

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ----------- | ---------------- | ------------------ |
| 2 | **Finalize preliminary components & key technologies** <br> - Identify core services and modules <br> - Evaluate areas that need improvement | 27/10/2025 | 27/10/2025 | Internal project architecture |
| 3 | **Review AI/AWS theory videos on YouTube** <br>  | 28/10/2025 | 28/10/2025 |[YouTube: AWS Tutorials](https://www.youtube.com/watch?v=AQlsd0nWdZk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| 4 | **Systematize AWS knowledge** <br> - EC2, RDS, S3, IAM, Lambda, VPC <br> - Review using AI tools (ChatGPT/Claude) | 29/10/2025 | 29/10/2025 | AWS Docs |
| 5 | **Theory review & exam practice** <br> - [Quizlet: AWS Hotfix V10](https://quizlet.com/vn/1099628340/aws-hotfix-v10-flash-cards/?funnelUUID=e6969943-0cf6-481d-a9f1-72c54016d0c3) <br> - [Practice Exam AWS Practitioner](https://github.com/kananinirav/AWS-Certified-Cloud-Practitioner-Notes/blob/master/practice-exam/practice-exam-1.md) <br> - [Practice Exam AWS SAA-C03](https://github.com/Iamrushabhshahh/AWS-Certified-Solutions-Architect-Associate-SAA-C03-Exam-Dump-With-Solution/blob/main/AWS%20Certified%20Solutions%20Architect%20Associate%20SAA-C03.pdf)  | 30/10/2025 | 30/10/2025 | Quizlet, AWS Exam Guide |
| 6 | **Midterm exam** <br>- Select *Top 10 highest-scoring candidates (Round 1)*  | 31/10/2025 | 31/10/2025 | Internal exam results |

---

### Week 8 Achievements:

#### **1. Finalizing preliminary project components**
Identified the core AWS + AI services:

**1.1. RAG Module – in progress**
* Challenge: understanding & extracting Vietnamese intent.
* Solution: Lex → Lambda (acting as RAG) → DynamoDB.
* Intent = Customer Support → retrieve RAG from DynamoDB.
* Intent = Scheduling → call Bedrock to generate SQL.

**1.2. Scheduling Module**
* Challenge: safely executing insert/update/delete SQL queries on the appointment table.
* Tech stack: RDS + pgvector.
* Cost optimization: consider EventBridge to start/stop RDS.

**1.3. User UI Flow**
* Lex → Lambda → Amazon Translate → intent detection → RAG or Scheduling.

**1.4. Admin UI**
* Web dashboard (weekly/monthly/yearly analytics) → S3 + CloudFront + Route53 → admin-level DB actions.
* Combine Athena + Glue for analytics and reporting.

**1.5. Memory System (Cache) – DynamoDB**
* Stores: session history, RAG results, SQL results, Bedrock outputs.
* Implementation: Lambda trigger on DB changes → invalidate cache; TTL for auto-expiry (e.g., 1 hour).

**1.6. Storage**
* Periodically archive appointment data to S3 for analytics/revenue tracking.

---

#### **2. Technical review & improvements**
* Documented optimization points before building.
* Evaluated all architecture and technology decisions.

---

#### **3. AWS Services Review**
* Strengthened understanding of EC2, RDS, IAM, S3, Networking.
* Used AI to reinforce key concepts.

---

#### **4. AWS Certification Practice**
* Completed Quizlet Hotfix V10.
* Practiced AWS Practitioner and SAA-C03 exams.

---

#### **5. Midterm Exam**
* Completed the exam.
* Made it into the Top 10 highest-scoring candidates (Round 1).

---

### Week 8 Summary:
Week 8 focused on **refining the project architecture and reviewing AWS fundamentals**.  
The main modules (RAG, Scheduling, UI, Cache, Storage) and their associated technologies were clearly identified.  
At the same time, AWS knowledge was reinforced through exam practice, achieving solid results in the midterm assessment.