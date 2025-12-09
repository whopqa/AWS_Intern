---
title: "Week 7 Worklog"
date: 2025-09-10
weight: 1
chapter: false
pre: " <b> 1.7. </b> "
---
### Week 7 Objectives:

* Read and analyze AI-related blogs on AWS.
* Select an architectural baseline from an AWS blog to develop the chatbot.
* Build the initial project direction for the chatbot.
* Deploy and test the sample Text-to-SQL Chatbot.
* Conduct team meeting and summarize optimization strategies (cache, RBAC, scaling, etc.).

---

### Tasks to carry out this week:

| Day | Tasks | Start Date | Completion Date | Reference Material |
| --- | ----- | ---------- | ----------- | ----------- |
| 2 | **Read & review AI blogs** <br> - AWS Knowledge Hub <br> - Summarize AI knowledge & best practices | 20/10/2025 | 20/10/2025 | [AWS Knowledge Hub](https://www.notion.so/268d23b23efb808a8805c570231cefa9?v=268d23b23efb8088ba76000ca96674ea&source=copy_link) |
| 3 | **Select baseline blog:** <br> - [“Build an AI-powered Text-to-SQL Chatbot”](https://aws.amazon.com/vi/blogs/database/build-an-ai-powered-text-to-sql-chatbot-using-amazon-bedrock-amazon-memorydb-and-amazon-rds/?utm_source=chatgpt.com) <br> - Study code, architecture, workflow <br> - Analyze technologies: Bedrock, Aurora, SQL generation | 21/10/2025 | 21/10/2025 | [AWS Blog](https://aws.amazon.com/vi/blogs/database/build-an-ai-powered-text-to-sql-chatbot-using-amazon-bedrock-amazon-memorydb-and-amazon-rds/?utm_source=chatgpt.com) |
| 4 | **Create initial chatbot Direction** <br> - Write Direction document on Notion <br> - Define pipeline, roles, architecture, bot limitations <br> - Specify interaction rules | 22/10/2025 | 22/10/2025 | [Direction](https://www.notion.so/Directions-295d23b23efb80bb9500e5cb3222414c?v=268d23b23efb8088ba76000ca96674ea&source=copy_link) |
| 5 | **Deploy sample blog project:** “Build an AI-powered Text-to-SQL Chatbot” <br> - Run end-to-end tests <br> - Document issues & optimization ideas | 23/10/2025 | 23/10/2025 |[AWS Blog](https://aws.amazon.com/vi/blogs/database/build-an-ai-powered-text-to-sql-chatbot-using-amazon-bedrock-amazon-memorydb-and-amazon-rds/?utm_source=chatgpt.com) |
| 6 | **Team meeting & notes on Notion** <br> **Meeting agenda includes:** <br> 1. Caching mechanism & bot optimization <br> 2. RBAC access control design <br> 3. Data flow RDS → S3 archive <br> 4. Scaling: RDS, UI, Lex + Translate | 24/10/2025 | 24/10/2025 | [Internal Meeting](https://www.notion.so/NOTE-h-p-298d23b23efb8072a6a3e1f67d5c640a?source=copy_link) |

---

### Week 7 Achievements:

* **Reviewed AWS Knowledge Hub:**  
  - Summarized common AI chatbot workflows.  
  - Noted key AWS services: Bedrock, RDS, S3, caching layer.

* **Selected baseline from “Build an AI-powered Text-to-SQL Chatbot”:**  
  - Understood the Text-to-SQL architecture.  
  - Captured pipeline: embedding → SQL generation → execution.

* **Completed Direction document on Notion:**  
  - Defined feature scope.  
  - Established strategies to prevent incorrect bot actions.  
  - Designed role-based flow: member / consultant.  
  - Set safe rules for SELECT/UPDATE/DELETE.

* **Successfully deployed the sample model:**  
  - Performed real-world testing.  
  - Documented improvement points.

* **Meeting summary:**

  **1. Cache & bot optimization**  
  - Cache frequent questions to reduce database load.  
  - Prevent bot from having unrestricted modification permissions.

  **2. RBAC – Access control & security**  
  - Bot operates using credentials tied to user role.  
  - SELECT allowed broadly; UPDATE/DELETE requires strict role & logic checks.

  **3. Data flow & storage**  
  - Archive RDS data to S3 for analytics and dashboards.

  **4. Scaling**  
  - RDS: read replicas, Multi-AZ, autoscaling.  
  - UI scaling.  
  - Lex + Translate for Vietnamese support (Translate free 2M characters/month in the first year).
