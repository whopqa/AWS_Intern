---
title: "Blog 3"
date: 2025-09-10
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---

# Đổi mới với tốc độ: Giải pháp AI tạo sinh của BMW cho phân tích sự cố đám mây
bởi Johann Wildgruber, Dr. Jens Kohl, Thilo Bindel, Luisa-Sophie Gloger, Aishwarya Lakshmi Krishnan, Huong Vu, Kim Robins, Otto Kruse, Satyam Saxena, and Tanrajbir Takher | ngày 05 THÁNG 3 2025 | trong [Advanced (300)](https://aws.amazon.com/blogs/machine-learning/category/learning-levels/advanced-300/), [Amazon Bedrock](https://aws.amazon.com/blogs/machine-learning/category/artificial-intelligence/amazon-machine-learning/amazon-bedrock/), [Amazon Bedrock Agents](https://aws.amazon.com/blogs/machine-learning/category/artificial-intelligence/amazon-machine-learning/amazon-bedrock/amazon-bedrock-agents/), [Amazon CloudWatch](https://aws.amazon.com/blogs/machine-learning/category/management-tools/amazon-cloudwatch/), [Artificial Intelligence](https://aws.amazon.com/blogs/machine-learning/category/artificial-intelligence/), [AWS CloudTrail](https://aws.amazon.com/blogs/machine-learning/category/management-tools/aws-cloudtrail/), [Customer Enablement](https://aws.amazon.com/blogs/machine-learning/category/customer-enablement/), [Customer Solutions](https://aws.amazon.com/blogs/machine-learning/category/post-types/customer-solutions/) | [Permalink](https://aws.amazon.com/blogs/machine-learning/innovating-at-speed-bmws-generative-ai-solution-for-cloud-incident-analysis/) | [Comments](https://aws.amazon.com/blogs/machine-learning/innovating-at-speed-bmws-generative-ai-solution-for-cloud-incident-analysis/#Comments) | [Share](https://aws.amazon.com/blogs/machine-learning/innovating-at-speed-bmws-generative-ai-solution-for-cloud-incident-analysis/)

<i>Bài viết này được đồng tác giả cùng với Johann Wildgruber, Tiến sĩ Jens Kohl, Thilo Bindel và Luisa-Sophie Gloger từ Tập đoàn BMW.</i>

Tập đoàn [BMW Group](https://www.bmwgroup.com/) — có trụ sở chính tại Munich, Đức — là nhà sản xuất xe hơi với hơn 154.000 nhân viên, cùng 30 nhà máy sản xuất và lắp ráp trên toàn cầu, cũng như các trung tâm nghiên cứu và phát triển (R&D) tại 17 quốc gia. Ngày nay, BMW Group (BMW) là nhà sản xuất hàng đầu thế giới về xe hơi và xe máy cao cấp, đồng thời cung cấp các dịch vụ tài chính và di động cao cấp.

[BMW Connected Company](https://www.bmwusa.com/explore/connecteddrive.html) là một bộ phận trong BMW, chịu trách nhiệm phát triển và vận hành các dịch vụ số cao cấp cho đội xe kết nối (connected fleet) của BMW, hiện có hơn 23 triệu phương tiện trên toàn cầu. Các dịch vụ số này được nhiều chủ xe BMW sử dụng hàng ngày — ví dụ: khóa hoặc mở cửa xe từ xa qua ứng dụng di động, khởi động chế độ sưởi kính trước từ xa, mua bản đồ định vị mới từ menu trên xe, hoặc nghe nhạc trực tuyến qua Internet trong xe.

Trong bài viết này, chúng tôi giải thích cách BMW sử dụng công nghệ Generative AI trên AWS để giúp vận hành các dịch vụ số này với độ khả dụng cao (high availability). Cụ thể, BMW sử dụng [Amazon Bedrock Agents](https://aws.amazon.com/bedrock/agents/) để rút ngắn thời gian khắc phục các sự cố dịch vụ (service outages) bằng cách tự động hóa quy trình Root Cause Analysis (RCA) vốn tốn nhiều thời gian. Agent RCA hoàn toàn tự động có thể xác định đúng nguyên nhân gốc rễ trong khoảng 85% trường hợp, và hỗ trợ kỹ sư trong việc hiểu hệ thống và có cái nhìn theo thời gian thực (real-time insights). Hiệu quả này được xác thực qua giai đoạn Proof of Concept (POC), khi việc sử dụng RCA Agent trên các trường hợp đại diện cho thấy thời gian chẩn đoán giảm đáng kể, minh chứng rõ ràng lợi ích của giải pháp này.

## Thách thức trong phân tích nguyên nhân gốc rễ của sự cố
Các dịch vụ số thường được triển khai bằng cách kết hợp nhiều thành phần phần mềm lại với nhau; các thành phần này có thể được xây dựng và vận hành bởi những đội ngũ khác nhau.Ví dụ, hãy xem xét dịch vụ mở và khóa cửa xe từ xa. Có thể có một đội phát triển và vận hành ứng dụng iOS, một đội khác cho ứng dụng Android, một đội xây dựng và vận hành lớp backend-for-frontend được cả hai ứng dụng sử dụng, và tương tự như vậy.Hơn nữa, các đội ngũ này có thể phân tán về mặt địa lý và vận hành khối lượng công việc của họ ở các địa điểm và vùng khác nhau; nhiều đội chạy trên AWS, số khác chạy ở nơi khác.

Giả sử một tình huống (giả định) khi nhiều chủ xe báo rằng họ không thể khóa cửa xe từ xa bằng ứng dụng. Liệu nguyên nhân đến từ ứng dụng iOS, hay từ backend-for-frontend?
Có phải firewall rule (quy định tường lửa)  nào đó bị thay đổi? Chứng chỉ TLS nội bộ có hết hạn không? Hệ thống MQTT có đang gặp trễ không? Một thay đổi API gần đây có gây lỗi không tương thích (breaking change)? Hay mật khẩu cơ sở dữ liệu của dịch vụ trung tâm lại bị xoay lần nữa?

Việc xác định nguyên nhân gốc trong các tình huống như vậy là rất khó khăn. Nó yêu cầu kiểm tra nhiều hệ thống, nhiều nhóm, nhiều trong số đó có thể đang lỗi do chúng phụ thuộc lẫn nhau. Các kỹ sư phải hiểu rõ kiến trúc hệ thống, đưa ra giả thuyết, rồi lần theo chuỗi các thành phần cho đến khi tìm ra thủ phạm thực sự — đôi khi phải quay lại và thay đổi giả thuyết ban đầu.

Những khó khăn này cho thấy nhu cầu về một phương pháp RCA hiệu quả, mạnh mẽ và tự động hơn. Trong bối cảnh đó, hãy khám phá mà thế nào BMW và AWS đã hợp tác phát triển một giải pháp sử dụng Amazon Bedrock Agents để tăng tốc và tinh gọn quy trình RCA. 

## Tổng quan giải pháp
Ở cấp độ tổng quát, giải pháp sử dụng Amazon Bedrock Agent để tự động hóa quy trình RCA. Agent này có nhiều công cụ (tools) tùy chỉnh được xây dựng riêng để phục vụ nhiệm vụ của nó. Các công cụ này được triển khai dưới dạng [AWS Lambda](https://aws.amazon.com/lambda/) functions, và sử dụng dịch vụ như [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/) và [AWS CloudTrail](https://aws.amazon.com/cloudtrail/) để phân tích log và metric của hệ thống. Biểu đồ dưới đây minh hoạ kiến trúc của giải pháp.
![Kiến trúc giải pháp sử dụng Amazon Bedrock Agents để tự động hóa quy trình RCA.](/images/3-BlogsTranslated/3.3-Blog3/1.png)

Khi xảy ra sự cố, kỹ sư trực (on-call engineer) mô tả vấn đề cho Amazon Bedrock Agent.
Agent bắt đầu điều tra nguyên nhân gốc rễ, sử dụng các công cụ để thực hiện những nhiệm vụ mà kỹ sư thường làm thủ công — như tìm kiếm trong log. Dựa trên các dấu hiệu thu được, agent đưa ra một số giả thuyết và trình bày với kỹ sư. Kỹ sư có thể tự khắc phục sự cố hoặc hướng dẫn agent tiếp tục điều tra sâu hơn. Trong phần tiếp theo, hãy đi sâu hơn vào các công cụ mà agent sử dụng.

## Các công cụ của Amazon Bedrock Agent
Hiệu quả của Amazon Bedrock Agent trong RCA nằm ở khả năng tích hợp linh hoạt các công cụ tùy chỉnh. Các công cụ này, được triển khai dưới dạng Lambda functions, tận dụng các dịch vụ AWS như CloudWatch và CloudTrail để tự động hóa các tác vụ thủ công tốn thời gian. Bằng cách tổ chức những tính năng của chúng vào trong một công cụ, Amazon Bedrock Agent đảm bảo phân tích lỗi gốc nhanh và chính xác.

**Architecture Tool**
Architecture Tool sử dụng [C4 diagrams](https://c4model.com/) (được nâng cấp bằng [Structurizr](https://structurizr.com/)) để cung cấp cái nhìn toàn cảnh về kiến trúc hệ thống — bao gồm quan hệ giữa các thành phần, phụ thuộc và luồng công việc. Điều này giúp agent khoanh vùng khu vực có khả năng lỗi cao nhất, dựa trên mối tương tác giữa các hệ thống.

Ví dụ: nếu sự cố ảnh hưởng đến một service cụ thể, Architecture Tool có thể xác định các phụ thuộc upstream hoặc downstream và gợi ý các giả định để tập trung phân tích. Việc này thúc đẩy chẩn đoán bằng việc cho phép agents suy luận ngữ cảnh về kiến trúc hệ thống thay vì phải duyệt log hay metrics một cách mù quáng.

**Logs Tool**
Logs Tool sử dụng CloudWatch Logs Insights để phân tích log theo thời gian thực.
Bằng cách phát hiện pattern, lỗi, hoặc bất thường, cũng như so sánh xu hướng với giai đoạn trước, nó giúp agent nhanh chóng xác định sự kiện bất thường như lỗi xác thực, crash, hoặc timeout.

Ví dụ: nếu có lỗi truy cập database, Logs Tool có thể phát hiện sự tăng đột biến của thông điệp “FATAL: password authentication failed” — gợi ý nguyên nhân có thể là mật khẩu database bị rotate sai.

**Metrics Tool**
Metrics Tool cung cấp cho agent khả năng theo dõi sức khỏe hệ thống theo thời gian thực qua CloudWatch metrics. Công cụ này phát hiện các bất thường thống kê trong các chỉ số như latency, error rate, resource utilization,… — thường là dấu hiệu sớm của vấn đề.

Ví dụ: trong trường hợp Kubernetes memory overload, công cụ này phát hiện mức sử dụng bộ nhớ tăng mạnh hoặc phân bổ tài nguyên bất thường trước khi xảy ra lỗi, giúp agent khoanh vùng vấn đề về resource mismanagement hoặc load spike để việc kiểm tra giải quyết vấn đề hiệu quả hơn.

**Infrastructure Tool**
Infrastructure Tool sử dụng dữ liệu CloudTrail để phân tích các sự kiện control-plane, như thay đổi cấu hình, cập nhật security group, hoặc API call. Công cụ này rất hiệu quả trong việc phát hiện misconfiguration hoặc breaking change gây ra lỗi lan truyền.

Ví dụ: nếu một ingress rule trong security group bị xóa nhầm gây vấn đề kết nối giữa các dịch vụ. Công cụ này sẽ phát hiện và liên kết sự kiện đó với sự cố kết nối, giúp agent nhanh chóng chỉ ra nguyên nhân.

Bằng cách kết hợp các công cụ này, Amazon Bedrock Agent mô phỏng quy trình suy luận từng bước của kỹ sư có kinh nghiệm, nhưng thực hiện ở tốc độ máy. Cấu trúc module của hệ thống cho phép linh hoạt tùy chỉnh, phù hợp với hạ tầng đám mây phức tạp và đa vùng của BMW.

## Amazon Bedrock Agents: ReAct Framework trong hành động
Cốt lõi của quy trình RCA nhanh của BMW là ReAct (Reasoning + Action) Framework — một cách tiếp cận kết hợp lý luận logic với thực thi hành động. Bằng cách tích hợp ReAct với Amazon Bedrock, BMW có được một giải pháp linh hoạt để chẩn đoán và khắc phục sự cố trong môi trường đám mây phức tạp. Khác với các quy trình tĩnh truyền thống, ReAct Agent dựa vào dữ liệu thời gian thực và đưa ra quyết định lặp lại (iterative decision-making) để thích ứng với từng tình huống.

 Giải pháp ReAct agent trong BMW’s RCA dùng quy trình cấu trúc nhưng linh hoạt để chẩn đoán. Đầu tiên, khi nhận mô tả sự cố (ví dụ: “Vehicle doors cannot be locked via the app”), agent xác định thành phần nào của hệ thống có khả năng bị ảnh hưởng. Sau đó, cơ chế tư duy lặp lại của ReAct framework sẽ chỉ agent gọi các công cụ chuyên dụng để thu thập bằng chứng (evidence) từ hệ thống giám sát đa tài khoản (cross-account observability).
Qua mỗi vòng đánh giá, agent thu hẹp dần phạm vi cho đến khi xác định được nguyên nhân gốc — như chứng chỉ hết hạn, firewall bị thu hồi, hoặc spike lưu lượng. Dưới đây là biểu đồ biểu diễn workflow.

<video width="100%" controls>
  <source src="/images/3-BlogsTranslated/3.3-Blog3/react-flow.mp4" type="video/mp4">
</video>


Lợi ích của ReAct Framework:
- Động và thích ứng: ReAct agent điều chỉnh quy trình dựa trên từng sự cố cụ thể thay vì phương pháp one-size-fits-all. Việc thích ứng này rất quan trọng với kiến trúc đa vùng, đa dịch vụ của BMW.


- Hiệu quả: Bằng cách suy luận công cụ nào nên dùng khi nào giúp giảm truy vấn dư thừa, tối ưu thời gian chẩn đoán.


- Suy luận giống con người: Mô phỏng quy trình tư duy của kỹ sư giàu kinh nghiệm, khám phá các giả thuyết đến khi tìm ra vấn đề gốc nhưng ở tốc độ máy.

Nhờ ReAct, BMW giảm đáng kể thời gian chẩn đoán, tăng hiệu quả vận hành, và giúp kỹ sư tập trung vào chiến lược hơn là thao tác thủ công.

## Case Study: RCA cho sự cố “Unlocking vehicles via the iOS app”
Để minh họa sức mạnh của Amazon Bedrock Agents, hãy xem xét một tình huống thực tế gồm tương tác giữa BMW’s connected fleet và dịch vụ kỹ thuật số chạy lên cloud backend

Trong thử nghiệm, nhóm kỹ sư thay đổi security group của tài khoản mạng trung tâm trong môi trường test. Kết quả: yêu cầu từ fleet bị chặn và không đến được dịch vụ hosted trong backend, và người dùng test không thể khóa/mở xe từ xa.

**Chi tiết sự cố**

Kỹ sư BMW nhận báo cáo rằng tính năng khóa/mở xe từ xa trong app không hoạt động.

Câu hỏi đặt ra: lỗi ở app, backend-for-frontend, hay hệ thống MQTT / chứng thực?

**Cách ReAct Agent xử lý**
Vấn đề được mô tả cho tác nhân Amazon Bedrock ReAct: ‘Người dùng ứng dụng iOS không thể mở khóa cửa xe từ xa.’ Agent lập tức bắt đầu phân tích:

1. Gọi Architecture Tool để hiểu cấu trúc hệ thống. Phát hiện: iOS app kết nối đến backend-for-frontend API, và API này giao tiếp các nội bộ APIs khác như Remote Vehicle Management API. Remote Vehicle Management API có trách nhiệm gửi lệnh tới ô tô qua MQTT
2. Agents sử dụng các tools khác để xử lý một cách có mục tiêu: quét logs, metrics và các hoạt động bảng điều khiển liên quan tới lỗi không thể mở khoá xe từ xa. Phát hiện:


      a. Log bất thường biểu thị lỗi kết nối (network timeout).


      b. Giảm đột ngột số lượng invocation thành công của Remote Vehicle Management API.


      c. Thay đổi trong security groups ở tài khoản mạng trung tâm.
3. Kết luận: Giải thiết đầu tiên là nguyên nhân gốc: Security group bị thay đổi nhầm ở tài khoản trung tâm khiến lưu lượng giữa BFF và Remote Vehicle Management API bị chặn. Agent đã liên hệ chính xác giữa logs ( lỗi hết thời gian chờ khi lấy dữ liệu), metrics(giảm lượt gọi) và bảng điều khiển bị thay đổi (ingress rule thay đổi trong SG)
4. Nếu kĩ sư sẵn có muốn thêm thông tin khác, họ có thể đặt thêm các câu hỏi tới agent hoặc hướng dẫn tra khảo chỗ nào khác

Tất cả quá trình chỉ tốn vài phút so với hàng giờ ở phương pháp RCA cũ. ReAct agent có thể chủ động suy luận, kết nối data từ tài khoản quan sát khác nhau và lặp lại theo giả thuyết của nó đã giảm bớt đi các kiểm tra dư thừa thông thường.
<video width="100%" controls>
  <source src="/images/3-BlogsTranslated/3.3-Blog3/ios+issue+BMW-truncated.mp4" type="video/mp4">
</video>

## Kết luận
Bằng việc sử dụng Amazon Bedrock ReAct Agents, BMW đã biến quy trình RCA thủ công phức tạp thành quy trình tự động, nhanh và chính xác. Các công cụ tích hợp trong ReAct Framework giúp thu hẹp không gian suy luận, tạo giả thuyết động và chẩn đoán chính xác, mô phỏng kỹ sư kỳ cựu nhưng hoạt động ở tốc độ máy. Đổi mới này giúp giảm thời gian có xác định và giải quyết gián đoạn dịch vụ, từ đó nâng cao hơn độ tin cậy của dịch vụ kết nối BMW, cải thiện trải nghiệm hàng triệu khách hàng trên toàn thế giới.

Giải pháp đã chứng minh hiệu quả rõ ràng, khi agent xác định được nguyên nhân gốc rễ trong 85% trường hợp thử nghiệm và cung cấp những phân tích chi tiết cho phần còn lại, giúp rút ngắn đáng kể thời gian điều tra của kỹ sư. Bằng cách giảm rào cản cho các kỹ sư trẻ, giải pháp cho phép những thành viên ít kinh nghiệm hơn cũng có thể chẩn đoán vấn đề một cách hiệu quả, đồng thời duy trì độ tin cậy và khả năng mở rộng trên toàn bộ hoạt động của BMW.

Việc tích hợp AI tạo sinh vào quy trình RCA cho thấy tiềm năng mang tính chuyển đổi của AI trong các hoạt động hiện đại dựa trên đám mây.Khả năng thích ứng linh hoạt, suy luận theo ngữ cảnh và xử lý các hạ tầng phức tạp đa vùng khiến Amazon Bedrock Agents trở thành một bước ngoặt cho các tổ chức muốn duy trì mức độ sẵn sàng cao cho dịch vụ số của họ.

Khi BMW tiếp tục mở rộng đội xe kết nối và các dịch vụ số của mình, việc áp dụng các giải pháp dựa trên AI tạo sinh như Amazon Bedrock sẽ đóng vai trò quan trọng trong việc duy trì hiệu quả vận hành và cung cấp trải nghiệm liền mạch cho khách hàng. Bằng cách học theo ví dụ của BMW, tổ chức của bạn cũng có thể tận dụng Amazon Bedrock Agents cho phân tích nguyên nhân gốc rễ nhằm tăng độ tin cậy của dịch vụ.

Bắt đầu bằng cách khám phá [Amazon Bedrock Agents](https://aws.amazon.com/bedrock/agents/) để tối ưu hóa việc chẩn đoán sự cố hoặc sử dụng [CloudWatch Logs Insights](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/AnalyzingLogData.html) để xác định bất thường trong log hệ thống của bạn. Nếu bạn muốn tìm hiểu thực hành cách tạo các Amazon Bedrock agent của riêng mình — bao gồm ví dụ mã nguồn và các best practice — hãy xem [repo GitHub](https://github.com/awslabs/amazon-bedrock-agent-samples/) sau. Những công cụ này đang thiết lập một tiêu chuẩn mới trong ngành cho RCA hiệu quả và vận hành xuất sắc.

