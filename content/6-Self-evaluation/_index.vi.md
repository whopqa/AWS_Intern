---
title: "Tự đánh giá"
date: 2025-09-10
weight: 6
chapter: false
pre: " <b> 6. </b> "
---


Trong suốt thời gian thực tập tại **First Cloud Journey (FCJ)** từ **08/09/2025** đến **07/12/2025**, tôi đã có cơ hội học hỏi, rèn luyện và áp dụng kiến thức về AWS Cloud vào môi trường làm việc thực tế.

Tôi đã tham gia **thiết kế và phát triển hệ thống AI Chatbot sử dụng Amazon Bedrock, Lambda, RDS PostgreSQL, DynamoDB và các dịch vụ AWS khác**, qua đó cải thiện kỹ năng **phát triển full-stack với AWS CDK, prompt engineering, kiến trúc hệ thống AI, xử lý dữ liệu, và tối ưu hóa chi phí cloud**.

**Kiến thức AI và Machine Learning đã áp dụng:**
* **Amazon Bedrock & Large Language Models (LLM):** Sử dụng Claude 3 Haiku và Claude 3.5 Sonnet để xây dựng chatbot hội thoại thông minh, xử lý ngôn ngữ tự nhiên tiếng Việt.
* **Prompt Engineering:** Thiết kế và tối ưu các prompt chuyên biệt cho phân loại intent, trích xuất thông tin, sinh SQL query, và tạo response theo context. Áp dụng Few-shot Learning và Reflection technique để cải thiện độ chính xác.
* **Vector Search & Embeddings:** Sử dụng embedding models để chuyển đổi text thành vector, xây dựng cơ chế tìm kiếm schema và cache câu hỏi dựa trên cosine similarity.
* **Retrieval-Augmented Generation (RAG):** Nghiên cứu và áp dụng kiến trúc RAG kết hợp Amazon Kendra, LangChain agent, và knowledge base để chatbot trả lời dựa trên nguồn dữ liệu doanh nghiệp.
* **Text-to-SQL Generation:** Xây dựng pipeline chuyển đổi câu hỏi tự nhiên thành SQL query, kết hợp context awareness và schema annotation để tăng độ chính xác.
* **Session Management & Context Window:** Thiết kế cơ chế quản lý ngữ cảnh hội thoại với Rolling Summary, giới hạn token, và cache để tối ưu chi phí API LLM.
* **Model Selection & Cross-Region Inference:** So sánh và lựa chọn model phù hợp (Haiku vs Sonnet), cân bằng giữa chất lượng và latency khi sử dụng cross-region.

**Nền tảng kiến thức AWS quan trọng:**
* **Compute & Serverless:** Lambda, API Gateway, EventBridge, SQS - xây dựng kiến trúc event-driven và xử lý throttling/timeout.
* **Database:** RDS PostgreSQL (ACID, transaction, unaccent extension), DynamoDB (NoSQL, session storage), Vector Search.
* **Storage:** S3 (static website, lifecycle, versioning), Storage Gateway, FSx.
* **Networking:** VPC, Subnet, Security Group, NAT Gateway, Transit Gateway, Site-to-Site VPN, Route 53 Resolver.
* **Security & IAM:** IAM User/Role/Policy, Permission Boundary, KMS encryption, Security Hub, Cognito, Organizations, Identity Center.
* **Infrastructure as Code:** AWS CDK (TypeScript) để triển khai toàn bộ stack: Text2SQL, Webhook, Database, Networking theo mô hình decoupling.
* **Monitoring & Cost Optimization:** CloudWatch, Budget, Cost Explorer, auto start/stop EC2, giảm VPC Endpoint không cần thiết.
* **Data Analytics:** Data Lake, Athena, Glue, QuickSight, Redshift, ElastiCache.

**Trải nghiệm và bài học quý giá:**

Chương trình thực tập tại FCJ không chỉ trang bị kiến thức kỹ thuật mà còn mang lại những trải nghiệm thực tế vô cùng giá trị:

* **Môi trường làm việc chuyên nghiệp:** Được làm quen với văn hóa làm việc theo chuẩn doanh nghiệp công nghệ, hiểu rõ quy trình phát triển sản phẩm từ research, design, development đến deployment và monitoring. Học cách làm việc với các công cụ quản lý dự án, version control (Git), documentation (Notion), và best practices trong team collaboration.

* **Góc nhìn thực tế về Cloud Architecture:** Được hình dung rõ hơn cách các dự án thực tế trong doanh nghiệp được triển khai trên AWS - từ việc chọn dịch vụ phù hợp, thiết kế kiến trúc scalable và cost-effective, xử lý các vấn đề production như throttling/timeout/security, đến việc optimize performance và monitor hệ thống. Hiểu được sự khác biệt giữa "làm lab" và "làm dự án thực tế" - nơi phải cân nhắc nhiều yếu tố như business logic, user experience, cost, security, và maintainability.

* **Học hỏi từ cộng đồng:** Được học tập từ những người bạn giỏi trong chương trình - mỗi người đều có điểm mạnh riêng về frontend, backend, DevOps, hoặc AI/ML. Việc code review, discuss architecture, và pair programming giúp mở rộng tư duy và học được nhiều cách tiếp cận khác nhau cho cùng một vấn đề.

* **Mentorship từ người có kinh nghiệm:** Được các anh mentor hướng dẫn tận tình về technical skills, design thinking, và problem-solving approach. Những câu hỏi "tại sao lại chọn giải pháp này?", "có cách nào tốt hơn không?", "scale lên 1000x user thì sao?" giúp tôi suy nghĩ sâu hơn và tránh những sai lầm phổ biến. Học được cách đọc documentation hiệu quả, debug systematically, và quan trọng nhất là mindset "always learning" trong ngành công nghệ.

* **Kỹ năng mềm:** Cải thiện khả năng trình bày ý tưởng, viết proposal, làm demo, và nhận feedback một cách xây dựng. Học cách quản lý thời gian khi làm nhiều task song song và xử lý pressure khi gặp bug critical trước deadline.

Về tác phong, tôi luôn cố gắng hoàn thành tốt nhiệm vụ, chủ động tìm hiểu và nghiên cứu công nghệ mới, và tích cực trao đổi với đồng nghiệp để nâng cao hiệu quả công việc.

Để phản ánh một cách khách quan quá trình thực tập, tôi xin tự đánh giá bản thân dựa trên các tiêu chí dưới đây:


| STT | Tiêu chí                            | Mô tả                                                                                            | Tốt | Khá | Trung bình |
| --- | ----------------------------------- | ------------------------------------------------------------------------------------------------ | --- | --- | ---------- |
| 1   | **Kiến thức và kỹ năng chuyên môn** | Hiểu biết về ngành, áp dụng kiến thức vào thực tế, kỹ năng sử dụng công cụ, chất lượng công việc | ✅   | ☐   | ☐          |
| 2   | **Khả năng học hỏi**                | Tiếp thu kiến thức mới, học hỏi nhanh                                                            | ☐   | ✅   | ☐          |
| 3   | **Chủ động**                        | Tự tìm hiểu, nhận nhiệm vụ mà không chờ chỉ dẫn                                                  | ✅   | ☐   | ☐          |
| 4   | **Tinh thần trách nhiệm**           | Hoàn thành công việc đúng hạn, đảm bảo chất lượng                                                | ✅   | ☐   | ☐          |
| 5   | **Kỷ luật**                         | Tuân thủ giờ giấc, nội quy, quy trình làm việc                                                   | ☐   | ✅   |  ☐         |
| 6   | **Tính cầu tiến**                   | Sẵn sàng nhận feedback và cải thiện bản thân                                                     | ☐   | ✅   | ☐          |
| 7   | **Giao tiếp**                       | Trình bày ý tưởng, báo cáo công việc rõ ràng                                                     | ☐   | ✅   | ☐          |
| 8   | **Hợp tác nhóm**                    | Làm việc hiệu quả với đồng nghiệp, tham gia nhóm                                                 | ✅   | ☐   | ☐          |
| 9   | **Ứng xử chuyên nghiệp**            | Tôn trọng đồng nghiệp, đối tác, môi trường làm việc                                              | ✅   | ☐   | ☐          |
| 10  | **Tư duy giải quyết vấn đề**        | Nhận diện vấn đề, đề xuất giải pháp, sáng tạo                                                    | ✅  | ☐   | ☐          |
| 11  | **Đóng góp vào dự án/tổ chức**      | Hiệu quả công việc, sáng kiến cải tiến, ghi nhận từ team                                         | ✅   | ☐   | ☐          |
| 12  | **Tổng thể**                        | Đánh giá chung về toàn bộ quá trình thực tập                                                     | ✅   | ☐   | ☐          |

### Cần cải thiện

* **Kỷ luật và quản lý thời gian:** Tăng cường chấp hành nghiêm chỉnh nội quy, giờ giấc làm việc và deadline của dự án.
* **Tư duy giải quyết vấn đề:** Cải thiện khả năng phân tích vấn đề phức tạp, tách bài toán lớn thành các bước nhỏ hơn, và đưa ra giải pháp tối ưu nhanh chóng.
* **Kỹ năng giao tiếp:** Học cách trình bày ý tưởng rõ ràng hơn, chủ động báo cáo tiến độ, và xử lý các tình huống khó khăn trong làm việc nhóm một cách chuyên nghiệp.


### Những bài học quan trọng từ dự án AI Chatbot

* **Temperature của model ảnh hưởng lớn đến độ chính xác** của thông tin trích xuất - cần điều chỉnh cẩn thận cho từng use case.
* **Gộp nhiều prompt thành một** giúp giảm số lần gọi API, tăng tính nhất quán và tiết kiệm chi phí.
* **Vector search cần fine-tune cẩn thận** với annotation và similarity threshold để đạt kết quả tốt nhất.
* **Cross-region inference là trade-off** giữa model quality và latency - cần cân bằng theo yêu cầu thực tế.
* **SQS là giải pháp hiệu quả** cho vấn đề throttling và timeout trong serverless architecture.
* **Xử lý tiếng Việt cần extension unaccent** trong PostgreSQL để tìm kiếm không dấu chính xác.
* **Business logic ràng buộc rất quan trọng** để tránh data không hợp lệ và đảm bảo tính toàn vẹn dữ liệu.
* **Decoupling architecture** giúp code dễ maintain, test và scale - áp dụng Service pattern tách biệt Session, Bedrock, Database, Messenger.
* **Context window management** quyết định chi phí và performance - Rolling Summary và cache strategy là chìa khóa.
* **Prompt engineering là nghệ thuật** đòi hỏi nhiều thử nghiệm và hiểu sâu về business logic - Few-shot Learning và Reflection technique cải thiện đáng kể độ chính xác.