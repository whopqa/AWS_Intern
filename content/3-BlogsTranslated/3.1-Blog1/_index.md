---
title: "Blog 1"
date: 2025-09-10
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# Improving accuracy for your cloud budgeting with new features in AWS Budgets
by Fredrik Tunvall | on 29 APR 2025 | in **[Announcements](https://aws.amazon.com/blogs/aws-cloud-financial-management/category/post-types/announcements/), [AWS Budgets](https://aws.amazon.com/blogs/aws-cloud-financial-management/category/aws-cloud-financial-management/aws-budgets/), [AWS Cloud Financial Management](https://aws.amazon.com/blogs/aws-cloud-financial-management/category/aws-cloud-financial-management/) | [Permalink](https://aws.amazon.com/blogs/aws-cloud-financial-management/improving-accuracy-for-your-cloud-budgeting-with-new-features-in-aws-budgets/) | [Share](https://aws.amazon.com/blogs/aws-cloud-financial-management/improving-accuracy-for-your-cloud-budgeting-with-new-features-in-aws-budgets/)**

Today, AWS announced new capabilities in [AWS Budgets](https://aws.amazon.com/aws-cost-management/aws-budgets/) that provides greater flexibility in how you track and manage your AWS spend. These enhancements include:

- Support for additional cost metrics: net unblended costs and net amortized costs
- Ability to exclude specific dimension values when creating budgets (such as service, account, and instance type)
- New filtering capabilities for charge types for fine-grained control to include or exclude [AWS Savings Plans](https://aws.amazon.com/savingsplans/) (SPs) or Reservation (RI) upfront charges, recurring fees, taxes, and credits
Enhanced API functionality that supports filter expressions that are consistent with AWS [Cost Explorer](https://aws.amazon.com/aws-cost-management/aws-budgets/)

These improvements enable you to create budgets that better reflect your actual costs, including discounts, and provide more granular control over what’s included in your budget calculations. They also let you create a budget with filter selections consistent with AWS Cost Explorer.

## Enhanced Capabilities for More Accurate Cost Tracking
The new capabilities in AWS Budgets offer significant improvements in cost tracking accuracy and flexibility. By supporting net unblended and net amortized cost metrics, you can now create budgets that align precisely with your actual spend, including all applicable discounts. This enhancement is particularly valuable for companies using Savings Plans or Reserved Instances, as it allows for more accurate budget planning and tracking.

The introduction of advanced filtering capabilities, including the ability to exclude specific dimension values, opens up new possibilities for precise cost monitoring. These features enable several powerful use cases that were previously challenging to implement:

- **Granular Cost Control**: Creating targeted budgets is now much simpler. For example, you can easily exclude shared infrastructure costs when setting up budgets for specific research initiatives, providing a clearer view of project-specific expenses.

- **Compliance and Governance**: You can create region-specific budgets more effectively, aiding in compliance with data sovereignty requirements. You can now efficiently track costs for specific regions while excluding others, simplifying regulatory compliance and cost allocation.

- **Financial Planning**: The support for new cost metrics allows you to create budgets that precisely match your cost reporting needs. You can now maintain more accurate forecasts that include all applicable discounts, leading to improved financial planning and decision-making.

By leveraging these new capabilities, you can gain deeper insights into your AWS spend, enabling more effective cost management and financial governance across your cloud environments.

## Getting Started in the AWS Console
Prerequisite: To use these features, you need Cost Explorer IAM permissions (ce:GetCostAndUsage and ce:GetDimensionValues). Contact your account or IAM administrator to add these permissions. To learn more about access to billing and cost management tools, see [Using identity-based policies (IAM policies) for AWS Cost Management.](https://docs.aws.amazon.com/cost-management/latest/userguide/billing-permissions-ref.html)

To create a budget with the new capabilities:
1. Open the AWS Budgets console.
2. Choose Create budget.
3. Under Budget setup, choose Customize (advanced).
4. For Budget metric, select your preferred option:
   1. Net unblended cost
   2. Net amortized cost
5. Under Filters, configure your budget scope:
   1. Optionally exclude specific dimensions
   2. Choose charge types, e.g. Reservation Applied Usage and Savings Plan fees
6. Set your budget amount and configure alert thresholds.
![AWS Budgets console showing new options for budget metric and filters](/images/3-BlogsTranslated/3.1-Blog1/1.png)

## API Changes and Backward Compatibility
AWS Budgets is introducing two new fields, [FilterExpression and Metrics](https://docs.aws.amazon.com/aws-cost-management/latest/APIReference/API_budgets_Budget.html), while maintaining support for the existing [CostFilters and CostTypes](https://docs.aws.amazon.com/aws-cost-management/latest/APIReference/API_budgets_CostTypes.html) fields. The new FilterExpression field provides the same filtering capabilities as Cost Explorer, allowing for more sophisticated filtering options including the ability to exclude specific dimension values. The Metrics field supports additional cost metrics such as net unblended and net amortized costs.

If you’re already using AWS Budgets, your existing budgets and API integrations will continue to function as before. When describing a budget, AWS Budgets will now include both the new FilterExpression and Metrics fields alongside the existing CostFilters and CostTypes fields in the response. This gives you a starting point for making further updates without having to build the entire Expression data type from scratch.

When updating budgets, you can use either the old fields (CostFilters and CostTypes) or the new fields (FilterExpression and Metrics), but not both in the same API call. For configurations that can be expressed using both old and new fields, the API response will include both formats. However, when using new features like exclusions that cannot be represented in the old format, only the new fields will appear in the response.

## Working with Budgets: CLI Examples
Let’s walk through some examples to see how these capabilities work in practice.

**Describing an existing budget**

As a FinOps engineer, you need to audit your existing budget for your storage cost. To do so, you use the CLI commands below to describe your existing budget. This command will show your budget configuration with both old and new filters:

```
aws budgets describe-budget \
--account-id 111122223333 \
--budget-name "StorageCostsBudget"
```

In the response, you’ll see both the old fields (CostFilters and CostTypes) and the new fields (FilterExpression and Metrics), allowing you to understand how your existing budget configuration translates to the new format.

```
{
  "Budget": {
    "BudgetName": "StorageCostsBudget",
    "BudgetLimit": {
      "Amount": "1000.0",
      "Unit": "USD"
    },
    // Previous filter representation
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
    // Equivalent new filter representation
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

**Updating an existing budget**

Now that you’ve reviewed your storage budget, you want to refine it to include a new storage service, Amazon FSx. Here’s how you can update an existing budget:

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
        "Values": ["Amazon Simple Storage Service", "Amazon FSx"] // add FSx
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

**Creating a New Budget with Exclusion**

You’re now ready to create a new monthly budget that excludes shared enterprise services to better track team-specific costs. Here’s how you can create a budget using the new exclusion capability:

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

This new budget excludes shared services, allowing you to focus on team-specific costs. Note that when you describe this budget, you’ll see only the new fields (FilterExpression and Metrics) in the response, as the exclusion capability cannot be represented using the old fields.

## Best Practices for Leveraging the New Capabilities
To make the most of these new features, consider the following best practices:

1. Review your existing budgets to determine if the new metrics and filtering options can provide more accurate tracking of your actual costs.
2. Use the net amortized or net unblended cost metrics to create budgets that match how you report on AWS costs internally.
3. Leverage the new exclusion capabilities to create more targeted budgets for specific teams, projects, or cost centers by excluding shared or irrelevant costs.
4. Create separate budgets for different types of costs (e.g., upfront fees vs. usage-based costs) to get a more detailed view of your spend patterns.
5. If you have existing automation using the AWS Budgets API, plan a gradual transition to the new fields. Test thoroughly to ensure your integrations work as expected with the enhanced capabilities.

## Frequently Asked Questions

**How can I most easily convert my budgets to use the new filter options?**

You can view your existing budget configurations in the console or through the [DescribeBudget API](https://docs.aws.amazon.com/aws-cost-management/latest/APIReference/API_budgets_DescribeBudget.html), which will display both old and new field formats. This helps you see how your current filters translate to the new format.

**What if I don't want to use the new features?**

You can continue to use AWS Budgets as you do today, and simply ignore the new fields across all APIs. Your existing budgets will continue to function as before.

**Can I have some budgets that use old filters and some budgets that use new?**

Yes, you can. When you use the DescribeBudget API or view budgets in the console, budgets will be shown with both old and new fields if the configuration can be represented in both formats. However, for budgets using new features like exclusions, which cannot be represented in the old format, only the new fields (FilterExpression and Metrics) will be present in the response.

**What changes do I need to make in my code so I don’t break anything?**

Existing code using the old fields (CostFilters and CostTypes) will continue to work as before. If you want to use the new capabilities, you’ll need to update your code to use FilterExpression and Metrics instead. Remember that you cannot mix old and new fields in the same API call.

## Conclusion
With these new capabilities, AWS Budgets offers you more flexibility and accuracy in managing your cloud spend. Whether you’re looking to track costs after discounts, create focused budgets for specific teams, or get a more granular view of your AWS expenses, these enhancements provide the tools you need for effective cloud financial management.
