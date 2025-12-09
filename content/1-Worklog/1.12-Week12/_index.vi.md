---
title: "Worklog Tuần 12"
date: 2025-09-10
weight: 2
chapter: false
pre: " <b> 1.12 </b> "
---
### Mục tiêu tuần 12:

* Tái cấu trúc và tối ưu hóa kiến trúc hệ thống Chatbot.
* Xây dựng cơ chế quản lý session và caching hiệu quả.
* Phát triển các service files theo nguyên tắc decoupling.
* Triển khai luồng đặt lịch hẹn thông minh với LLM.
* Deploy và test hệ thống đặt lịch trên môi trường thực.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Thiết kế cơ chế Reset Session sau 15 phút để tiết kiệm chi phí <br> - Tạo state xác nhận thông tin đặt lịch trước khi lưu vào DB <br> - Tái cấu trúc code base theo nguyên tắc decoupling: <br>&emsp; + Session Service: quản lý session, context LLM, timeout, cache <br>&emsp; + Bedrock Service: các prompt chuyên biệt (intent classification, SQL query, response) <br>&emsp; + Authenticator Service: xác thực user <br>&emsp; + Embed Service: gọi model embedding và lấy vector <br>&emsp; + Indexer Service: tạo embedding table schema <br>&emsp; + Messenger Service: gửi tin nhắn đến user <br> - Xây dựng Handler Files: <br>&emsp; + Chat Handler: xử lý logic hội thoại <br>&emsp; + Text2SQL Handler: xử lý query và thực thi SQL trên Facebook <br> - Hệ thống lại luồng data cho Admin | 24/11/2025   | 24/11/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - Phân tích các câu hỏi nghiệp vụ đặt lịch: <br>&emsp; + "Bên bạn đang trống những khung giờ nào?" <br>&emsp; + "Tôi rảnh giờ này, bạn có thể đề xuất giờ nào hợp lý nhất không?" <br> - Tìm hiểu schema chính trong hệ thống đặt lịch <br> - Thiết kế cơ chế đặt lịch tối ưu: <br>&emsp; + Giữ lịch tạm thời trong cache (2-3 phút) để tránh đặt trùng <br>&emsp; + Xử lý xung đột khi nhiều người đặt lịch cùng lúc <br>&emsp; + Cấp token xác nhận cho người đặt trước <br> - Cache lịch trống để tăng tốc độ phản hồi <br> - Kiểm tra câu hỏi trùng lặp với cache để tái sử dụng câu trả lời <br> - Nghiên cứu cơ chế Reflection với LLM khi SQL không trả kết quả đúng <br> - Áp dụng Prompt-based Few-shot Learning <br> - Đánh giá khả năng sử dụng SQS <br> - Thiết kế cấu trúc Table Cache: <br>&emsp; + Rolling Summary cho hội thoại (giới hạn token) <br>&emsp; + Cache câu hỏi đặt lịch (SQL statement, text, response, query result, prompt, schema, column name) <br> - Setup SQS để tránh timeout Lambda | 25/11/2025   | 25/11/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Tạo hàm lấy context hội thoại cho LLM <br> - Xây dựng cấu trúc Context cho Model chính (Sonnet/Haiku): <br>&emsp; + System Prompt: định nghĩa luật lệ của bot <br>&emsp; + Structured Summary (từ Cache): tóm tắt trạng thái nghiệp vụ <br>&emsp; + Recent History: giữ nguyên 2-3 turn hội thoại cuối <br> - Phát triển Bedrock Service với cơ chế caching: <br>&emsp; + So sánh query với câu hỏi trước bằng LLM <br>&emsp; + Trả lời từ cache nếu liên quan <br>&emsp; + Lưu metadata cho mỗi turn <br>&emsp; + Giữ lại 3 turn cuối để tiết kiệm token <br> - Hoàn thành phần lớn các Service Files <br> - Xây dựng cấu trúc Session Table trong DynamoDB | 26/11/2025   | 26/11/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Thêm jsonState vào field appointment của Session Table <br> - Xác định phương pháp phân loại intent chính xác (SQL query vs RAG) <br> - Chuẩn bị context cho bot để hiểu ngữ cảnh hội thoại <br> - Code Chat Handler để điều phối luồng logic hội thoại <br> - Xử lý vấn đề câu hỏi cộc lốc thiếu context <br> - Hoàn thành sơ bộ luồng hội thoại <br> - Chuẩn bị sẵn sàng test luồng đặt lịch <br> - Lưu ý: <br>&emsp; + Chưa hoàn thành Intent Classify và RAG Service <br>&emsp; + Chưa set thời gian hủy/xóa session <br>&emsp; + Chưa áp dụng JSON template cho đặt lịch | 27/11/2025   | 27/11/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Deploy và test riêng luồng đặt lịch <br> - Xử lý vấn đề DynamoDB không lưu được dữ liệu float của vector: <br>&emsp; + Chuyển vector thành string khi ghi session <br>&emsp; + Chuyển ngược lại khi search cache <br> - Thay đổi region: <br>&emsp; + Singapore không có model embedding <br>&emsp; + Host sang Tokyo (đánh đổi độ trễ) <br> - Enable model Claude trong Playground <br> - Phát triển hai Prompt chuyên biệt: <br>&emsp; + Mutation Prompt: ràng buộc cho INSERT/UPDATE SQL <br>&emsp; + Query Prompt: chuyên truy vấn thông tin các bảng <br> - Triển khai Logic luồng đặt lịch: <br>&emsp; + Xác định intent (truy vấn vs đặt lịch) <br>&emsp; + Phân chia 3 luồng nhỏ: Đặt lịch / Cập nhật / Hủy <br>&emsp; + In thông tin cuộc hẹn trống và index cache <br>&emsp; + Extract thông tin khách hàng bằng LLM <br>&emsp; + Xác nhận và thực thi đặt lịch <br> - Nhận diện hạn chế: Logic có thể in quá nhiều lịch cùng lúc | 28/11/2025   | 28/11/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 12:

**Tái Cấu Trúc Hệ Thống theo Nguyên Tắc Decoupling:**
* Xây dựng thành công kiến trúc Service-based với các module độc lập:
  * **Session Service:** Quản lý session với các tính năng:
    - Tạo session mới với các trường có sẵn
    - Cập nhật và xóa session
    - Lấy thông tin session và ngữ cảnh cho LLM
    - Kiểm tra timeout và state
    - Lưu cache và tìm kiếm bằng vector search
  * **Bedrock Service:** Quản lý các prompt chuyên biệt:
    - Phân loại intent
    - Truy vấn SQL
    - Tạo response
  * **Authenticator Service:** Xác thực người dùng
  * **Embed Service:** Gọi model embedding và lấy vector
  * **Indexer Service:** Tạo embedding table schema
  * **Messenger Service:** Quản lý gửi tin nhắn đến user
* Xây dựng Handler Files:
  * **Chat Handler:** Xử lý logic hội thoại
  * **Text2SQL Handler:** Xử lý query và thực thi SQL trực tiếp trên Facebook
* Hệ thống lại luồng data cho Admin.

**Tối Ưu Hóa Cơ Chế Session và Caching:**
* Thiết kế cơ chế Reset Session sau 15 phút để tiết kiệm chi phí khi thông tin đặt chưa được xác nhận.
* Tạo state xác nhận để đảm bảo template đầy đủ thông tin trước khi đưa vào DB.
* Xây dựng cấu trúc Session Table trong DynamoDB với trường jsonState trong field appointment.
* Thiết kế cơ chế caching thông minh:
  - **Rolling Summary:** Tóm tắt hội thoại với giới hạn token qua LLM giá rẻ
  - **Query Caching:** Lưu SQL statement, text, response, query result, prompt text, schema_text, column name
  - **Recent History:** Giữ lại 3 turn cuối để tiết kiệm token
  - **Vector Search:** So sánh query với câu hỏi trước bằng LLM

**Xây Dựng Context cho LLM:**
* Thiết kế cấu trúc Context gửi cho Model chính (Sonnet/Haiku):
  - **System Prompt:** Định nghĩa luật lệ của bot
  - **Structured Summary (từ Cache):** Tóm tắt trạng thái nghiệp vụ (ví dụ: "Khách tên A, muốn khám ngày X, chưa chốt giờ")
  - **Recent History:** Giữ nguyên văn 2-3 turn cuối để bot nắm bắt giọng văn và câu hỏi liền trước
* Chuẩn bị context cho bot mỗi lần gọi để hiểu được ngữ cảnh hội thoại.

**Phát Triển Luồng Đặt Lịch Thông Minh:**
* Phân tích và xử lý các câu hỏi nghiệp vụ:
  - "Bên bạn đang trống những khung giờ nào?"
  - "Tôi rảnh giờ này, bạn có thể đề xuất giờ nào hợp lý nhất không?"
* Thiết kế cơ chế đặt lịch tối ưu:
  - **Giữ lịch tạm thời:** Cache lịch trong 2-3 phút để tránh đặt trùng khi nhiều người đặt cùng lúc
  - **Token xác nhận:** Người đặt trước nhận token để tiếp tục xác nhận
  - **Thông báo chờ:** Những trường hợp khác được thông báo chờ cập nhật mới nhất
  - **Cache lịch trống:** Tăng tốc độ phản hồi, cập nhật khi có thay đổi trong DB
  - **Kiểm tra trùng lặp:** Check câu hỏi user có cùng nghĩa với các câu trước để gửi lại câu trả lời cũ
* Triển khai Logic luồng với 3 nhánh chính:
  1. **Đặt lịch mới:** In thông tin cuộc hẹn trống → User chọn → Extract thông tin bằng LLM → Xác nhận → Thực thi
  2. **Cập nhật lịch:** Tự động in các lịch đã đặt của user → User chọn lịch cần cập nhật → Sửa đổi thông tin → Xác nhận → Thực thi
  3. **Hủy lịch:** Tự động in các lịch đã đặt của user → User chọn lịch cần hủy → Xác nhận → Hủy cuộc hẹn

**Phát Triển Prompt Chuyên Biệt:**
* **Mutation Prompt:** Chứa các ràng buộc chuyên cho INSERT/UPDATE SQL
* **Query Prompt:** Chuyên cho truy vấn thông tin các bảng
* Nghiên cứu cơ chế Reflection với LLM khi SQL không trả kết quả đúng.
* Áp dụng Prompt-based Few-shot Learning.

**Deploy và Xử Lý Vấn Đề Kỹ Thuật:**
* Deploy và test thành công luồng đặt lịch riêng.
* Xử lý vấn đề DynamoDB không lưu được dữ liệu float:
  - Chuyển vector thành string khi ghi session
  - Chuyển ngược lại khi search cache
* Thay đổi region cho model embedding:
  - Region Singapore không có model embedding
  - Host sang Tokyo (đánh đổi độ trễ)
* Enable model Claude trong Playground để sử dụng.
* Setup SQS để tránh timeout Lambda.

**Các Bài Học và Thách Thức:**
* Xác định phương pháp phân loại intent chính xác giữa SQL query và RAG.
* Xử lý vấn đề câu hỏi cộc lốc thiếu context (ví dụ: "Giờ nào?" → Đâu biết giờ của ai?).
* Nhận diện hạn chế: Logic hiện tại có thể in quá nhiều lịch cùng lúc, chưa thông minh.
* Các phần chưa hoàn thành:
  - Intent Classify và RAG Service
  - Thời gian hủy/xóa session
  - JSON template cho đặt lịch


