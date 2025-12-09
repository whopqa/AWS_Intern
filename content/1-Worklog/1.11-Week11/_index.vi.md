---
title: "Worklog Tuần 11"
date: 2025-09-10
weight: 2
chapter: false
pre: " <b> 1.11. </b> "
---

### Mục tiêu tuần 11:

* Triển khai và hoàn thiện Webhook Stack cho tích hợp Facebook Messenger.
* Phát triển các nghiệp vụ cho phía Admin và User.
* Tối ưu hóa kiến trúc hệ thống để tiết kiệm chi phí.
* Nghiên cứu Knowledge Distillation trên Amazon Bedrock.
* Xây dựng hệ thống xác thực người dùng an toàn với OTP qua email.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | -------------- |
| 2   | - Tiếp tục phát triển Webhook Stack và Backend Webhook <br> - Thực hiện các thao tác thay đổi DB ở mức row level (theo ID) <br> - Tìm hiểu về Knowledge Distillation trên Amazon Bedrock <br> - Tham dự Workshop event | 17/11/2025   | 17/11/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - Tiếp tục triển khai phía User <br> - Phát triển nghiệp vụ phía Admin <br> - Tìm hiểu cơ chế hoạt động của Event trên Lambda                                                                  | 18/11/2025   | 18/11/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Thiết kế lại Architecture để tiết kiệm chi phí <br>&emsp; + Admin lấy data analytics từ Lambda ngoài VPC <br>&emsp; + Sử dụng DDL/Athena thay cho Glue Crawler <br> - Tạo Jira để quản lý tiến độ project | 19/11/2025   | 19/11/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Nghiên cứu sâu về quản lý bảo mật của Cognito <br> - Đánh giá khả năng áp dụng Cognito cho hệ thống                                                                                         | 20/11/2025   | 20/11/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Deploy thành công Webhook Stack <br> - Tạo App Messenger trên Facebook Developer Dashboard <br> - Cấu hình Page Access Token và Webhook URL <br> - Thiết lập quyền và subscription <br> - Debug và fix các lỗi handler, authentication <br> - Kiểm tra kết nối Messenger với Lambda qua API Gateway <br> - Chuyển sang xác thực OTP qua email (thay thế Cognito) <br> - Triển khai AWS SES Service để gửi email <br> - Xây dựng hệ thống xác thực người dùng với session management <br> - Tích hợp các cơ chế bảo mật: <br>&emsp; + Rate limiting (block sau 5 lần sai OTP) <br>&emsp; + Session timeout (reset sau 15 phút) <br>&emsp; + OTP request throttling (11 giây giữa các lần yêu cầu) <br> - Thêm Usage Plan cho API Gateway <br> - Xác thực Webhook và Facebook Signature | 21/11/2025   | 23/11/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 11:

**Triển khai Webhook và Tích hợp Facebook Messenger:**
* Deploy thành công Webhook Stack kết nối với Facebook Messenger.
* Tạo và cấu hình App Messenger trên Facebook Developer Dashboard bao gồm:
  * Page Access Token
  * Webhook URL configuration
  * Subscription settings và permissions
* Hiểu và triển khai các khái niệm quan trọng:
  * **Page Token:** Khóa xác thực để kết nối API Messenger
  * **Verify Token:** Khóa để Messenger trả thông tin cho API Gateway
  * **PSID (Page-Scoped ID):** ID đặc biệt không thay đổi của mỗi user đối với từng page
* Kết nối thành công Messenger với Lambda qua API Gateway, kiểm tra được events trên CloudWatch.

**Tối ưu hóa Kiến trúc và Chi phí:**
* Thiết kế lại architecture để giảm chi phí:
  * Admin lấy data analytics từ Lambda ngoài VPC
  * Sử dụng DDL/Athena thay vì Glue Crawler để tiết kiệm chi phí
* Thực hiện các thao tác database ở mức row level (theo ID) để tối ưu hiệu suất.
* Tìm hiểu cơ chế hoạt động của Events trên Lambda.

**Nghiên cứu và Học hỏi:**
* Tìm hiểu về Knowledge Distillation trên Amazon Bedrock.
* Nghiên cứu sâu về quản lý bảo mật của Cognito.
* Tham dự Workshop event để cập nhật kiến thức mới.

**Xây dựng Hệ thống Xác thực An toàn:**
* Chuyển từ Cognito sang hệ thống xác thực OTP qua email do vấn đề về lỗi và độ phức tạp.
* Triển khai thành công AWS SES Service để gửi email OTP.
* Xác thực người dùng và lưu session vào DynamoDB với các trường cơ bản.
* Tích hợp các cơ chế bảo mật toàn diện:
  * **Rate Limiting:** Block tài khoản sau 5 lần nhập sai OTP trong một phiên
  * **Session Management:** Reset trạng thái user chưa xác nhận sau 15 phút
  * **Request Throttling:** Yêu cầu OTP cách nhau tối thiểu 11 giây
  * **API Gateway Protection:** Thêm Usage Plan để kiểm soát lưu lượng truy cập
  * **Webhook Security:** Xác thực Facebook Signature để đảm bảo request hợp lệ

**Quản lý Dự án:**
* Tạo Jira để quản lý tiến độ project một cách có hệ thống.
* Phát triển nghiệp vụ cho cả phía User và Admin.

**Các Bài học Kỹ thuật:**
* Hiểu rõ sự khác biệt giữa Page Token và App Secret.
* Nắm vững cơ chế JWT (JSON Web Token) và vai trò của nó như mã bảo mật cho ứng dụng.
* Nhận thức về tính năng động của các thông tin như Webhook URL, Callback URL, User Pool ID, Client ID khi deploy stack - cần có biện pháp quản lý để tránh thay đổi code nhiều lần.
* Debug thành công các lỗi:
  * Handler không xử lý được event (nhầm Page Token thành App Secret)
  * URL Cognito login không hoạt động
* Lưu trữ Session data trong DynamoDB với các trường thông tin user cần thiết.


