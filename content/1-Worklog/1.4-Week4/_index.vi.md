---
title: "Worklog Tuần 4"
date: 2025-09-10
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---
### Mục tiêu tuần 4:
* Nắm chắc lý thuyết về IAM, Shared Responsibility Model, Organizations, Identity Center, KMS và Security Hub.
* Hiểu sâu cách quản lý người dùng, nhóm, policy, role, permission boundary và IAM condition.
* Thực hành chuỗi lab liên quan đến quản lý quyền truy cập, giới hạn quyền, gắn role vào EC2 và bảo mật tài khoản AWS.
* Tăng cường kỹ năng vận hành bảo mật: Security Hub, CloudTrail, KMS encryption, Lambda automation.

---

### Các công việc triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2 | - Hoàn thành Lab 02 – IAM User & Group:<br>&emsp; + Tạo User, Group, gán policy theo nhóm<br>&emsp; + Thực hành Switch Role & cấp quyền tạm thời<br><br> - Hoàn thành Lab 44:<br>&emsp; + Tạo Group và gán IAM Policy<br>&emsp; + Tạo User, gán policy & Access Key<br>&emsp; + Cấu hình IAM Role & Condition (IP, encryption, time-based) | 29/9/2025 | 29/9/2025 | IAM Labs |
| 3 | - Hoàn thành lý thuyết Module 4:<br>&emsp; + Shared Responsibility Model<br>&emsp; + IAM Users, Roles, Policies<br>&emsp; + Cognito identity management<br>&emsp; + AWS Organizations & SCP<br>&emsp; + IAM Identity Center (SSO)<br>&emsp; + KMS Encryption & Key Management<br>&emsp; + AWS Security Hub tổng quan | 30/9/2025 | 30/9/2025 | AWS Academy Module 4 |
| 4 | - Hoàn thành Lab 48 – EC2 with IAM Role:<br>&emsp; + Gắn IAM Role vào EC2<br>&emsp; + EC2 nhận temporary credentials từ STS<br>&emsp; + Ứng dụng truy cập S3 không cần Access Key<br><br> - Hoàn thành Lab 30 – IAM Permission Boundary:<br>&emsp; + Tạo boundary policy<br>&emsp; + Tạo user bị giới hạn<br>&emsp; + Kiểm tra giới hạn quyền<br><br> - Hoàn thành Lab 28 – EC2 Tag-based Permissions:<br>&emsp; + Giới hạn EC2 dựa trên Resource Tag<br>&emsp; + Tạo role dành cho EC2 Admin<br>&emsp; + Kiểm tra quyền theo tag<br><br> - Hoàn thành Lab 18 – Security Hub:<br>&emsp; + Kích hoạt Security Hub<br>&emsp; + Kiểm tra tuân thủ CIS/AWS<br>&emsp; + Tổng hợp cảnh báo GuardDuty/Inspector/Macie | 1/10/2025 | 1/10/2025 | IAM & Security Labs |
| 5 | - Lab 22 – Lambda auto start/stop EC2 để tiết kiệm chi phí<br>&emsp; + Tạo Lambda function<br>&emsp; + Gán EventBridge Scheduler<br><br> - Lab 33 – S3 Encryption + KMS:<br>&emsp; + Mã hóa S3 bằng KMS CMK<br>&emsp; + CloudTrail log key usage<br>&emsp; + Query bằng Athena<br><br> - Lab 12 – AWS IAM Identity Center:<br>&emsp; + Quản lý SSO cho multi-account<br>&emsp; + Gán quyền least privilege theo role<br>&emsp; + Zero Trust access model | 2/10/2025 | 2/10/2025 | AWS Security Workshops |
| 6 | - Dịch blog 1: AWS Budgets – cải thiện độ chính xác ngân sách cloud<br> - Dịch blog 2: Amazon Bedrock Flows – tăng tương tác nội dung bản địa hóa | 3/10/2025 | 3/10/2025 | AWS Blog |

---

### Kết quả đạt được tuần 4:

#### **1. Hoàn thành toàn bộ lý thuyết Module 4**
* Nắm rõ mô hình trách nhiệm chia sẻ giữa AWS và khách hàng.
* Thành thạo IAM Users, Groups, Policies, Roles và các cơ chế cấp quyền.
* Hiểu vai trò của Organizations, SCP, Identity Center trong multi-account.
* Nắm cơ chế mã hóa và quản lý khóa bằng AWS KMS.
* Có cái nhìn tổng quan về Security Hub và các tiêu chuẩn CIS.

#### **2. Hoàn thành 8 lab quan trọng về IAM, EC2 và Security**
* Làm chủ cách tạo User/Group/Policy và thực hành quản trị quyền.
* Biết cách gắn IAM Role vào EC2 và sử dụng temporary credentials an toàn.
* Áp dụng Permission Boundary để ngăn misuse và privilege escalation.
* Kiểm soát EC2 dựa trên Tag để quản trị phân tán.
* Kích hoạt Security Hub, phân tích cảnh báo và kiểm tra tuân thủ.

#### **3. Tối ưu chi phí và bảo mật dữ liệu**
* Tự động bật/tắt EC2 bằng Lambda + EventBridge để tiết kiệm chi phí.
* Mã hóa S3 bằng KMS CMK và theo dõi truy cập bằng CloudTrail.
* Query dữ liệu an toàn qua Athena mà không cần tải file về.

#### **4. Làm chủ AWS Identity Center**
* Quản lý SSO nhiều account, phân quyền theo role.
* Áp dụng Zero Trust: authenticate & authorize tập trung.

#### **5. Hoàn thành dịch thuật 2 blog AWS**
* Hiểu sâu về tính năng AWS Budgets và Bedrock Flows.
* Tăng khả năng đọc – hiểu tài liệu tiếng Anh chuyên ngành.

---

###  Tổng kết tuần 4:
Tuần 4 tập trung vào **bảo mật, quản trị truy cập và tối ưu chi phí AWS**, đặc biệt xoay quanh IAM, Security Hub, KMS và Lambda automation.  
Hoàn thành lý thuyết + loạt lab nâng cao, tạo nền tảng vững chắc cho việc quản trị hệ thống AWS theo chuẩn doanh nghiệp.



