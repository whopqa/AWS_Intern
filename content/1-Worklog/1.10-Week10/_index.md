---
title: "Week 10 Worklog"
date: 2025-09-10
weight: 2
chapter: false
pre: " <b> 1.10. </b> "
---
### Week 10 Objectives:

* Explore CDK and AWS CLI to prepare for infrastructure development.
* Refine the overall system architecture and renumber all data flows.
* Assign tasks within the team and define module ownership.
* Start implementing the core stacks: Text2SQL and Webhook.
* Research and integrate Facebook Messenger and Cognito authentication.

---

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ----- | ---------- | ---------------- | ------------------ |
| 2 | - Study AWS CDK and AWS CLI to prepare for infrastructure deployment | 11/10/2025 | 11/10/2025 | AWS Docs |
| 3 | - Team meeting & task assignment <br> - Refine and finalize the overall system architecture <br> - Renumber all architecture data flows | 11/11/2025 | 11/11/2025 | Internal Architecture Docs |
| 5 | - Draft infrastructure structure using the CDK model: <br>&emsp; + Stack modules (infrastructure deployment) <br>&emsp; + Service modules (backend logic) <br>&emsp; + Handler modules (event flow handling) <br> - Research deployment workflow for CDK infrastructure | 11/13/2025 | 11/13/2025 | AWS CDK Workshop |
| 6 | - Take responsibility for the User flow: handling interactions, consultation, appointment booking, and database writes <br> - Research secure & optimized DB operations <br> - Study methods to optimize booking flow <br> - Start implementing Text2SQL Stack & Webhook Stack <br> - **Text2SQL Stack:** Implement Lambda to process queries → convert to SQL → execute on PostgreSQL <br> - **Webhook Stack:** Implement Webhook Verification Lambda, API Gateway GET/POST, IAM Role permissions | 11/14/2025 | 11/14/2025 | Internal |
| 6 (continued) | - Deploy Messenger App on Facebook Developer <br> - Explore Cognito authentication via Facebook Provider | 11/14/2025 | 11/14/2025 | Facebook Developer, AWS Cognito |

---

### Week 10 Achievements:

* Gained solid understanding of CDK and AWS CLI fundamentals for infrastructure deployment.
* Completed refinement of the overall system architecture and renumbered all data flows clearly.
* Structured the infrastructure into three major module groups:
  * **Stack** – Deploy CDK resources (Lambda, API Gateway, RDS, IAM, …)
  * **Service** – Backend logic processing
  * **Handler** – Event/Lambda flow processing
* Began implementation of core system components:
  * **Text2SQL Stack** – Lambda for query → SQL transformation → execute on PostgreSQL
  * **Webhook Stack** – Lambda for Webhook/Facebook Signature verification, API Gateway GET/POST, IAM Role setup
* Redesigned the User flow: consultation, booking, safe & optimized DB operations.
* Researched methods to optimize booking scheduling and avoid conflicts.
* Deployed Facebook Messenger App and experimented with Cognito authentication via Facebook Provider.

