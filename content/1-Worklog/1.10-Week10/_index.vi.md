---
title: "Worklog Tuần 10"
date: 2025-09-10
weight: 2
chapter: false
pre: " <b> 1.10. </b> "
---
### Mục tiêu tuần 10:

* Tìm hiểu CDK, AWS CLI để chuẩn bị xây dựng hạ tầng dự án.
* Hoàn thiện kiến trúc tổng thể và đánh số lại toàn bộ luồng đi.
* Phân công nhiệm vụ trong team và xác định module chịu trách nhiệm.
* Bắt đầu triển khai các stack cơ bản: Text2SQL, Webhook.
* Nghiên cứu và triển khai tích hợp Facebook Messenger, Cognito.

---

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | ---------------- | -------------- |
| 2 | - Tìm hiểu AWS CDK và AWS CLI để phục vụ quá trình xây dựng dự án | 10/11/2025 | 10/11/2025 | AWS Docs |
| 3 | - Họp team, phân task <br> - Chỉnh sửa và hoàn thiện kiến trúc tổng thể <br> - Đánh số lại toàn bộ luồng đi trong kiến trúc | 11/11/2025 | 11/11/2025 | Kiến trúc nội bộ |
| 5 | - Phác thảo cấu trúc hạ tầng theo mô hình CDK: <br>&emsp; + Module Stack (triển khai tài nguyên) <br>&emsp; + Module Service (xử lý logic backend) <br>&emsp; + Module Handler (xử lý luồng sự kiện) <br> - Nghiên cứu cách triển khai CDK hạ tầng | 13/11/2025 | 13/11/2025 | AWS CDK Workshop |
| 6 | - Đảm nhận luồng User: xử lý tương tác, tư vấn, đặt lịch, ghi dữ liệu vào DB <br> - Nghiên cứu cách thao tác DB tối ưu & an toàn <br> - Nghiên cứu tối ưu lịch hẹn (booking flow) <br> - Bắt đầu làm Text2SQL Stack & Webhook Stack <br> - Text2SQL Stack: triển khai Lambda Text2SQL để xử lý truy vấn & SQL execution lên PostgreSQL <br> - Webhook Stack: triển khai Lambda Webhook Verify, API Gateway GET/POST, Lambda Role | 14/11/2025 | 14/11/2025 | Nội bộ |
| 6 (tiếp) | - Triển khai Messenger App trên Facebook Developer <br> - Tìm hiểu luồng xác thực Cognito qua Facebook Provider <br> | 14/11/2025 | 14/11/2025 | Facebook Developer, AWS Cognito |

---

### Kết quả đạt được tuần 10:

* Hiểu và nắm được các khái niệm cơ bản về CDK, AWS CLI phục vụ triển khai hạ tầng.
* Hoàn thiện lại kiến trúc tổng thể của dự án và đánh số hợp lý toàn bộ luồng dữ liệu.
* Đã phân chia mô hình hạ tầng thành 3 nhóm module rõ ràng:
  * **Stack** – triển khai tài nguyên CDK (Lambda, API Gateway, RDS, IAM,…)
  * **Service** – xử lý logic backend
  * **Handler** – xử lý event/lambda flow
* Bắt đầu triển khai:
  * **Text2SQL Stack** – Lambda xử lý truy vấn → chuyển thành SQL → chạy trên PostgreSQL
  * **Webhook Stack** – Lambda verify Webhook/Facebook Signature, API Gateway GET/POST, gán IAM Role
* Xây dựng lại luồng User: tư vấn, đặt lịch, ghi DB an toàn & tối ưu.
* Tìm hiểu cách optimize booking flow tránh trùng & tối ưu workflow.
* Triển khai thử Facebook Messenger App và tích hợp Cognito qua Facebook Provider.


---

