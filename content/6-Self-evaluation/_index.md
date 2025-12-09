---
title: "Self-Assessment"
date: 2025-09-10
weight: 6
chapter: false
pre: " <b> 6. </b> "
---


During my internship at **First Cloud Journey (FCJ)** from **September 8, 2025** to **December 7, 2025**, I had the opportunity to learn, practice, and apply AWS Cloud knowledge in a real-world working environment.

I participated in **designing and developing an AI Chatbot system using Amazon Bedrock, Lambda, RDS PostgreSQL, DynamoDB, and other AWS services**, through which I improved my skills in **full-stack development with AWS CDK, prompt engineering, AI system architecture, data processing, and cloud cost optimization**.

**AI and Machine Learning Knowledge Applied:**
* **Amazon Bedrock & Large Language Models (LLM):** Used Claude 3 Haiku and Claude 3.5 Sonnet to build intelligent conversational chatbot, processing Vietnamese natural language.
* **Prompt Engineering:** Designed and optimized specialized prompts for intent classification, information extraction, SQL query generation, and context-aware responses. Applied Few-shot Learning and Reflection technique to improve accuracy.
* **Vector Search & Embeddings:** Used embedding models to convert text to vectors, built schema search mechanism and question caching based on cosine similarity.
* **Retrieval-Augmented Generation (RAG):** Researched and applied RAG architecture combining Amazon Kendra, LangChain agent, and knowledge base for chatbot to answer based on enterprise data sources.
* **Text-to-SQL Generation:** Built pipeline to convert natural language questions to SQL queries, combining context awareness and schema annotation to increase accuracy.
* **Session Management & Context Window:** Designed conversation context management mechanism with Rolling Summary, token limitation, and caching to optimize LLM API costs.
* **Model Selection & Cross-Region Inference:** Compared and selected appropriate models (Haiku vs Sonnet), balancing quality and latency when using cross-region.

**Important AWS Foundation Knowledge:**
* **Compute & Serverless:** Lambda, API Gateway, EventBridge, SQS - building event-driven architecture and handling throttling/timeout.
* **Database:** RDS PostgreSQL (ACID, transaction, unaccent extension), DynamoDB (NoSQL, session storage), Vector Search.
* **Storage:** S3 (static website, lifecycle, versioning), Storage Gateway, FSx.
* **Networking:** VPC, Subnet, Security Group, NAT Gateway, Transit Gateway, Site-to-Site VPN, Route 53 Resolver.
* **Security & IAM:** IAM User/Role/Policy, Permission Boundary, KMS encryption, Security Hub, Cognito, Organizations, Identity Center.
* **Infrastructure as Code:** AWS CDK (TypeScript) to deploy entire stack: Text2SQL, Webhook, Database, Networking following decoupling model.
* **Monitoring & Cost Optimization:** CloudWatch, Budget, Cost Explorer, auto start/stop EC2, reducing unnecessary VPC Endpoints.
* **Data Analytics:** Data Lake, Athena, Glue, QuickSight, Redshift, ElastiCache.

**Valuable Experience and Lessons:**

The FCJ internship program not only equipped me with technical knowledge but also provided invaluable real-world experiences:

* **Professional Work Environment:** Experienced technology enterprise standard work culture, understood product development process from research, design, development to deployment and monitoring. Learned to work with project management tools, version control (Git), documentation (Notion), and best practices in team collaboration.

* **Real-World Perspective on Cloud Architecture:** Gained clearer understanding of how real enterprise projects are deployed on AWS - from selecting appropriate services, designing scalable and cost-effective architecture, handling production issues like throttling/timeout/security, to optimizing performance and monitoring systems. Understood the difference between "doing labs" and "doing real projects" - where multiple factors must be considered such as business logic, user experience, cost, security, and maintainability.

* **Learning from Community:** Learned from talented peers in the program - each person had their own strengths in frontend, backend, DevOps, or AI/ML. Code review, architecture discussions, and pair programming helped broaden thinking and learn different approaches to the same problem.

* **Mentorship from Experienced Professionals:** Received dedicated guidance from mentors on technical skills, design thinking, and problem-solving approach. Questions like "why choose this solution?", "is there a better way?", "what if we scale to 1000x users?" helped me think deeper and avoid common mistakes. Learned to read documentation effectively, debug systematically, and most importantly the "always learning" mindset in technology.

* **Soft Skills:** Improved ability to present ideas, write proposals, conduct demos, and receive constructive feedback. Learned time management when working on multiple tasks in parallel and handling pressure when encountering critical bugs before deadlines.

In terms of work ethic, I always strived to complete tasks well, proactively researched new technologies, and actively engaged with colleagues to improve work efficiency.

To objectively reflect on my internship period, I would like to evaluate myself based on the following criteria:

| No. | Criteria                            | Description                                                                                      | Good | Fair | Average |
| --- | ----------------------------------- | ------------------------------------------------------------------------------------------------ | ---- | ---- | ------- |
| 1   | **Professional knowledge & skills** | Understanding of the field, applying knowledge in practice, proficiency with tools, work quality | ✅    | ☐    | ☐       |
| 2   | **Ability to learn**                | Ability to absorb new knowledge and learn quickly                                                | ☐    | ✅    | ☐       |
| 3   | **Proactiveness**                   | Taking initiative, seeking out tasks without waiting for instructions                            | ✅    | ☐    | ☐       |
| 4   | **Sense of responsibility**         | Completing tasks on time and ensuring quality                                                    | ✅    | ☐    | ☐       |
| 5   | **Discipline**                      | Adhering to schedules, rules, and work processes                                                 | ☐    | ✅    | ☐       |
| 6   | **Progressive mindset**             | Willingness to receive feedback and improve oneself                                              | ☐    | ✅    | ☐       |
| 7   | **Communication**                   | Presenting ideas and reporting work clearly                                                      | ☐    | ✅    | ☐       |
| 8   | **Teamwork**                        | Working effectively with colleagues and participating in teams                                   | ✅    | ☐    | ☐       |
| 9   | **Professional conduct**            | Respecting colleagues, partners, and the work environment                                        | ✅    | ☐    | ☐       |
| 10  | **Problem-solving skills**          | Identifying problems, proposing solutions, and showing creativity                                | ✅    | ☐    | ☐       |
| 11  | **Contribution to project/team**    | Work effectiveness, innovative ideas, recognition from the team                                  | ✅    | ☐    | ☐       |
| 12  | **Overall**                         | General evaluation of the entire internship period                                               | ✅    | ☐    | ☐       |

### Areas for Improvement

* **Discipline and Time Management:** Strengthen adherence to regulations, work schedules, and project deadlines.
* **Problem-Solving Mindset:** Improve ability to analyze complex problems, break down large tasks into smaller steps, and deliver optimal solutions quickly.
* **Communication Skills:** Learn to present ideas more clearly, proactively report progress, and handle difficult situations in teamwork professionally.

### Important Lessons from AI Chatbot Project

* **Model temperature significantly impacts accuracy** of information extraction - requires careful adjustment for each use case.
* **Combining multiple prompts into one** reduces API calls, increases consistency, and saves costs.
* **Vector search requires careful fine-tuning** with annotations and similarity thresholds to achieve optimal results.
* **Cross-region inference is a trade-off** between model quality and latency - requires balancing based on actual requirements.
* **SQS is an effective solution** for throttling and timeout issues in serverless architecture.
* **Vietnamese text processing requires unaccent extension** in PostgreSQL for accurate accent-insensitive search.
* **Business logic constraints are crucial** to prevent invalid data and ensure data integrity.
* **Decoupling architecture** makes code easier to maintain, test, and scale - applying Service pattern to separate Session, Bedrock, Database, Messenger.
* **Context window management** determines cost and performance - Rolling Summary and cache strategy are key.
* **Prompt engineering is an art** requiring extensive experimentation and deep understanding of business logic - Few-shot Learning and Reflection technique significantly improve accuracy.
