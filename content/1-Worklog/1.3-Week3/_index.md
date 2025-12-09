---
title: "Week 3 Worklog"
date: 2025-09-10
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---

### Week 3 Objectives:
* Understand advanced AWS storage services: S3, Storage Gateway, AWS Backup, VM Import/Export, Amazon FSx.
* Practice hybrid storage integration between on-premises and AWS.
* Learn how to host and manage static websites on Amazon S3.
* Gain hands-on experience with backup automation and VM migration workflows.
* Implement shared Windows file storage using Amazon FSx.

### Tasks to carry out this week:
| Day | Tasks | Start Date | Completion Date | Reference Material |
| --- | ----- | ---------- | ---------------- | ----------- |
| 2 | - Completed Module 4 theory: <br> &emsp; + S3 concepts <br> &emsp; + Storage Classes (Standard, IA, Intelligent-Tiering, One Zone IA, Glacier) <br> &emsp; + CORS in S3 <br> &emsp; + Versioning <br> &emsp; + Object Key & Performance <br> &emsp; + Snow Family <br> &emsp; + Storage Gateway <br> &emsp; + AWS Backup | 22/9/2025 | 22/9/2025 | AWS Docs |
| 3 | - Completed Lab 13 (AWS Backup): <br> &emsp; + Create backup vault <br> &emsp; + Create backup plan <br> &emsp; + Assign resources <br> &emsp; + Run backup jobs <br> &emsp; + Restore resources <br> &emsp; + Configure SNS notifications <br><br> - Completed Lab 14 (VM Import/Export): <br> &emsp; + Prepare VM OVA/OVF/VMDK <br> &emsp; + Upload to S3 <br> &emsp; + Create `vmimport` role <br> &emsp; + Import VM → AMI <br> &emsp; + Launch EC2 from AMI <br> &emsp; + Export instance if needed | 23/9/2025 | 23/9/2025 | AWS Docs |
| 4 | - Completed Lab 24 (File Storage Gateway): <br> &emsp; + Create & activate Storage Gateway <br> &emsp; + Connect S3 bucket as backend <br> &emsp; + Create NFS/SMB file share <br> &emsp; + Install Storage Gateway client on on-prem machine <br> &emsp; + Mount file share <br> &emsp; + Test file sync | 24/9/2025 | 24/9/2025 | AWS Docs |
| 5 | - Completed Lab 57 (Amazon S3 Static Website): <br> &emsp; + Create S3 bucket <br> &emsp; + Enable Static Website Hosting <br> &emsp; + Disable Block Public Access (controlled) <br> &emsp; + Add Bucket Policy for public read <br> &emsp; + Upload website files <br> &emsp; + Test website endpoint <br> &emsp; + Enable Transfer Acceleration <br> &emsp; + Enable Versioning <br> &emsp; + Copy/Move objects <br> &emsp; + Replicate objects cross-region <br> &emsp; + Clean up resources | 25/9/2025 | 25/9/2025 | AWS Docs |
| 6 | - Completed Lab 25 (Amazon FSx for Windows): <br> &emsp; + Prepare Windows environment & VPC <br> &emsp; + Create FSx file system <br> &emsp; + Connect via SMB <br> &emsp; + Map network drive <br> &emsp; + Create/read/write files <br> &emsp; + Run performance tests <br> &emsp; + Enable Data Deduplication <br> &emsp; + Enable Shadow Copy <br> &emsp; + Manage user sessions & file locks <br> &emsp; + Apply User Quota <br> &emsp; + Enable Continuous Access <br> &emsp; + Increase throughput capacity <br> &emsp; + Expand storage capacity <br> &emsp; + Clean up FSx resources | 26/9/2025 | 26/9/2025 | AWS Docs |

###  Week 3 Achievements:

* Gained strong understanding of advanced S3 features:
  * Storage classes, versioning, CORS, performance optimization.
  * Hybrid data transfer options via Snow Family.

* Completed AWS Backup automation workflow:
  * Backup vault, plan, lifecycle, SNS notification, restore.

* Understood full VM migration cycle using VM Import/Export:
  * Preparing VM images, uploading to S3, importing to AMI, exporting back.

* Successfully deployed File Storage Gateway:
  * Hybrid NFS/SMB sharing between on-premises and AWS S3.

* Built and optimized a static website hosted on S3:
  * Public access control, versioning, acceleration, replication.

* Implemented FSx for Windows as shared storage:
  * SMB file sharing, deduplication, shadow copy, quotas, continuous access.

* Strengthened knowledge about hybrid storage, backup strategies, and enterprise-grade file systems on AWS.

---

