---
title: "Worklog Tuần 9"
date: 2025-09-10
weight: 1
chapter: false
pre: " <b> 1.9. </b> "
---
### Mục tiêu tuần 9:

* Hoàn thiện và thống nhất kiến trúc tổng thể của dự án.
* Đánh giá lựa chọn công nghệ: Lex, Translate, Bedrock, Webhook.
* Tối ưu chi phí và mô hình triển khai.
* Chuẩn hóa proposal: mục tiêu bài toán, component, dataflow.
* Nộp proposal đợt 1.

---

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | -------- | ------------ | --------------- | -------------- |
| 2 | - Họp với team về hướng tiếp cận mới <br> - Đề xuất thay Amazon Lex + Translate bằng Custom Webhook + Bedrock Claude <br> - Lý do: Lex không hỗ trợ tiếng Việt, Claude hỗ trợ tốt hơn | 03/11/2025 | 03/11/2025 | Tài liệu nội bộ |
| 3 | - Hoàn thiện kiến trúc tổng thể dự án trên draw.io <br> - Upload bản kiến trúc lên Google Drive | 04/11/2025 | 04/11/2025 | [Proposal,Architecture](https://drive.google.com/drive/u/0/folders/1gkahOsw673lZPGN3CNM1mr5l34ZpCcOt) |
| 4 | - Tiếp tục cải thiện kiến trúc <br>&emsp; + Giảm số lượng VPC Endpoint để tiết kiệm chi phí <br>&emsp; + Sắp xếp Lambda theo mức bảo mật & hiệu suất (trong/ngoài VPC) <br>&emsp; + Đánh số luồng dữ liệu | 05/11/2025 | 05/11/2025 | [Proposal,Architecture](https://drive.google.com/drive/u/0/folders/1gkahOsw673lZPGN3CNM1mr5l34ZpCcOt) |
| 5 | - Tính toán pricing cho toàn bộ hệ thống <br> - Kiểm tra và chỉnh sửa Proposal: <br>&emsp; + Mục tiêu bài toán <br>&emsp; + Các component chính và vai trò <br>&emsp; + Giải thích dataflow | 06/11/2025 | 06/11/2025 | AWS Pricing |
| 6 | - Hoàn thiện Proposal <br> - Nộp Proposal đợt 1 | 07/11/2025 | 07/11/2025 | [Proposal,Architecture](https://drive.google.com/drive/u/0/folders/1gkahOsw673lZPGN3CNM1mr5l34ZpCcOt) |

---

### Kết quả đạt được tuần 9:

* **Thống nhất hướng tiếp cận mới:**  
  - Loại bỏ Lex + Translate.  
  - Dùng Custom Webhook + Bedrock Claude cho luồng hội thoại tiếng Việt.  
  - Đơn giản hóa pipeline và nâng độ chính xác.

* **Hoàn thiện bản kiến trúc tổng thể:**  
  - Cập nhật đầy đủ flow: Webhook → Bedrock → Lambda → Database.  
  - Tối ưu hóa vị trí Lambda (inside/outside VPC).  
  - Đánh số và chuẩn hóa toàn bộ luồng dữ liệu.

* **Tối ưu chi phí:**  
  - Giảm số lượng VPC Endpoint không cần thiết.  
  - Rà soát chi phí RDS, S3, Lambda, Bedrock, API Gateway.

* **Tính toán pricing & lập báo cáo chi phí dự kiến.**

* **Hoàn thiện Proposal (đợt 1):**  
  - Rõ ràng mục tiêu bài toán.  
  - Mô tả đầy đủ các component và vai trò.  
  - Giải thích dataflow theo kiến trúc cập nhật.  
  - Chuẩn hóa format để nộp cho team.


