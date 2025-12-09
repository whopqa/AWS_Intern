---
title: "Worklog Tuần 13"
date: 2025-09-10
weight: 13
chapter: false
pre: " <b> 1.13 </b> "
---
### Mục tiêu tuần 13:

* Hoàn thiện và tối ưu hóa luồng đặt lịch hẹn với xử lý các trường hợp edge case.
* Xử lý vấn đề throttling và timeout trong hệ thống.
* Cải thiện prompt engineering để tăng độ chính xác của bot.
* Tối ưu hóa vector search và schema retrieval.
* Deploy, test và fix bug trên môi trường production.
* Hoàn thiện documentation và demo.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 1   | - Tiếp tục phát triển luồng đặt lịch song song với deploy test chức năng <br> - Bổ sung Webhook Receiver để xử lý request từ Messenger: <br>&emsp; + Triển khai SQS để tránh Lambda timeout <br>&emsp; + Ngăn chặn việc trả response nhiều lần <br> - Xử lý lỗi throttling khi invoke Lambda (quá nhiều lần gọi bot) <br> - Cải thiện prompt cho SQL mutation: <br>&emsp; + Fix lỗi cột, lỗi bảng, lỗi param <br>&emsp; + Thêm chú thích về enum param và param cho user nhập <br> - Tối ưu schema search bằng embedding: <br>&emsp; + Tạo hàm lọc lấy top bảng gần nhất <br>&emsp; + Cải thiện similarity score bằng cách thêm string annotation cho tên bảng <br> - Cập nhật quyền: <br>&emsp; + Admin cho mutation SQL (DB admin secret) <br>&emsp; + Readonly cho SELECT SQL | 01/12/2025   | 01/12/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 2   | - Merge 2 nhánh phát triển và deploy test <br> - Xử lý các vấn đề phát hiện: <br>&emsp; + Prompt mutation SQL thiếu linh hoạt khi schema thay đổi <br>&emsp; + Hallucination: Bot trả lời bình thường khi không có kết quả SQL <br>&emsp; + Throttling vẫn xảy ra <br>&emsp; + Response quá dài (>2000 ký tự) khiến Messenger không xử lý được <br> - Cải thiện prompt: <br>&emsp; + Thêm prompt trả lời dựa trên kết quả SQL (không có kết quả → trả lời theo context) <br>&emsp; + Chỉnh extraction prompt để hiểu ý định cuối cùng trước khi lấy thông tin <br>&emsp; + Tránh bias vào context <br>&emsp; + Yêu cầu output <2000 ký tự <br> - Thử nghiệm nâng cấp model: <br>&emsp; + Đổi Claude 3 Haiku → Claude 3.5 Sonnet <br>&emsp; + Sử dụng cross-region (đánh đổi độ trễ cao → timeout) | 03/12/2025   | 03/12/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 2   | - Cập nhật luồng đặt lịch mới: <br>&emsp; **Luồng Create:** <br>&emsp;&emsp; • Prompt lấy thông tin bắt đầu khi xác định intent là booking create <br>&emsp;&emsp; • Chuyển sang collecting state <br>&emsp;&emsp; • Không cần gọi prompt phân loại intent trong collecting state <br>&emsp;&emsp; • Gọi prompt trích xuất → check field → response hỏi → cho phép user hỏi thêm <br>&emsp;&emsp; • Lặp đến khi đủ consultant name, date, time <br>&emsp;&emsp; • Hiển thị thông báo chờ → lấy lịch trống → cache index <br>&emsp;&emsp; • User chọn lịch → xác nhận → confirm state → mutation → thông báo → idle <br>&emsp; **Luồng Update:** <br>&emsp;&emsp; • Intent update → selecting slots state <br>&emsp;&emsp; • Lấy lịch đã đặt theo customer ID → cache index → user chọn <br>&emsp;&emsp; • Lưu param lịch cũ và lịch mới → chuyển collecting state <br>&emsp;&emsp; • Update: Cancel lịch cũ + Insert lịch mới <br>&emsp; **Luồng Delete:** <br>&emsp;&emsp; • Lấy lịch theo customer ID → user chọn → xác nhận → mutation cancel | 03/12/2025   | 03/12/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Điều chỉnh temperature của model để tăng độ chính xác <br> - Fix lỗi so sánh tiếng Việt: <br>&emsp; + Không dùng ILIKE thông thường <br>&emsp; + Sử dụng unaccent trong DB schema <br> - Cải thiện prompt lấy ID: <br>&emsp; + Linh hoạt hơn với thông tin mềm (consultant name) <br>&emsp; + Sử dụng SELECT OR thay vì yêu cầu đủ cả name, date, time <br> - Gộp intent recognition và extraction info thành một prompt (Claude 3 Sonnet) <br> - Thêm ràng buộc: <br>&emsp; + Hỏi thông tin customer chỉ theo ID <br>&emsp; + Lấy lịch consultant chỉ theo thời gian hiện tại và tương lai | 05/12/2025   | 05/12/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Hoàn thiện welcome message thông minh hơn <br> - Chỉnh sửa: <br>&emsp; + Chỉ lấy lịch của user với status "pending" <br>&emsp; + Ràng buộc lấy lịch hẹn: time > current_time nếu day = current_day <br> - Chỉnh sửa lại proposal document <br> - Viết README documentation <br> - Chuẩn bị và thực hiện demo hệ thống | 07/12/2025   | 07/12/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 13:

**Xử Lý Vấn Đề Throttling và Timeout:**
* Triển khai SQS làm message queue giữa Messenger và Lambda:
  - Webhook receiver nhận request từ Messenger và đẩy vào SQS
  - Lambda consumer xử lý message từ queue
  - Ngăn chặn việc trả response nhiều lần do timeout
  - Giảm thiểu lỗi throttling khi có quá nhiều request đồng thời
* Xử lý lỗi throttling invoke Lambda khi thực hiện SQL mutation để đặt lịch
* Cấu hình quyền truy cập database:
  - Admin secret cho mutation SQL (INSERT/UPDATE/DELETE)
  - Readonly permission cho SELECT SQL

**Tối Ưu Hóa Vector Search và Schema Retrieval:**
* Cải thiện hiệu quả tìm kiếm schema bằng embedding:
  - Tạo hàm lọc để lấy top các bảng có similarity cao nhất
  - Thêm string annotation (chú thích) cho mỗi tên bảng để cải thiện similarity score
  - Giảm số lượng schema trả về từ quá nhiều xuống chỉ những bảng liên quan nhất
* Xử lý vấn đề similarity score thấp và kết quả không chính xác

**Cải Thiện Prompt Engineering:**
* Nâng cấp prompt cho SQL mutation:
  - Fix lỗi cột, lỗi bảng, lỗi parameter
  - Thêm hướng dẫn chi tiết về enum parameters
  - Chỉ rõ parameters nào user cần nhập
  - Tăng tính linh hoạt khi schema thay đổi
* Xử lý vấn đề hallucination:
  - Bot trả lời dựa trên kết quả SQL thực tế
  - Khi không có kết quả SQL → trả lời theo context thay vì câu trả lời cứng
  - Tránh bias vào context không liên quan
* Tối ưu output:
  - Yêu cầu response <2000 ký tự để Messenger xử lý được
  - Điều chỉnh temperature của model để tăng độ chính xác
* Cải thiện extraction prompt:
  - Hiểu ý định cuối cùng của user trước khi lấy thông tin điền field
  - Gộp intent recognition và extraction info thành một prompt cho Claude 3 Sonnet

**Hoàn Thiện Luồng Đặt Lịch:**
* **Luồng Create (Đặt lịch mới):**
  1. Xác định intent là booking create → chuyển sang collecting state
  2. Không cần gọi prompt phân loại intent trong collecting state
  3. Gọi prompt trích xuất thông tin → check các field cần thiết
  4. Trả response hỏi thông tin thiếu → cho phép user hỏi thêm thông tin
  5. Lặp lại cho đến khi đủ consultant name, date, time
  6. Hiển thị thông báo chờ → gọi prompt lấy lịch trống
  7. Cache index thông tin lịch mới (consultant id, name, date, time)
  8. User chọn lịch → lấy thông tin làm param
  9. User xác nhận → confirm state → mutation prompt → execute
  10. Thông báo thành công/thất bại → chuyển về idle state

* **Luồng Update (Cập nhật lịch):**
  1. Xác định intent update → selecting slots state
  2. Tự động lấy lịch đã đặt theo customer ID → cache index
  3. User chọn lịch muốn đổi
  4. Lưu time, date, consultant id của lịch cũ vào param
  5. Lưu customer id, email, phone vào param lịch mới
  6. Chuyển sang collecting state (tương tự create)
  7. Execute: Cancel lịch cũ (update status) + Insert lịch mới

* **Luồng Delete (Hủy lịch):**
  1. Xác định intent delete
  2. Tự động lấy lịch đã đặt theo customer ID → cache index
  3. User chọn lịch muốn hủy
  4. Lấy thông tin lịch cũ
  5. User xác nhận → mutation SQL (update status thành "cancelled")

**Xử Lý Tiếng Việt và Database:**
* Fix lỗi so sánh tiếng Việt:
  - Không sử dụng ILIKE thông thường
  - Cấu hình và sử dụng extension unaccent trong PostgreSQL
  - Thiết lập lại trong DB schema để hỗ trợ tìm kiếm tiếng Việt không dấu
* Cải thiện prompt lấy ID dựa trên thông tin mềm:
  - Linh hoạt hơn với thông tin như consultant name
  - Sử dụng SELECT OR thay vì yêu cầu đủ cả consultant name, date, và time

**Thử Nghiệm Model và Cross-Region:**
* Nâng cấp từ Claude 3 Haiku lên Claude 3.5 Sonnet:
  - Cải thiện chất lượng trả lời
  - Hiểu context tốt hơn
* Sử dụng cross-region inference:
  - Đánh đổi giữa chất lượng model và độ trễ
  - Độ trễ cao hơn nhưng có thể gây timeout
  - Cần cân bằng giữa performance và latency

**Ràng Buộc và Business Logic:**
* Thêm các ràng buộc nghiệp vụ:
  - Hỏi thông tin customer chỉ được theo customer ID
  - Lấy lịch consultant chỉ theo thời gian hiện tại và tương lai
  - Chỉ lấy lịch của user với status "pending"
  - Lấy lịch hẹn: time > current_time nếu day = current_day
* Hoàn thiện welcome message thông minh hơn với context

**Documentation và Demo:**
* Chỉnh sửa và hoàn thiện proposal document
* Viết README documentation đầy đủ
* Chuẩn bị và thực hiện demo hệ thống thành công

**Các Bài Học và Insight:**
* Temperature của model ảnh hưởng lớn đến độ chính xác của thông tin trích xuất
* Gộp nhiều prompt thành một có thể giảm số lần gọi API và tăng tính nhất quán
* Vector search cần fine-tune cẩn thận với annotation để đạt similarity tốt
* Cross-region inference là trade-off giữa model quality và latency
* SQS là giải pháp hiệu quả cho vấn đề throttling và timeout
* Xử lý tiếng Việt cần extension unaccent trong PostgreSQL
* Business logic ràng buộc rất quan trọng để tránh data không hợp lệ


