---
title: "Blog 1"
date: 2025-09-10
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# Cải thiện độ chính xác cho ngân sách đám mây của bạn với các tính năng mới trong AWS Budgets
bởi Fredrik Tunvall | vào ngày 29 THÁNG 4 2025 | trong **[Announcements](https://aws.amazon.com/blogs/aws-cloud-financial-management/category/post-types/announcements/), [AWS Budgets](https://aws.amazon.com/blogs/aws-cloud-financial-management/category/aws-cloud-financial-management/aws-budgets/), [AWS Cloud Financial Management](https://aws.amazon.com/blogs/aws-cloud-financial-management/category/aws-cloud-financial-management/) | [Permalink](https://aws.amazon.com/blogs/aws-cloud-financial-management/improving-accuracy-for-your-cloud-budgeting-with-new-features-in-aws-budgets/) | [Share](https://aws.amazon.com/blogs/aws-cloud-financial-management/improving-accuracy-for-your-cloud-budgeting-with-new-features-in-aws-budgets/)**

Hôm nay, AWS công bố các khả năng mới trong [AWS Budgets](https://aws.amazon.com/aws-cost-management/aws-budgets/) giúp bạn linh hoạt hơn trong cách theo dõi và quản lý chi tiêu AWS của mình. Những cải tiến này bao gồm:

- Hỗ trợ các chỉ số chi phí bổ sung: net unblended costs và net amortized costs
- Khả năng loại trừ các giá trị chiều cụ thể khi tạo ngân sách (như dịch vụ, tài khoản và loại instance)
- Khả năng lọc mới cho các loại phí giúp kiểm soát chi tiết để bao gồm hoặc loại trừ [AWS Savings Plans](https://aws.amazon.com/savingsplans/) (SPs) hoặc chi phí trả trước của Reservation (RI) (gói đặt trước tài nguyên), phí định kỳ, thuế và tín dụng
- Chức năng API được cải thiện hỗ trợ filter expressions (biểu thức lọc) tương thích với AWS [Cost Explorer](https://aws.amazon.com/aws-cost-management/aws-budgets/)

Những cải tiến này cho phép bạn tạo ngân sách phản ánh tốt hơn chi phí thực tế của bạn, bao gồm các khoản chiết khấu, và cung cấp kiểm soát chi tiết hơn về những gì được bao gồm trong tính toán ngân sách. Chúng cũng cho phép bạn tạo ngân sách với các lựa chọn bộ lọc phù hợp với AWS Cost Explorer.

## Khả năng nâng cao để theo dõi chi phí chính xác hơn
Các khả năng mới trong AWS Budgets mang lại cải tiến đáng kể về độ chính xác và linh hoạt trong việc theo dõi chi phí. Bằng việc hỗ trợ các chỉ số net unblended (chi phí thực tế sau khi áp dụng mức giá riêng cho từng tài khoản, chưa tính gộp) và net amortized cost (chi phí phân bổ theo thời gian, thường bao gồm chi phí trả trước của Reserved Instances hoặc Savings Plans), bạn có thể tạo ngân sách phù hợp chính xác với chi tiêu thực tế của bạn, bao gồm tất cả các chiết khấu áp dụng. Cải tiến này đặc biệt quan trọng đối với các công ty sử dụng Savings Plans hoặc Reserved Instances, vì nó cho phép lên kế hoạch ngân sách và theo dõi chính xác hơn.

Sự ra mắt của khả năng lọc nâng cao, bao gồm khả năng loại trừ các giá trị chiều cụ thể, mở ra các khả năng mới để giám sát chi phí chính xác. Những tính năng này cho phép nhiều trường hợp sử dụng mạnh mẽ mà trước đây khó thực hiện, chẳng hạn:

- **Kiểm soát chi phí chi tiết**: Tạo ngân sách mục tiêu giờ đây dễ dàng hơn nhiều. Ví dụ: bạn có thể dễ dàng loại bỏ chi phí chia sẻ hạ tầng khi thiết lập ngân sách cho các sáng kiến nghiên cứu cụ thể, cung cấp cái nhìn rõ hơn về chi phí theo dự án.


- **Tuân thủ và quản trị**: Bạn có thể tạo ngân sách theo vùng hiệu quả hơn, hỗ trợ tuân thủ các yêu cầu chủ quyền dữ liệu. Bạn có thể theo dõi chi phí cho các vùng cụ thể trong khi loại trừ những vùng khác, đơn giản hóa việc tuân thủ quy định và phân bổ chi phí.

- **Lập kế hoạch tài chính**: Hỗ trợ các chỉ số chi phí mới cho phép bạn tạo ngân sách phù hợp với cách bạn báo cáo chi phí AWS nội bộ. Bạn có thể duy trì các dự báo chính xác hơn bao gồm tất cả chiết khấu áp dụng, dẫn đến lập kế hoạch tài chính và ra quyết định tốt hơn.

Bằng cách tận dụng những khả năng mới này, bạn có thể có cái nhìn sâu sắc hơn về chi tiêu AWS của mình, từ đó quản lý chi phí và quản trị tài chính hiệu quả hơn trong môi trường đám mây của bạn.

## Bắt đầu trong AWS Console
Tiền điều kiện: Để sử dụng những tính năng này, bạn cần có quyền IAM Cost Explorer (ce:GetCostAndUsage và ce:GetDimensionValues). Liên hệ với quản trị tài khoản hoặc IAM của bạn để thêm các quyền này. Để tìm hiểu thêm về quyền truy cập các công cụ quản lý chi phí và thanh toán, xem [Using identity-based policies (IAM policies) for AWS Cost Management.](https://docs.aws.amazon.com/cost-management/latest/userguide/billing-permissions-ref.html)

Để tạo ngân sách với các khả năng mới:
1. Mở AWS Budgets console.
2. Chọn Create budget.
3. Trong mục Budget setup, chọn Customize (advanced).
4. Đối với Budget metric, chọn tùy chọn bạn thích:
   1. Net unblended cost
   2. Net amortized cost
5. Trong Filters, cấu hình phạm vi ngân sách của bạn:
   1. Tùy chọn loại trừ các chiều cụ thể
   2. Chọn loại phí, ví dụ: Reservation Applied Usage và Savings Plan fees
6. Đặt số lượng ngân sách và cấu hình ngưỡng cảnh báo.
![AWS Budgets console showing new options for budget metric and filters](/images/3-BlogsTranslated/3.1-Blog1/1.png)

## Thay đổi API và tương thích ngược
AWS Budgets đang giới thiệu hai nhóm tính năng mới, [FilterExpression và Metrics](https://docs.aws.amazon.com/aws-cost-management/latest/APIReference/API_budgets_Budget.html), đồng thời vẫn duy trì hỗ trợ cho các trường hiện có [CostFilters và CostTypes](https://docs.aws.amazon.com/aws-cost-management/latest/APIReference/API_budgets_CostTypes.html). FilterExpression cung cấp khả năng lọc tương đồng với Cost Explorer, cho phép các lựa chọn lọc phức tạp hơn bao gồm loại trừ các giá trị chiều cụ thể. Metrics hỗ trợ các chỉ số chi phí bổ sung như net unblended và net amortized costs.

Nếu bạn đang sử dụng AWS Budgets, các ngân sách và tích hợp API hiện tại của bạn sẽ tiếp tục hoạt động như trước. Khi mô tả một ngân sách (describe a budget), AWS Budgets sẽ bao gồm cả hai trường mới FilterExpression và Metrics cùng với các trường cũ CostFilters và CostTypes trong phản hồi. Điều này cho bạn điểm khởi đầu để thực hiện cập nhật thêm mà không cần xây dựng toàn bộ loại dữ liệu Expression từ đầu.

Khi cập nhật ngân sách, bạn có thể sử dụng các trường cũ (CostFilters và CostTypes) hoặc các trường mới (FilterExpression và Metrics), nhưng không được dùng cả hai cùng lúc trong cùng một cuộc gọi API. Đối với các cấu hình có thể được biểu diễn bằng cả hai cách, phản hồi API sẽ bao gồm cả hai định dạng. Tuy nhiên, khi sử dụng các tính năng mới như loại trừ mà không thể được biểu diễn bằng định dạng cũ, chỉ các trường mới sẽ xuất hiện trong phản hồi.

## Làm việc với Budgets: Ví dụ CLI
Hãy xem qua một số ví dụ để hiểu cách các khả năng này hoạt động trong thực tiễn.

**Mô tả một ngân sách hiện có**

Là một kỹ sư FinOps, bạn cần kiểm tra ngân sách hiện có cho chi phí lưu trữ của bạn. Để làm điều đó, bạn sử dụng lệnh CLI dưới đây để mô tả ngân sách hiện có. Lệnh này sẽ hiển thị cấu hình ngân sách của bạn với cả trường cũ và trường mới:

```
aws budgets describe-budget \
--account-id 111122223333 \
--budget-name "StorageCostsBudget"
```

Trong phản hồi, bạn sẽ thấy cả các trường cũ (CostFilters và CostTypes) và các trường mới (FilterExpression và Metrics), cho phép bạn hiểu cách cấu hình ngân sách hiện tại chuyển sang định dạng mới.

```
{
  "Budget": {
    "BudgetName": "StorageCostsBudget",
    "BudgetLimit": {
      "Amount": "1000.0",
      "Unit": "USD"
    },
    // Cách biểu diễn bộ lọc trước đây
    "CostFilters": {
      "Service": ["Amazon Simple Storage Service"],
      "Region": ["us-east-1", "us-west-2"]
    },
    "CostTypes": {
      "IncludeCredit": true,
      "IncludeDiscount": true,
      "IncludeRefund": false,
      "IncludeSubscription": true,
      "UseBlended": false
    },
    // Cách biểu diễn bộ lọc mới tương đương
    "FilterExpression": {
      "Dimensions": {
        "Key": "SERVICE",
        "Values": ["Amazon Simple Storage Service"]
      },
      "And": [{
        "Dimensions": {
          "Key": "REGION",
          "Values": ["us-east-1", "us-west-2"]
        }
      }]
    },
    "Metrics": ["UNBLENDED_COST"],
    "TimeUnit": "MONTHLY"
  }
}
```

**Cập nhật một ngân sách hiện có**

Bây giờ bạn đã kiểm tra ngân sách lưu trữ, bạn muốn tinh chỉnh nó để bao gồm một dịch vụ lưu trữ mới, Amazon FSx. Dưới đây là cách bạn có thể cập nhật một ngân sách hiện có:

```
aws budgets update-budget \
--account-id 111122223333 \
--cli-input-json file://update-budget.json
```

```
# update-budget.json contents:
{
  "NewBudget": {
    "BudgetName": "StorageCostsBudget",
    "BudgetLimit": {
      "Amount": "1000.0",
      "Unit": "USD"
    },
    "FilterExpression": {
      "Dimensions": {
        "Key": "SERVICE",
        "Values": ["Amazon Simple Storage Service", "Amazon FSx"] // thêm FSx
      },
      "And": [{
        "Dimensions": {
          "Key": "REGION",
          "Values": ["us-east-1", "us-west-2"]
        }
      }]
    },
    "Metrics": ["NET_UNBLENDED_COST"],
    "TimeUnit": "MONTHLY"
  }
}
```

**Tạo một ngân sách mới với loại trừ**

Bây giờ bạn đã sẵn sàng tạo một ngân sách hàng tháng mới mà loại trừ các dịch vụ doanh nghiệp chia sẻ để theo dõi chi phí theo nhóm tốt hơn. Dưới đây là cách bạn có thể tạo ngân sách sử dụng khả năng loại trừ mới:

```
aws budgets create-budget \
--account-id 111122223333 \
--cli-input-json file://create-budget.json
```

```
# create-budget.json contents:
{
  "Budget": {
    "BudgetName": "TeamSpecificBudget",
    "BudgetType": "COST",
    "BudgetLimit": {
      "Amount": "5000.0",
      "Unit": "USD"
    },
    "FilterExpression": {
      "Not": {
        "Dimensions": {
          "Key": "SERVICE",
          "Values": ["AWS Shield", "AWS Support (Enterprise)"]
        }
      }
    },
    "Metrics": ["NET_UNBLENDED_COST"],
    "TimeUnit": "MONTHLY"
  },
  "NotificationsWithSubscribers": [
    {
      "Notification": {
        "ComparisonOperator": "GREATER_THAN",
        "NotificationType": "ACTUAL",
        "Threshold": 80,
        "ThresholdType": "PERCENTAGE"
      },
      "Subscribers": [
        {
          "Address": "team-budget-alerts@example.com",
          "SubscriptionType": "EMAIL"
        }
      ]
    }
  ]
}
```

Ngân sách mới này loại trừ các dịch vụ chia sẻ, cho phép bạn tập trung vào chi phí theo nhóm cụ thể. Lưu ý rằng khi bạn mô tả ngân sách này, bạn sẽ chỉ thấy các trường mới (FilterExpression và Metrics) trong phản hồi, vì khả năng loại trừ không thể được biểu diễn bằng các trường cũ.

## Các thực hành tốt nhất để tận dụng những khả năng mới
Để tận dụng tối đa các tính năng mới này, hãy xem xét các thực hành sau:

1. Rà soát các ngân sách hiện tại của bạn để xác định xem các chỉ số và tùy chọn lọc mới có thể cung cấp theo dõi chi phí thực tế chính xác hơn không.
2. Sử dụng các chỉ số net amortized hoặc net unblended cost để tạo ngân sách phù hợp với cách bạn báo cáo chi phí AWS nội bộ.
3. Tận dụng khả năng loại trừ mới để tạo các ngân sách nhắm đến các nhóm, dự án hoặc trung tâm chi phí cụ thể bằng cách loại trừ chi phí chia sẻ hoặc không liên quan.
4. Tạo các ngân sách riêng cho các loại chi phí khác nhau (ví dụ: phí trả trước so với chi phí sử dụng) để có cái nhìn chi tiết hơn về mô hình chi tiêu của bạn.
5. Nếu bạn có tự động hóa hiện hữu sử dụng API AWS Budgets, lên kế hoạch chuyển đổi dần sang các trường mới. Thử nghiệm kỹ để đảm bảo các tích hợp hoạt động như mong đợi với các khả năng được cải thiện.


## Câu hỏi thường gặp

**Làm sao tôi có thể thay đổi ngân sách của mình dễ dàng nhất để sử dụng các tùy chọn lọc mới?**

Bạn có thể xem cấu hình ngân sách hiện tại trong console hoặc thông qua [API Describe Budget](https://docs.aws.amazon.com/aws-cost-management/latest/APIReference/API_budgets_DescribeBudget.html), API này sẽ hiển thị cả định dạng trường cũ và trường mới. Điều này giúp bạn dễ nhìn thấy cách bộ lọc hiện tại chuyển sang định dạng mới.

**Nếu tôi không muốn sử dụng các tính năng mới thì sao?**

Bạn có thể tiếp tục sử dụng AWS Budgets như hiện tại và bỏ qua các trường mới trong tất cả các API. Ngân sách hiện tại của bạn sẽ tiếp tục hoạt động như trước.

**Tôi có thể có một số ngân sách dùng bộ lọc cũ và một số dùng bộ lọc mới không?**

Có. Khi bạn sử dụng API DescribeBudget hoặc xem ngân sách trong console, ngân sách sẽ được hiển thị với cả định dạng cũ và mới nếu cấu hình có thể biểu diễn bằng cả hai. Tuy nhiên, đối với ngân sách dùng các tính năng mới như loại trừ — vốn không thể biểu diễn trong định dạng cũ — chỉ các trường mới (FilterExpression và Metrics) sẽ xuất hiện trong phản hồi.

**Tôi cần thay đổi gì trong mã của mình để không làm hỏng hệ thống?**

Mã hiện tại sử dụng các trường cũ (CostFilters và CostTypes) sẽ tiếp tục hoạt động như trước. Nếu bạn muốn sử dụng các khả năng mới, bạn sẽ cần cập nhật mã của mình để sử dụng FilterExpression và Metrics thay thế. Hãy nhớ rằng bạn không thể trộn cả trường cũ và mới trong cùng một cuộc gọi API.

## Kết luận
Với những khả năng mới này, AWS Budgets mang đến cho bạn linh hoạt và độ chính xác cao hơn trong quản lý chi tiêu đám mây. Dù bạn muốn theo dõi chi phí sau chiết khấu, tạo ngân sách tập trung cho các nhóm cụ thể, hay có cái nhìn chi tiết hơn về chi phí AWS của mình, những cải tiến này cung cấp các công cụ cần thiết để quản lý tài chính đám mây hiệu quả.





