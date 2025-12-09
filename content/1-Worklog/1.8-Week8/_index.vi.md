---
title: "Worklog Tuần 8"
date: 2025-09-10
weight: 1
chapter: false
pre: " <b> 1.8. </b> "
---
### Mục tiêu tuần 8:

* Hoàn thiện sơ bộ các thành phần & công nghệ sẽ sử dụng trong dự án.
* Rà soát và cải thiện kiến trúc, các lựa chọn công nghệ.
* Ôn lý thuyết AWS qua video và tài liệu.
* Hệ thống hóa kiến thức các dịch vụ AWS.
* Luyện thi AWS Practitioner & AWS SAA-C03.
* Kiểm tra giữa kỳ.

---

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2 | **Hoàn thiện sơ bộ các thành phần & công nghệ chính** <br> - Xác định dịch vụ & module chính <br> - Đánh giá các điểm cần cải thiện | 27/10/2025 | 27/10/2025 | Kiến trúc nội bộ dự án |
| 3 | **Review video lý thuyết AWS trên YouTube** <br> | 28/10/2025 | 28/10/2025 | [YouTube: AWS Tutorials](https://www.youtube.com/watch?v=AQlsd0nWdZk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| 4 | **Hệ thống lại kiến thức AWS** <br> - EC2, RDS, S3, IAM, Lambda, VPC <br> - Ôn tập bằng AI (ChatGPT/Claude) | 29/10/2025 | 29/10/2025 | AWS Docs |
| 5 | **Ôn tập lý thuyết & luyện đề** <br> - [Quizlet: AWS Hotfix V10](https://quizlet.com/vn/1099628340/aws-hotfix-v10-flash-cards/?funnelUUID=e6969943-0cf6-481d-a9f1-72c54016d0c3) <br> - [Practice Exam AWS Practitioner](https://github.com/kananinirav/AWS-Certified-Cloud-Practitioner-Notes/blob/master/practice-exam/practice-exam-1.md) <br> - [Practice Exam AWS SAA-C03](https://github.com/Iamrushabhshahh/AWS-Certified-Solutions-Architect-Associate-SAA-C03-Exam-Dump-With-Solution/blob/main/AWS%20Certified%20Solutions%20Architect%20Associate%20SAA-C03.pdf) | 30/10/2025 | 30/10/2025 | Quizlet, AWS Exam Guide |
| 6 | **Kiểm tra giữa kỳ** <br> *Top 10 thí sinh điểm cao nhất đợt 1* <br>  | 31/10/2025 | 31/10/2025 | Kết quả nội bộ |

---

### Kết quả đạt được tuần 8:

#### **1. Hoàn thiện sơ bộ các thành phần dự án**
Xác định các dịch vụ cốt lõi (AWS + AI):

**1.1. RAG module – đang hoàn thiện**
* Vấn đề: hiểu & trích xuất intent tiếng Việt.
* Giải pháp: Lex → Lambda (đóng vai trò RAG) → DynamoDB.
* Intent = CSKH → truy xuất RAG từ DynamoDB.
* Intent = Đặt lịch → gọi Bedrock thực thi SQL.

**1.2. Scheduling module**
* Vấn đề: thực thi SQL an toàn cho insert/update/delete trên bảng lịch hẹn.
* Tech: RDS + pgvector.
* Tối ưu cost: cân nhắc EventBridge start/stop RDS.

**1.3. User UI flow**
* Lex → Lambda → Amazon Translate → detect intent → RAG hoặc Scheduling.

**1.4. Admin UI**
* Dashboard web (thống kê tuần/tháng/năm) → S3 + CloudFront + Route53 → thao tác DB với quyền admin.
* Kết hợp Athena + Glue để trích xuất dữ liệu thống kê.

**1.5. Memory system (cache) – DynamoDB**
* Lưu: session history, RAG results, SQL results, output từ Bedrock.
* Triển khai: Lambda trigger khi DB đổi → xoá cache; TTL tự hết hạn (ví dụ 1h).

**1.6. Storage**
* Định kỳ chuyển dữ liệu lịch hẹn sang S3 để thống kê/doanh thu.

#### **2. Rà soát & cải thiện kỹ thuật**
* Ghi chú các điểm cần tối ưu trước lúc build.
* Đánh giá các lựa chọn công nghệ và kiến trúc.


#### **3. Ôn tập AWS Services**
* Củng cố kiến trúc EC2, RDS, IAM, S3, Networking.
* Đặt câu hỏi với AI để củng cố kiến thức trọng tâm.

#### **4. Luyện thi AWS**
* Hoàn thành Quizlet Hotfix V10.
* Làm đề AWS Practitioner và SAA-C03.

#### **5. Kiểm tra giữa kỳ**
* Hoàn thành bài kiểm tra.
* Thuộc danh sách top 10 điểm cao nhất đợt 1.

---

### Tổng kết tuần 8:
Tuần 8 tập trung vào **chỉnh sửa kiến trúc dự án và ôn tập kiến thức AWS**. Đã xác định rõ các module chính (RAG, Scheduling, UI, Cache, Storage) và công nghệ sử dụng. Đồng thời củng cố kiến thức qua luyện đề và đạt kết quả khá tốt trong kiểm tra giữa kỳ.
