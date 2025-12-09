---
title: "Week 9 Worklog"
date: 2025-09-10
weight: 1
chapter: false
pre: " <b> 1.9. </b> "
---
### Week 9 Objectives:

* Finalize and align the overall system architecture.
* Evaluate technology selections: Lex, Translate, Bedrock, Webhook.
* Optimize system cost and deployment model.
* Standardize the proposal: problem statement, components, dataflow.
* Submit Proposal – Phase 1.

---

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ----- | ----------- | ---------------- | ------------------ |
| 2 | - Team meeting on the updated project approach <br> - Proposed switching from Amazon Lex + Translate to Custom Webhook + Bedrock Claude <br> - Reason: Lex does not support Vietnamese, Claude handles Vietnamese much better | 11/03/2025 | 11/03/2025 | Internal Documentation |
| 3 | - Finalize the overall system architecture on draw.io <br> - Upload the architecture diagram to Google Drive | 11/04/2025 | 11/04/2025 | [Proposal, Architecture](https://drive.google.com/drive/u/0/folders/1gkahOsw673lZPGN3CNM1mr5l34ZpCcOt) |
| 4 | - Continue improving the architecture <br>&emsp; + Reduce unnecessary VPC Endpoints to optimize cost <br>&emsp; + Organize Lambda functions based on security & performance requirements (inside/outside VPC) <br>&emsp; + Number and standardize all dataflows | 11/05/2025 | 11/05/2025 | [Proposal, Architecture](https://drive.google.com/drive/u/0/folders/1gkahOsw673lZPGN3CNM1mr5l34ZpCcOt) |
| 5 | - Calculate pricing for the entire system <br> - Review and refine the Proposal: <br>&emsp; + Problem objectives <br>&emsp; + Main system components & their roles <br>&emsp; + Explanation of the dataflow | 11/06/2025 | 11/06/2025 | AWS Pricing |
| 6 | - Finalize the Proposal <br> - Submit Proposal – Phase 1 | 11/07/2025 | 11/07/2025 | [Proposal, Architecture](https://drive.google.com/drive/u/0/folders/1gkahOsw673lZPGN3CNM1mr5l34ZpCcOt) |

---

### Week 9 Achievements:

* **Aligned on the new technical approach:**  
  - Removed Lex + Translate from the architecture.  
  - Switched to Custom Webhook + Bedrock Claude for Vietnamese conversational workflows.  
  - Simplified the pipeline and improved response accuracy.

* **Completed the overall system architecture:**  
  - Updated the entire flow: Webhook → Bedrock → Lambda → Database.  
  - Optimized Lambda placement (inside or outside VPC).  
  - Numbered and standardized all data pipelines.

* **Cost optimization:**  
  - Reduced unnecessary VPC Endpoints.  
  - Reviewed projected cost for RDS, S3, Lambda, Bedrock, API Gateway.

* **Pricing calculation & cost report created.**

* **Completed Proposal – Phase 1:**  
  - Clear and well-defined problem objectives.  
  - Detailed description of system components and roles.  
  - Updated and standardized dataflow explanation.  
  - Reformatted and finalized content for the team submission.

---