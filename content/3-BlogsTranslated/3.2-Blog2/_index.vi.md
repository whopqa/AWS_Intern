---
title: "Blog 2"
date: 2025-09-10
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---

# Tăng tương tác với nội dung bản địa hóa bằng Amazon Bedrock Flows
bởi Benjamin Le and Emilio Garcia Montano | ngày 01 Tháng 5 2025 | trong [Amazon Bedrock](https://aws.amazon.com/blogs/media/category/artificial-intelligence/amazon-machine-learning/amazon-bedrock/), [Amazon Bedrock Knowledge Bases](https://aws.amazon.com/blogs/media/category/artificial-intelligence/amazon-machine-learning/amazon-bedrock/amazon-bedrock-knowledge-bases/), [Amazon Bedrock Prompt Management](https://aws.amazon.com/blogs/media/category/artificial-intelligence/amazon-machine-learning/amazon-bedrock/amazon-bedrock-prompt-management/), [Amazon Machine Learning](https://aws.amazon.com/blogs/media/category/artificial-intelligence/amazon-machine-learning/), [Amazon Nova](https://aws.amazon.com/blogs/media/category/artificial-intelligence/amazon-machine-learning/amazon-bedrock/amazon-nova/), [Amazon Simple Storage Service (S3)](https://aws.amazon.com/blogs/media/category/storage/amazon-simple-storage-services-s3/), [Artificial Intelligence](https://aws.amazon.com/blogs/media/category/artificial-intelligence/), [Content Production](https://aws.amazon.com/blogs/media/category/industries/entertainment/content-production/), [Data Science & Analytics for Media](https://aws.amazon.com/blogs/media/category/industries/entertainment/data-science/), [Industries](https://aws.amazon.com/blogs/media/category/industries/), [Media & Entertainment](https://aws.amazon.com/blogs/media/category/industries/entertainment/), [Storage](https://aws.amazon.com/blogs/media/category/storage/) | [Permalink](https://aws.amazon.com/blogs/media/increase-engagement-with-localized-content-using-amazon-bedrock-flows/) | [Share](https://aws.amazon.com/blogs/media/increase-engagement-with-localized-content-using-amazon-bedrock-flows/)

Các nhà sản xuất và nhà xuất bản nội dung có các bộ sưu tập lớn với hàng ngàn, nếu không muốn nói hàng trăm ngàn bài viết có thể được bản địa hóa cho các khán giả và vùng địa lý mới để mang lại mức tương tác cao hơn tại các thị trường mới nổi và mới tiếp cận. Bản địa hóa nói chung là quá trình chuyển đổi nội dung (lựa chọn từ vựng, chuyển tông và dịch thuật) cho khán giả mới từ một vùng địa lý này sang vùng khác.

Việc bản địa hóa do con người thực hiện không thể mở rộng tới khối lượng cần thiết, vì vậy thường sử dụng dịch thuật tự động. Tuy nhiên, bản địa hóa tự động vẫn gặp khó khăn về chất lượng, đặc biệt trong khả năng đặt nội dung vào ngữ cảnh để hiểu được các sắc thái của từng thị trường cụ thể. Điều này thường dẫn đến nội dung có tỷ lệ tương tác thấp hơn từ người tiêu dùng khi so sánh với nội dung gốc. Với các mô hình nền tảng hỗ trợ nhiều ngôn ngữ và phương ngữ, khách hàng trong ngành truyền thông và giải trí ngày càng tận dụng AI tạo sinh (generative AI) để cung cấp nội dung bản địa hóa chất lượng cao hơn.

[Amazon Bedrock Flows](https://aws.amazon.com/bedrock/flows/) cung cấp một trình xây dựng trực quan, không cần mã (no-code visual builder) và một bộ API để liên kết liền mạch các mô hình nền tảng hàng đầu (SOTA) (như [Anthropic’s Claude](https://aws.amazon.com/bedrock/claude/) và [Amazon Nova](https://aws.amazon.com/ai/generative-ai/nova/)) trong [Amazon Bedrock](https://aws.amazon.com/bedrock/). Nó cũng tích hợp với các dịch vụ AWS khác để tự động hóa các workflow AI tạo sinh do người dùng định nghĩa, vượt xa việc chỉ gửi một prompt tới mô hình ngôn ngữ lớn.

[Amazon Bedrock Prompt Management](https://aws.amazon.com/bedrock/prompt-management/) cung cấp giao diện tinh gọn để tạo, đánh giá, quản lý phiên bản và chia sẻ các prompt. Nó giúp các nhà phát triển và kỹ sư prompt đạt được các phản hồi tốt nhất từ các mô hình nền tảng cho các trường hợp sử dụng của họ.

Chúng tôi sẽ trình bày cách bạn có thể tận dụng các tính năng của Amazon Bedrock (như Flows, Prompt Management và các mô hình nền tảng khác nhau) để nhanh chóng xây dựng và thử nghiệm một workflow. Workflow này sẽ lấy nội dung hiện có, cung cấp bản sao đã bản địa hóa và đưa ra đánh giá về những thay đổi để biên tập viên xem xét.

## Tổng quan kịch bản
Là một nhà xuất bản trực tuyến có kế hoạch mở rộng lượng người đọc sang các vùng địa lý và kênh mới mà không hoàn toàn phụ thuộc vào nội dung địa phương mới, bạn muốn tạo một workflow mà:

1. Bản địa hóa nội dung văn bản hiện có cho một quốc gia và ngôn ngữ cụ thể để phù hợp hơn với thị trường địa phương và chiến lược quảng cáo.
2. Điều chỉnh nội dung cho các kênh mới, đang nổi (như mạng xã hội dạng ngắn) sử dụng hướng dẫn phong cách (style guides) hiện được nạp vào [Amazon Bedrock Knowledge Bases](https://aws.amazon.com/bedrock/knowledge-bases/) để giúp các biên tập viên kiểm tra công việc của họ.
3. Cung cấp đánh giá dựa trên các chỉ số (như tính chính xác thực tế, độ dài, phương ngữ và thay đổi tổng thể về ý nghĩa) để biên tập viên có thể đưa ra lựa chọn thông minh để xuất bản hoặc thực hiện thay đổi thêm.
![Hình 1: Sơ đồ kiến trúc tổng quan phác thảo hệ thống quản lý nội dung kết hợp Amazon Bedrock Flows và Amazon Bedrock Knowledge Bases để bản địa hóa nội dung và cung cấp đánh giá hỗ trợ biên tập viên xuất bản nội dung mới.](/images/3-BlogsTranslated/3.2-Blog2/1.png)
*Hình 1: Sơ đồ kiến trúc tổng quan phác thảo hệ thống quản lý nội dung kết hợp Amazon Bedrock Flows và Amazon Bedrock Knowledge Bases để bản địa hóa nội dung và cung cấp đánh giá hỗ trợ biên tập viên xuất bản nội dung mới.*

## Yêu cầu trước
Trước khi tạo flow và các prompt, hãy đảm bảo bạn có thiết lập sau:

- Một tài khoản Amazon Web Services (AWS) và một người dùng có vai trò [IAM](https://aws.amazon.com/iam/) được ủy quyền sử dụng Amazon Bedrock. Để tham khảo, xem hướng dẫn [Getting started with Amazon Bedrock](https://docs.aws.amazon.com/bedrock/latest/userguide/getting-started.html). Đảm bảo vai trò đó bao gồm các quyền để sử dụng Flows và Prompt Management, như giải thích trong Prerequisites for [Amazon Bedrock Flows](https://docs.aws.amazon.com/bedrock/latest/userguide/flows-prereq.html) và [Prerequisites for prompt management](https://docs.aws.amazon.com/bedrock/latest/userguide/prompt-management-prereq.html).
- Truy cập các mô hình bạn chọn để gọi (invoke) và đánh giá (evaluate). Tham khảo [Manage access to Amazon Bedrock foundation models](https://docs.aws.amazon.com/bedrock/latest/userguide/model-access.html).
    - Ví dụ của chúng tôi sử dụng Amazon Nova Pro, [Cohere Command R, Cohere Embed Multilingual v3](https://aws.amazon.com/bedrock/cohere/) và các mô hình Anthropic’s Claude 3.7 Sonnet trong vùng Oregon (us-west-2)
- [Amazon Bedrock Knowledge Bases](https://docs.aws.amazon.com/bedrock/latest/userguide/knowledge-base.html) được cấu hình với nguồn dữ liệu [Amazon S3 (Amazon Simple Storage Service).](https://docs.aws.amazon.com/bedrock/latest/userguide/s3-data-source-connector.html)
  - Trong ví dụ này, knowledge base của chúng tôi đã chứa hướng dẫn phong cách về cách tạo nội dung cho mạng xã hội.


## Tạo các prompt
Trước khi tạo flow, bạn cần tạo hai prompt sẽ được sử dụng trong prompt flow sau này.

Prompt đầu tiên của chúng tôi bản địa hóa nội dung, và chúng tôi sử dụng mô hình nền tảng Anthropic’s Claude 3.7 Sonnet, hỗ trợ các ngôn ngữ như tiếng Anh, Pháp, Tây Ban Nha, Bồ Đào Nha, Nhật và các ngôn ngữ khác.

Khi tạo các prompt, các biến như bài viết (text article) được biểu diễn bằng {{article}} hoặc ngôn ngữ đích là {{language}} để cho phép các giá trị được tham chiếu giữa các nút flow khác nhau, cho phép linh hoạt và hiệu quả hơn.

![Hình 2: Prompt bản địa hóa nội dung (Content Localization)](/images/3-BlogsTranslated/3.2-Blog2/2.png)
*Hình 2: Prompt bản địa hóa nội dung (Content Localization)*


Prompt thứ hai đánh giá nội dung gốc và nội dung bản địa hóa để cung cấp đánh giá cho biên tập viên. Để đảm bảo tính độc lập với prompt bản địa hóa, prompt này sử dụng Amazon Nova Pro. Amazon Nova Pro là một mô hình đa phương thức (multimodal) rất mạnh với sự kết hợp tốt nhất về độ chính xác, tốc độ và chi phí cho nhiều nhiệm vụ — hỗ trợ hơn 200 ngôn ngữ.

![Hình 3: Prompt đánh giá nội dung (Content Evaluation)](/images/3-BlogsTranslated/3.2-Blog2/3.png)
*Hình 3: Prompt đánh giá nội dung (Content Evaluation)*

## Tạo và cấu hình flow
Sử dụng giao diện Amazon Bedrock console, điều hướng tới Flows dưới Builder Tools và tạo một flow mới như hiển thị trong Hình 4.

![Hình 4: Flow Amazon Bedrock có tên Content Localization, hiển thị tên, mô tả, ngày tạo, vai trò IAM sử dụng và một định danh flow duy nhất.](/images/3-BlogsTranslated/3.2-Blog2/4.png)
*Hình 4: Flow Amazon Bedrock có tên Content Localization, hiển thị tên, mô tả, ngày tạo, vai trò IAM sử dụng và một định danh flow duy nhất.*

Sau khi tạo, trình duyệt sẽ chuyển tới flow builder; nếu không, sử dụng “Edit in flow builder” để chuyển sang giao diện trực quan.

Trong Flow Builder, có các [node types](https://docs.aws.amazon.com/bedrock/latest/userguide/flows-nodes.html) khác nhau mà bạn có thể dùng để tạo flow. Bạn có thể kéo thả các node khác nhau lên canvas và tạo liên kết giữa chúng sau khi định nghĩa biến trong mỗi node hoặc bằng cách tải prompt đã lưu.

Trong ví dụ này, flow sau được tạo (Hình 5).
![Hình 5: Content localization flow.](/images/3-BlogsTranslated/3.2-Blog2/5.png) 
*Hình 5: Content localization flow.*

Bạn có thể xem các thiết lập cụ thể cho mỗi node bằng cách chọn node đó trong Flow Builder.

1. Để mô phỏng nội dung văn bản được gửi từ hệ thống quản lý nội dung (CMS), node Input của Flow chấp nhận một đối tượng JSON với các thuộc tính sau:


    1. article: văn bản bài viết được chọn để bản địa hóa


    2. country: quốc gia đích để bản địa hóa


    3. language: ngôn ngữ đích để bản địa hóa


    4. query: một prompt văn bản để truy vấn knowledge base lấy các hướng dẫn phong cách (style guide) liên quan

2. Sử dụng mô hình Cohere Command R, node Get_Style_Guides phân tích query text từ input và truy xuất các kết quả phù hợp từ knowledge base. Output từ node này bổ sung cách mà văn bản bản địa hóa được sinh ra.


3. Node Localization prompt sử dụng prompt đã tạo trước đó để bản địa hóa văn bản đầu vào.


4. Node Evaluation prompt sử dụng prompt đánh giá đã tạo trước đó để đánh giá văn bản gốc và bản địa hóa.

5. Hai node output của Flow sau đó truyền dữ liệu văn bản từ hai prompt node dưới dạng các sự kiện riêng biệt.


Các mô hình ngôn ngữ lớn (LLMs) có thể sinh ra thông tin không chính xác do hiện tượng “hallucinations”. Amazon Bedrock Flows tích hợp với [Amazon Bedrock Guardrails](https://docs.aws.amazon.com/bedrock/latest/userguide/flows-guardrails.html) để cho phép bạn cấu hình các biện pháp bảo vệ nhằm xác định, chặn hoặc lọc các phản hồi không mong muốn trong flow của bạn.

## Kiểm thử flow
Sử dụng bảng Test flow trong Flow Builder, bạn có thể nhanh chóng kiểm thử workflow hoàn chỉnh, với mỗi node output của flow truyền dữ liệu gần thời gian thực khi flow được thực thi. Để minh họa cách AI tạo sinh có thể làm việc với tiếng Tây Ban Nha qua các thị trường châu Âu và châu Mỹ Latinh, các ví dụ sau sử dụng cùng input text nhưng thay đổi quốc gia đích để bản địa hóa.

![Hình 6: Ví dụ về những đầu vào.](/images/3-BlogsTranslated/3.2-Blog2/6.png)
*Hình 6: Ví dụ về những đầu vào.*

![Hình 7: Văn bản bản địa hóa mẫu.](/images/3-BlogsTranslated/3.2-Blog2/7.png)
*Hình 7: Văn bản bản địa hóa mẫu.*

Trong bước cuối cùng, phần đánh giá sử dụng một mô hình nền tảng khác để độc lập so sánh nội dung gốc và nội dung bản địa hóa, cũng như cung cấp đánh giá có điểm số cho biên tập viên.

![Hình 8: Ví dụ về đánh giá nội dung.](/images/3-BlogsTranslated/3.2-Blog2/8.png)
*Hình 8: Ví dụ về đánh giá nội dung.*

## Giá
Amazon Bedrock Flows tính phí cho mỗi 1000 transitions cần thiết để thực thi workflow của bạn. Một transition xảy ra khi dữ liệu chuyển từ một node này sang node khác (ví dụ, một node input chuyển sang một prompt node). Không có phí bổ sung cho việc sử dụng Amazon Bedrock Prompt Management.

Phí sử dụng mô hình Amazon Bedrock sẽ khác nhau tùy theo loại mô hình được sử dụng và số lượng token đầu vào và đầu ra. Cần lưu ý rằng ví dụ trình diễn này cũng sử dụng Amazon Bedrock Knowledge Bases được cấu hình với cơ sở dữ liệu vector serverless [Amazon OpenSearch](https://aws.amazon.com/opensearch-service/serverless-vector-database/) và nguồn dữ liệu Amazon S3.

Giá sẽ khác nhau tùy theo AWS Region được sử dụng. Tất cả tài nguyên cho ví dụ minh họa của chúng tôi được cấu hình trong vùng Oregon (us-west-2). Tham khảo giá [Amazon Bedrock](https://aws.amazon.com/bedrock/pricing/), [Amazon S3](https://aws.amazon.com/s3/pricing/) và [Amazon OpenSearch Service](https://aws.amazon.com/opensearch-service/serverless-vector-database/) khi cần thiết.

## Kết luận
Chúng tôi đã minh chứng cách khách hàng trong ngành truyền thông và giải trí có thể cấu hình một workflow bản địa hóa bài viết sử dụng kiến trúc serverless, ít mã. Bằng cách sử dụng Amazon Bedrock Flows và Prompt Management, chủ sở hữu nội dung và biên tập viên có thể tận dụng lợi ích của generative AI để cung cấp nội dung hấp dẫn hơn cho khán giả mới.

Liên hệ với một [AWS Representative](https://pages.awscloud.com/Media-and-Entertainment-Contact-Us.html) để biết cách chúng tôi có thể giúp tăng tốc doanh nghiệp của bạn.

## Đọc thêm

- Amazon Bedrock Flows User Guide: [Build an end-to-end generative AI workflow with Amazon Bedrock Flows](https://docs.aws.amazon.com/bedrock/latest/userguide/flows.html)


- Amazon Bedrock Prompt Management User Guide: [Construct and store reusable prompts with Prompt management in Amazon Bedrock](https://docs.aws.amazon.com/bedrock/latest/userguide/prompt-management.html)


- [Amazon Bedrock Flows is now generally available with enhanced safety and traceability](https://aws.amazon.com/blogs/machine-learning/amazon-bedrock-flows-is-now-generally-available-with-enhanced-safety-and-traceability/)


- [Evaluating prompts at scale with Prompt Management and Prompt Flows for Amazon Bedrock](https://aws.amazon.com/blogs/machine-learning/evaluating-prompts-at-scale-with-prompt-management-and-prompt-flows-for-amazon-bedrock/)




