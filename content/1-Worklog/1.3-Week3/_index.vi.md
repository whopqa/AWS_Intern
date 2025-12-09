---
title: "Worklog Tuần 3"
date: 2025-09-10
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu tuần 3:
* Nắm chắc kiến thức lý thuyết về Amazon S3, Storage Class, CORS, Versioning, Glacier, Snow Family, Storage Gateway và AWS Backup.
* Thực hành chuỗi lab chuyên sâu về Storage: AWS Backup, VM Import/Export, File Storage Gateway, Amazon S3 static website hosting và Amazon FSx for Windows.
* Hiểu mô hình Hybrid Storage (On-premise ↔ AWS) và thực hành các cơ chế chia sẻ file, backup, phục hồi dữ liệu và import/export máy ảo.
* Nâng cao kỹ năng thao tác S3, Backup, Gateway, CLI, FSx và quản lý file system trên Windows.

---

### Các công việc triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2 | - Hoàn thành lý thuyết Module 4:<br>&emsp; + Khái niệm về S3<br>&emsp; + Storage Class (Standard, IA, Intelligent-Tiering, One Zone IA, Glacier/Deep Archive)<br>&emsp; + CORS & Versioning<br>&emsp; + Object key & hiệu năng<br>&emsp; + Snow Family & Storage Gateway<br>&emsp; + AWS Backup | 22/9/2025 | 22/9/2025 | AWS Academy Module 4 |
| 3 | - Hoàn thành Lab 13 – AWS Backup:<br>&emsp; + Tạo backup plan tự động<br>&emsp; + Khôi phục dữ liệu từ bản backup<br>&emsp; + Tích hợp SNS nhận thông báo backup/restore | 23/9/2025 | 23/9/2025 | Tài liệu lab AWS Backup |
| 4 | - Hoàn thành Lab 14 – VM Import/Export:<br>&emsp; + Chuẩn bị & export VM thành OVA/OVF<br>&emsp; + Upload vào S3 & tạo role vmimport<br>&emsp; + Import thành AMI & chạy EC2<br>&emsp; + Thực hành export instance ngược lại | 24/9/2025 | 24/9/2025 | Tài liệu VM Import/Export |
| 5 | - Hoàn thành Lab 24 – File Storage Gateway:<br>&emsp; + Khởi tạo Storage Gateway & kết nối S3<br>&emsp; + Tạo File Share (NFS/SMB)<br>&emsp; + Mount từ máy on-premise & kiểm tra chia sẻ file | 25/9/2025 | 25/9/2025 | AWS Storage Gateway Workshop |
| 6 | - Hoàn thành Lab 57 – Amazon S3 Static Website:<br>&emsp; + Tạo bucket & bật Static Website<br>&emsp; + Cấu hình public access & bucket policy<br>&emsp; + Upload file website & test S3 endpoint<br>&emsp; + Versioning / Transfer Acceleration / Sao chép object<br><br> - Hoàn thành Lab 25 – FSx for Windows:<br>&emsp; + Tạo FSx & kết nối SMB<br>&emsp; + Map network drive & chia sẻ file<br>&emsp; + Bật deduplication, shadow copy, quota, continuous access<br>&emsp; + Mở rộng throughput & storage | 26/9/2025 | 26/9/2025 | S3 Workshop, FSx Workshop |

---

### Kết quả đạt được tuần 3:

#### **1. Hoàn thành lý thuyết Module 4**
* Hiểu rõ về Amazon S3 và các Storage Class, cơ chế tiết kiệm chi phí và chọn lớp lưu trữ phù hợp.
* Nắm CORS, Versioning, Object key design và cách tối ưu hiệu năng truy cập S3.
* Hiểu các dịch vụ lưu trữ đặc thù: Glacier, Snow Family, Storage Gateway.
* Nắm cơ chế tự động hóa backup và lifecycle bằng AWS Backup.

#### **2. Hoàn thành Lab 13 – AWS Backup**
* Tạo và quản lý Backup Vault, Backup Plan.
* Tự động hóa sao lưu tài nguyên (EBS/RDS/DynamoDB/EFS).
* Khôi phục dữ liệu từ bản backup.
* Thiết lập SNS để nhận thông báo mỗi lần chạy backup/restore.

#### **3. Hoàn thành Lab 14 – VM Import/Export**
* Làm quen quy trình import máy ảo từ on-premise lên AWS bằng AWS CLI.
* Tạo AMI từ OVF/OVA/VMDK và chạy EC2 instance từ AMI đó.
* Thực hành export EC2 instance ngược về dạng VM on-prem.

#### **4. Hoàn thành Lab 24 – File Storage Gateway**
* Tạo File Storage Gateway và kết nối với S3 Bucket.
* Tạo File Share (SMB/NFS) và truy cập từ máy on-premise.
* Học cơ chế Hybrid Storage (lưu file local, đồng bộ lên AWS).

#### **5. Hoàn thành Lab 57 – S3 Static Website**
* Triển khai website tĩnh trên S3.
* Làm chủ cấu hình public access, bucket policy, versioning.
* Tăng tốc website bằng Transfer Acceleration.
* Thực hành copy object giữa các region và tối ưu chi phí.

#### **6. Hoàn thành Lab 25 – Amazon FSx for Windows**
* Tạo FSx và tích hợp vào Windows Server/Windows Client.
* Truy cập SMB file share và cấu hình phân quyền.
* Bật Shadow Copy, Deduplication, User Quota.
* Mở rộng throughput & storage theo nhu cầu.

---

### Tổng kết tuần 3:
Tuần 3 tập trung 100% vào mảng **AWS Storage & Hybrid Storage**, đặc biệt là các dịch vụ S3, Backup, Gateway, VM Import/Export và FSx. Đây là tuần quan trọng giúp hiểu cách AWS xử lý lưu trữ, phục hồi dữ liệu, quản lý file system và kết nối với hệ thống on-premise.

Hoàn thành đầy đủ lý thuyết + 5 lab quan trọng, tạo nền tảng vững chắc cho các tuần tiếp theo về EC2 nâng cao, Database và Systems Operations.

---
