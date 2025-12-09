---
title: "Worklog Tuần 7"
date: 2025-09-10
weight: 1
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu tuần 7:

* Đọc và phân tích các blog AI trên AWS.
* Chọn baseline kiến trúc từ blog AWS để phát triển chatbot.
* Xây dựng direction ban đầu cho chatbot dự án.
* Chạy thử nghiệm deploy Text-to-SQL Chatbot mẫu.
* Họp và tổng hợp các hướng tối ưu (cache, RBAC, scaling…).

---

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2 | **Đọc & tham khảo blog AI** <br> - AWS Knowledge Hub <br> - Tổng hợp kiến thức & best practices AI | 20/10/2025 | 20/10/2025 | [AWS Knowledge Hub](https://www.notion.so/268d23b23efb808a8805c570231cefa9?v=268d23b23efb8088ba76000ca96674ea&source=copy_link)  |
| 3 | **Chọn blog baseline:** <br> - [“Build an AI-powered Text-to-SQL Chatbot”](https://aws.amazon.com/vi/blogs/database/build-an-ai-powered-text-to-sql-chatbot-using-amazon-bedrock-amazon-memorydb-and-amazon-rds/?utm_source=chatgpt.com) <br> - Nghiên cứu code, kiến trúc, workflow <br> - Phân tích các công nghệ: Bedrock, Aurora, SQL generation | 21/10/2025 | 21/10/2025 | [AWS Blog](https://aws.amazon.com/vi/blogs/database/build-an-ai-powered-text-to-sql-chatbot-using-amazon-bedrock-amazon-memorydb-and-amazon-rds/?utm_source=chatgpt.com) |
| 4 | **Xây dựng Direction ban đầu cho chatbot** <br> - Viết tài liệu Direction trên Notion <br> - Định hướng pipeline, role, kiến trúc, giới hạn bot <br> - Xác định quy tắc tương tác | 22/10/2025 | 22/10/2025 | [Direction](https://www.notion.so/Directions-295d23b23efb80bb9500e5cb3222414c?v=268d23b23efb8088ba76000ca96674ea&source=copy_link) |
| 5 | **Deploy thử blog mẫu**: “Build an AI-powered Text-to-SQL Chatbot” <br> - Chạy thử end-to-end <br> - Ghi chú vấn đề & hướng tối ưu | 23/10/2025 | 23/10/2025 | [AWS Blog](https://aws.amazon.com/vi/blogs/database/build-an-ai-powered-text-to-sql-chatbot-using-amazon-bedrock-amazon-memorydb-and-amazon-rds/?utm_source=chatgpt.com) |
| 6 | **Họp & ghi chú trên Notion** <br> **Nội dung họp gồm:** <br> 1. Cơ chế cache & tối ưu bot <br> 2. Thiết kế quyền truy cập RBAC <br> 3. Dòng dữ liệu RDS → S3 archive <br> 4. Scaling: RDS, UI, Lex + Translate | 24/10/2025 | 24/10/2025 | [Họp nội bộ](https://www.notion.so/NOTE-h-p-298d23b23efb8072a6a3e1f67d5c640a?source=copy_link)|

---

### Kết quả đạt được tuần 7:

* **Tham khảo AWS Knowledge Hub:**  
  - Tổng hợp workflow AI chatbot.  
  - Ghi chú các dịch vụ trọng điểm: Bedrock, RDS, S3, caching layer.

* **Chọn baseline từ “Build an AI-powered Text-to-SQL Chatbot”:**  
  - Hiểu kiến trúc Text-to-SQL.  
  - Nắm pipeline: embedding → SQL generation → execution.

* **Hoàn thành Direction trên Notion:**  
  - Xác định phạm vi tính năng.  
  - Định nghĩa chiến lược hạn chế bot thao tác sai.  
  - Flow theo role: member / consultant.  
  - Quy tắc SELECT/UPDATE/DELETE an toàn.

* **Deploy thành công mô hình mẫu:**  
  - Thử nghiệm thực tế.  
  - Ghi chú các vấn đề cần tối ưu.

* **Tổng hợp nội dung họp:**

  **1. Cache & tối ưu bot**  
  - Cache câu hỏi phổ biến để giảm tải DB.  
  - Giới hạn bot không được “toàn quyền chỉnh sửa” dữ liệu.

  **2. RBAC – quyền truy cập & bảo mật**  
  - Bot chạy theo credential tương ứng role.  
  - SELECT xử lý chung; UPDATE/DELETE kiểm tra role + logic.

  **3. Dòng dữ liệu & lưu trữ**  
  - RDS archive sang S3 để phân tích & dashboard.

  **4. Scaling**  
  - RDS: read replicas, Multi-AZ, autoscaling.  
  - UI scaling.  
  - Lex + Translate cho tiếng Việt (Translate free 2M ký tự/tháng năm đầu).


