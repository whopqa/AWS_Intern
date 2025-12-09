---
title: "Week 4 Worklog"
date: 2025-09-10
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---
### Week 4 Objectives:
* Gain solid knowledge of IAM, Shared Responsibility Model, Organizations, Identity Center, KMS, and Security Hub.
* Deeply understand user/group management, policies, roles, permission boundaries, and IAM conditions.
* Complete hands-on labs related to access control, permission restriction, EC2 IAM roles, and AWS account security.
* Strengthen operational security skills: Security Hub, CloudTrail, KMS encryption, and Lambda automation.

---

### Tasks to carry out this week:
| Day | Tasks | Start Date | Completion Date | Reference Material |
| --- | ------ | ---------- | -------- | --------- |
| Mon | - Completed Lab 02 – IAM User & Group:<br>&emsp; + Create Users, Groups, attach policies<br>&emsp; + Practice Switch Role & temporary permissions<br><br> - Completed Lab 44:<br>&emsp; + Create Groups and attach IAM Policies<br>&emsp; + Create Users, assign policy & Access Key<br>&emsp; + Configure IAM Role & Conditions (IP, encryption, time-based) | 29/09/2025 | 29/09/2025 | IAM Labs |
| Tue | - Completed Module 4 theory:<br>&emsp; + Shared Responsibility Model<br>&emsp; + IAM Users, Roles, Policies<br>&emsp; + Cognito for identity management<br>&emsp; + AWS Organizations & SCP<br>&emsp; + IAM Identity Center (SSO)<br>&emsp; + KMS Encryption & Key Management<br>&emsp; + Security Hub fundamentals | 30/09/2025 | 30/09/2025 | AWS Academy Module 4 |
| Wed | - Completed Lab 48 – EC2 with IAM Role:<br>&emsp; + Attach IAM Role to EC2<br>&emsp; + EC2 receives temporary credentials via STS<br>&emsp; + App accesses S3 without Access Keys<br><br> - Completed Lab 30 – Permission Boundary:<br>&emsp; + Create boundary policy<br>&emsp; + Create restricted IAM user<br>&emsp; + Validate restricted access<br><br> - Completed Lab 28 – EC2 Tag-based Permissions:<br>&emsp; + Restrict EC2 access using Resource Tags<br>&emsp; + Create EC2 Admin role<br>&emsp; + Validate tag-based access control<br><br> - Completed Lab 18 – Security Hub:<br>&emsp; + Enable Security Hub<br>&emsp; + Review CIS/AWS compliance results<br>&emsp; + Analyze GuardDuty/Inspector/Macie findings | 01/10/2025 | 01/10/2025 | IAM & Security Labs |
| Thu | - Lab 22 – Lambda auto start/stop EC2 for cost optimization<br>&emsp; + Create Lambda function<br>&emsp; + Attach EventBridge Scheduler<br><br> - Lab 33 – S3 Encryption + KMS:<br>&emsp; + Enable KMS CMK encryption for S3<br>&emsp; + CloudTrail logs for key usage<br>&emsp; + Query data using Athena<br><br> - Lab 12 – IAM Identity Center:<br>&emsp; + Manage SSO for multi-account setup<br>&emsp; + Assign least-privilege roles<br>&emsp; + Apply Zero Trust access model | 02/10/2025 | 02/10/2025 | AWS Security Workshops |
| Fri | - Translated Blog 1: Improve cloud budget accuracy with AWS Budgets new features<br> - Translated Blog 2: Increase engagement with localized content using Amazon Bedrock Flows | 03/10/2025 | 03/10/2025 | AWS Blog |

---

### Week 4 Achievements:

#### **1. Completed all Module 4 theory**
* Clearly understand the Shared Responsibility Model.
* Master IAM Users, Groups, Policies, Roles, and access control mechanisms.
* Understand how Organizations, SCP, and Identity Center manage multi-account environments.
* Learn how KMS manages encryption keys across AWS services.
* Understand Security Hub and its compliance standards (CIS, AWS best practices).

#### **2. Completed 8 critical labs on IAM, EC2, and Security**
* Fully mastered User/Group/Policy management and access control.
* Know how to attach IAM Roles to EC2 and use STS temporary credentials securely.
* Apply Permission Boundaries to prevent privilege escalation.
* Enforce EC2 access control through Resource Tags.
* Enable and analyze Security Hub findings for compliance and security posture.

#### **3. Cost optimization & data security**
* Automate EC2 start/stop using Lambda + EventBridge to reduce costs.
* Enable S3 encryption using KMS and audit key usage through CloudTrail.
* Query S3 data securely with Athena without downloading raw files.

#### **4. Master AWS Identity Center**
* Manage SSO across multiple AWS accounts.
* Implement least privilege and Zero Trust principles.
* Centralize authentication & authorization for better governance.

#### **5. Completed translations of 2 AWS blogs**
* Deep understanding of AWS Budgets enhancements.
* Understand how Bedrock Flows boost localized content engagement.

---

### Summary of Week 4:
Week 4 focuses on **security, access management, and cost optimization**, especially around IAM, Security Hub, KMS, and Lambda automation.  
Completed all theory and advanced labs, building a strong foundation for enterprise-level AWS operations and governance.

