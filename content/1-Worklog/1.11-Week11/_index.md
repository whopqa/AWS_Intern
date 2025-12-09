---
title: "Week 11 Worklog"
date: 2025-09-10
weight: 2
chapter: false
pre: " <b> 1.11. </b> "
---

### Week 11 Objectives:

* Deploy and complete the Webhook Stack for Facebook Messenger integration.
* Develop business logic for both Admin and User sides.
* Optimize system architecture to reduce costs.
* Research Knowledge Distillation on Amazon Bedrock.
* Build a secure user authentication system with email-based OTP.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                   | Start Date | Completion Date | Reference Material |
| --- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ------------------ |
| 2   | - Continue developing Webhook Stack and Backend Webhook <br> - Perform database change operations at row level (by ID) <br> - Learn about Knowledge Distillation on Amazon Bedrock <br> - Attend Workshop event | 11/17/2025   | 11/17/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - Continue implementing User side <br> - Develop Admin side business logic <br> - Learn about Event mechanism on Lambda                                                                  | 11/18/2025   | 11/18/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Redesign Architecture to reduce costs <br>&emsp; + Admin retrieves data analytics from Lambda outside VPC <br>&emsp; + Use DDL/Athena instead of Glue Crawler <br> - Create Jira to manage project progress | 11/19/2025   | 11/19/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Deep dive into Cognito security management <br> - Evaluate the feasibility of applying Cognito to the system                                                                                         | 11/20/2025   | 11/20/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Successfully deploy Webhook Stack <br> - Create Messenger App on Facebook Developer Dashboard <br> - Configure Page Access Token and Webhook URL <br> - Set up permissions and subscriptions <br> - Debug and fix handler, authentication errors <br> - Verify Messenger connection with Lambda via API Gateway <br> - Switch to email-based OTP authentication (replacing Cognito) <br> - Implement AWS SES Service to send emails <br> - Build user authentication system with session management <br> - Integrate security mechanisms: <br>&emsp; + Rate limiting (block after 5 incorrect OTP attempts) <br>&emsp; + Session timeout (reset after 15 minutes) <br>&emsp; + OTP request throttling (11 seconds between requests) <br> - Add Usage Plan for API Gateway <br> - Verify Webhook and Facebook Signature | 11/21/2025   | 11/23/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Week 11 Achievements:

**Webhook Deployment and Facebook Messenger Integration:**
* Successfully deployed Webhook Stack connected to Facebook Messenger.
* Created and configured Messenger App on Facebook Developer Dashboard including:
  * Page Access Token
  * Webhook URL configuration
  * Subscription settings and permissions
* Understood and implemented important concepts:
  * **Page Token:** Authentication key to connect Messenger API
  * **Verify Token:** Key for Messenger to return information to API Gateway
  * **PSID (Page-Scoped ID):** Unique unchanging ID of each user for each page
* Successfully connected Messenger with Lambda via API Gateway, verified events on CloudWatch.

**Architecture and Cost Optimization:**
* Redesigned architecture to reduce costs:
  * Admin retrieves data analytics from Lambda outside VPC
  * Used DDL/Athena instead of Glue Crawler to save costs
* Performed database operations at row level (by ID) to optimize performance.
* Learned about Events mechanism on Lambda.

**Research and Learning:**
* Studied Knowledge Distillation on Amazon Bedrock.
* Deep dive into Cognito security management.
* Attended Workshop event to update new knowledge.

**Building Secure Authentication System:**
* Switched from Cognito to email-based OTP authentication system due to errors and complexity issues.
* Successfully implemented AWS SES Service to send OTP emails.
* Authenticated users and stored sessions in DynamoDB with basic fields.
* Integrated comprehensive security mechanisms:
  * **Rate Limiting:** Block account after 5 incorrect OTP attempts in a session
  * **Session Management:** Reset unverified user status after 15 minutes
  * **Request Throttling:** OTP requests spaced at least 11 seconds apart
  * **API Gateway Protection:** Added Usage Plan to control traffic
  * **Webhook Security:** Verified Facebook Signature to ensure legitimate requests

**Project Management:**
* Created Jira to systematically manage project progress.
* Developed business logic for both User and Admin sides.

**Technical Lessons Learned:**
* Understood the difference between Page Token and App Secret.
* Mastered JWT (JSON Web Token) mechanism and its role as security code for applications.
* Recognized the dynamic nature of information such as Webhook URL, Callback URL, User Pool ID, Client ID when deploying stack - need management measures to avoid changing code multiple times.
* Successfully debugged errors:
  * Handler not processing events (confused Page Token with App Secret)
  * Cognito login URL not working
* Stored Session data in DynamoDB with necessary user information fields.
