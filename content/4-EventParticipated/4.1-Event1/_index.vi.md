---
title: "Event 1"
date: "2025-09-09"
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

# Những Điểm Chính từ "AWS Cloud Mastery Series #1 - AI/ML/GenAI on AWS"

### Tổng Quan Sự Kiện

Buổi học này cung cấp cái nhìn chuyên sâu về hệ sinh thái AI/ML/GenAI của AWS và các phương pháp thực tế để triển khai các công nghệ này trong môi trường production. Sự kiện đã tập hợp các chuyên gia cloud, những người đam mê AI và các chuyên gia trong ngành để chia sẻ những hiểu biết về việc tận dụng danh mục AI toàn diện của AWS để xây dựng các ứng dụng thông minh thế hệ mới.

### Diễn Giả

- **Lâm Tuấn Kiệt** – Sr DevOps Engineer, FPT Software  
- **Danh Hoàng Hiếu Nghị** – AI Engineer, Renova Cloud  
- **Đinh Lê Hoàng Anh** – Cloud Engineer Trainee, First Cloud AI Journey  
- **Văn Hoàng Kha** – Community Builder

### Các Chủ Đề Chính

## 1. Xây Dựng với Nền Tảng Generative AI Amazon Bedrock

**Hiểu về Foundation Models:**  
Amazon Bedrock cung cấp quyền truy cập vào các mô hình nền tảng được huấn luyện trước từ các công ty AI hàng đầu như Anthropic, OpenAI và Meta. Các mô hình này có thể được tinh chỉnh cho các trường hợp sử dụng cụ thể mà không cần cơ sở hạ tầng huấn luyện mở rộng. Điều này dân chủ hóa phát triển AI bằng cách loại bỏ nhu cầu về chuyên môn ML chuyên sâu và tài nguyên GPU đắt tiền, cho phép các đội tập trung vào giải quyết vấn đề kinh doanh thay vì quản lý cơ sở hạ tầng.

**Các Phương Pháp Prompt Engineering Hiệu Quả:**  
Các phương pháp prompting khác nhau có thể ảnh hưởng đáng kể đến hiệu suất của mô hình:
  + **Zero-shot prompting:** Hướng dẫn nhiệm vụ trực tiếp không có ví dụ, phù hợp cho các truy vấn đơn giản.  
  + **Few-shot prompting:** Bao gồm các đầu vào và đầu ra mẫu để hướng dẫn hành vi của mô hình.  
  + **Chain-of-Thought prompting:** Yêu cầu lập luận từng bước để cải thiện độ chính xác giải quyết vấn đề phức tạp.

**Kiến Trúc Retrieval Augmented Generation (RAG):**  
RAG nâng cao phản hồi AI bằng cách kết hợp khả năng của mô hình với các cơ sở tri thức bên ngoài, giải quyết thách thức về ảo giác (hallucination) và giữ cho các hệ thống AI được cập nhật với thông tin hiện tại:
  + **Giai đoạn Retrieval:** Tìm kiếm thông tin liên quan từ kho tài liệu bằng vector similarity.  
  + **Giai đoạn Augmentation:** Làm phong phú prompt với ngữ cảnh được truy xuất, cung cấp nền tảng cho mô hình.  
  + **Giai đoạn Generation:** Tạo ra các phản hồi chính xác, có cơ sở dựa trên cả kiến thức của mô hình và dữ liệu bên ngoài.  
  + **Các trường hợp sử dụng:** Chatbot thông minh, hệ thống tìm kiếm ngữ nghĩa, tóm tắt nội dung tự động và trả lời câu hỏi theo lĩnh vực cụ thể.  
  + **Lợi ích:** Giảm ảo giác, cho phép cập nhật kiến thức real-time mà không cần huấn luyện lại, và cung cấp nguồn trích dẫn để minh bạch.

**Amazon Titan Embeddings:**  
Mô hình chuyên biệt này chuyển đổi văn bản thành các biểu diễn vector số (embeddings), cho phép khớp tương tự ngữ nghĩa và hỗ trợ triển khai RAG với khả năng đa ngôn ngữ. Khác với khớp từ khóa truyền thống, embeddings nắm bắt ý nghĩa ngữ nghĩa của văn bản, cho phép hệ thống tìm nội dung tương tự về mặt khái niệm ngay cả khi các từ chính xác không khớp. Điều này đặc biệt có giá trị cho các ứng dụng đa ngôn ngữ và hiểu ý định người dùng.

**Các Dịch Vụ AI Sẵn Sàng của AWS:** API sẵn sàng production cho các tác vụ AI phổ biến:
  - Rekognition – Phân tích nội dung hình ảnh  
  - Translate – Dịch đa ngôn ngữ  
  - Textract – Xử lý tài liệu thông minh  
  - Transcribe – Chuyển đổi audio thành văn bản  
  - Polly – Tổng hợp giọng nói  
  - Comprehend – Phân tích văn bản và NLP  
  - Kendra – Tìm kiếm doanh nghiệp  
  - Lookout – Phát hiện bất thường  
  - Personalize – Đề xuất được cá nhân hóa  

**Demo Trực Tiếp:**  
Ứng dụng AMZPhoto đã trình diễn triển khai nhận diện khuôn mặt thực tế sử dụng các dịch vụ AI của AWS. Demo thực hành này minh họa cách tích hợp nhiều dịch vụ AWS (Rekognition, S3, Lambda) thành một ứng dụng gắn kết, thể hiện các mẫu kiến trúc thực tế và các phương pháp hay nhất để xây dựng các giải pháp AI sẵn sàng production.

---


## 2. Mở Rộng AI Agents với Amazon Bedrock AgentCore

AgentCore cung cấp cơ sở hạ tầng cấp doanh nghiệp để triển khai các AI agent tự động có thể thực hiện các tác vụ phức tạp, nhiều bước:
  - Thực thi workflow agent an toàn và khả năng mở rộng với cân bằng tải tự động  
  - Quản lý bộ nhớ liên tục cho các tương tác có trạng thái qua các phiên  
  - Kiểm soát truy cập và chính sách bảo mật chi tiết đảm bảo tuân thủ yêu cầu doanh nghiệp  
  - Tích hợp sẵn: Browser Tool, Code Interpreter, Memory Store và gọi hàm tùy chỉnh  
  - Giám sát toàn diện và audit trail cho gỡ lỗi và quản trị  
  - Tương thích với các framework chính: CrewAI, LangGraph, LlamaIndex, OpenAI Agents SDK  
  - Hỗ trợ các mẫu cộng tác và điều phối đa agent

---

### Những Điểm Học Chính

- **Phát triển AI tập trung với Bedrock:** Nền tảng duy nhất để truy cập các mô hình nền tảng đa dạng giúp đơn giản hóa phát triển và giảm rủi ro bị lock-in nhà cung cấp.  
- **Kết hợp prompts và RAG:** Các kỹ thuật này là thiết yếu để xây dựng các ứng dụng AI nhận biết ngữ cảnh có thể xử lý kiến thức theo lĩnh vực cụ thể.  
- **Vector embeddings cho phép hiểu ngữ nghĩa:** Titan Embeddings cải thiện độ liên quan tìm kiếm và truy xuất thông tin vượt xa khớp từ khóa đơn giản.  
- **Tận dụng các dịch vụ được quản lý:** Các công cụ AI sẵn có của AWS giảm đáng kể thời gian đưa ra thị trường và chi phí vận hành.  
- **AgentCore cho các agent production:** Xử lý độ phức tạp vận hành bao gồm mở rộng, bảo mật và quan sát, cho phép các đội tập trung vào logic agent.  
- **Chiến lược tối ưu chi phí:** Hiểu mô hình định giá và triển khai chiến lược caching có thể giảm đáng kể chi phí suy luận AI.  
- **Bảo mật và tuân thủ:** Các dịch vụ AI của AWS được thiết kế với yêu cầu bảo mật doanh nghiệp, bao gồm quyền riêng tư dữ liệu và tuân thủ khu vực.

---

### Ứng Dụng Thực Tế

- Kiến trúc RAG và framework AgentCore có thể áp dụng trực tiếp cho các sáng kiến GenAI đã lên kế hoạch của chúng tôi, cung cấp bản thiết kế triển khai. Chúng ta có thể tận dụng các mẫu này để xây dựng trợ lý kiến thức nội bộ và chatbot hướng đến khách hàng.
- Làm quen sâu với danh mục dịch vụ AI của AWS giúp đưa ra quyết định kiến trúc tốt hơn và tạo mẫu nhanh hơn. Hiểu khả năng dịch vụ giúp chọn công cụ phù hợp cho từng trường hợp sử dụng.
- Các kỹ thuật prompt engineering có thể cải thiện ngay chất lượng và độ tin cậy của tính năng hỗ trợ AI, giảm nhu cầu tinh chỉnh mở rộng.
- Phương pháp tìm kiếm dựa trên embedding có thể nâng cao chức năng tìm kiếm hiện có của chúng ta, cải thiện trải nghiệm người dùng và khám phá nội dung.
- Các mẫu đa agent được trình diễn với AgentCore có thể áp dụng để tự động hóa các quy trình phức tạp hiện đang yêu cầu can thiệp thủ công.

### Những Điểm Nổi Bật Cá Nhân

Workshop **"GenAI-powered App-DB Modernization"** là một trải nghiệm học tập phong phú, thể hiện các chiến lược thực tế để hiện đại hóa các hệ thống cũ với công nghệ AI và cơ sở dữ liệu tiên tiến. Định dạng thực hành khuyến khích sự tham gia tích cực và chia sẻ kiến thức giữa những người tham dự. Các khoảnh khắc đáng chú ý bao gồm:

- Đạt top 5 trong cuộc thi Kahoot kết thúc và gặp gỡ các diễn giả để chụp ảnh, tạo cơ hội thảo luận về thách thức triển khai và các phương pháp hay nhất.
- Thành lập nhóm **"Mèo Cam Đeo Khăn"** bằng cách kết hợp tài năng từ nhóm "The Ballers" và "Vinhomies", thúc đẩy hợp tác và kết nối mạng lưới.
- Tham gia các cuộc thảo luận kỹ thuật với những người tham gia khác về thách thức triển khai AI thực tế và giải pháp.
- Thiết lập các kết nối có giá trị trong cộng đồng AWS sẽ tạo điều kiện thuận lợi cho việc trao đổi kiến thức và cơ hội hợp tác trong tương lai.

#### Bộ Sưu Tập Ảnh Sự Kiện
![Sự kiện 1 - Ảnh 1](/images/4-EventParticipated/event1-1.jpg)
![Sự kiện 1 - Ảnh 2](/images/4-EventParticipated/event1-2.jpg)
![Sự kiện 1 - Ảnh 3](/images/4-EventParticipated/event1-3.jpg)
