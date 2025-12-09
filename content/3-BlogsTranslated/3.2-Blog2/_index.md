---
title: "Blog 2"
date: 2025-09-10
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---

# Increase engagement with localized content using Amazon Bedrock Flows
by Benjamin Le and Emilio Garcia Montano | on 01 MAY 2025 | in [Amazon Bedrock](https://aws.amazon.com/blogs/media/category/artificial-intelligence/amazon-machine-learning/amazon-bedrock/), [Amazon Bedrock Knowledge Bases](https://aws.amazon.com/blogs/media/category/artificial-intelligence/amazon-machine-learning/amazon-bedrock/amazon-bedrock-knowledge-bases/), [Amazon Bedrock Prompt Management](https://aws.amazon.com/blogs/media/category/artificial-intelligence/amazon-machine-learning/amazon-bedrock/amazon-bedrock-prompt-management/), [Amazon Machine Learning](https://aws.amazon.com/blogs/media/category/artificial-intelligence/amazon-machine-learning/), [Amazon Nova](https://aws.amazon.com/blogs/media/category/artificial-intelligence/amazon-machine-learning/amazon-bedrock/amazon-nova/), [Amazon Simple Storage Service (S3)](https://aws.amazon.com/blogs/media/category/storage/amazon-simple-storage-services-s3/), [Artificial Intelligence](https://aws.amazon.com/blogs/media/category/artificial-intelligence/), [Content Production](https://aws.amazon.com/blogs/media/category/industries/entertainment/content-production/), [Data Science & Analytics for Media](https://aws.amazon.com/blogs/media/category/industries/entertainment/data-science/), [Industries](https://aws.amazon.com/blogs/media/category/industries/), [Media & Entertainment](https://aws.amazon.com/blogs/media/category/industries/entertainment/), [Storage](https://aws.amazon.com/blogs/media/category/storage/) | [Permalink](https://aws.amazon.com/blogs/media/increase-engagement-with-localized-content-using-amazon-bedrock-flows/) | [Share](https://aws.amazon.com/blogs/media/increase-engagement-with-localized-content-using-amazon-bedrock-flows/)

Content creators and publishers often maintain large collections with thousands, if not hundreds of thousands, of articles that can be localized for new audiences and geographies to deliver higher engagement in emerging and newly targeted markets. Localization is generally the process of transforming content (vocabulary choice, tone adjustments, and translation) for a new audience from one geography to another.

Human-driven localization cannot scale to the necessary volume, so machine translation is commonly used. However, automated localization still struggles with quality—particularly in contextualizing content to capture the nuances of each specific market. This often results in lower engagement rates compared to the original content. With foundation models supporting a wide range of languages and dialects, media and entertainment customers are increasingly using generative AI to deliver higher-quality localized content.

[Amazon Bedrock Flows](https://aws.amazon.com/bedrock/flows/) provides a no-code visual builder and a set of APIs to seamlessly connect leading state-of-the-art foundation models (such as [Anthropic’s Claude](https://aws.amazon.com/bedrock/claude/) and [Amazon Nova](https://aws.amazon.com/ai/generative-ai/nova/)) within [Amazon Bedrock](https://aws.amazon.com/bedrock/). It also integrates with other AWS services to automate user-defined generative AI workflows that go far beyond sending a prompt to a large language model.

[Amazon Bedrock Prompt Management](https://aws.amazon.com/bedrock/prompt-management/) provides a streamlined interface to create, evaluate, version, and share prompts. It helps developers and prompt engineers achieve the best responses from foundation models for their use cases.

In this post, we demonstrate how you can leverage Amazon Bedrock capabilities (such as Flows, Prompt Management, and various foundation models) to quickly build and test a workflow. This workflow takes existing content, produces localized copies, and provides an evaluation of the differences for editor review.

## Scenario overview
As an online publisher looking to expand readership across new geographies and channels—without relying solely on new local content—you want to create a workflow that:

1. Localizes existing text content for a specific country and language to better align with local markets and advertising strategies.
2. Adapts content to new and emerging channels (such as short-form social media) using style guides currently stored in [Amazon Bedrock Knowledge Bases](https://aws.amazon.com/bedrock/knowledge-bases/) to help editors review their work.
3. Provides evaluation metrics (such as factual accuracy, length, dialect, and overall change in meaning) so editors can make informed decisions to publish or refine content further.

![Figure 1: High-level architecture diagram outlining a content management system using Amazon Bedrock Flows and Amazon Bedrock Knowledge Bases to localize content and provide evaluations for editor review.](/images/3-BlogsTranslated/3.2-Blog2/1.png)
*Figure 1: High-level architecture diagram outlining a content management system using Amazon Bedrock Flows and Amazon Bedrock Knowledge Bases to localize content and provide evaluations for editor review.*

## Prerequisites
Before creating the flow and prompts, ensure you have the following setup:

- An AWS account and an IAM user or role authorized to use Amazon Bedrock. Refer to: [Getting started with Amazon Bedrock](https://docs.aws.amazon.com/bedrock/latest/userguide/getting-started.html). Ensure the role includes permissions for Flows and Prompt Management as explained in the prerequisites for [Amazon Bedrock Flows](https://docs.aws.amazon.com/bedrock/latest/userguide/flows-prereq.html) and [Prompt Management](https://docs.aws.amazon.com/bedrock/latest/userguide/prompt-management-prereq.html).
- Access to the models you plan to invoke and evaluate. See: [Manage access to Amazon Bedrock foundation models](https://docs.aws.amazon.com/bedrock/latest/userguide/model-access.html).
  - Our example uses Amazon Nova Pro, [Cohere Command R, Cohere Embed Multilingual v3](https://aws.amazon.com/bedrock/cohere/), and Anthropic’s Claude 3.7 Sonnet in the Oregon Region (us-west-2).
- An [Amazon Bedrock Knowledge Base](https://docs.aws.amazon.com/bedrock/latest/userguide/knowledge-base.html) configured with an [Amazon S3 data source](https://docs.aws.amazon.com/bedrock/latest/userguide/s3-data-source-connector.html).
  - In our example, the knowledge base contains style guides for creating social media content.

## Creating the prompts
Before building the flow, create two prompts that will be used in the later prompt flow.

The first prompt performs content localization, and we use the Anthropic Claude 3.7 Sonnet foundation model, which supports languages such as English, French, Spanish, Portuguese, Japanese, and others.

When designing prompts, variables such as the article text are represented by `{{article}}`, and the target language is represented by `{{language}}`, allowing values to be shared across flow nodes for greater flexibility.

![Figure 2: Content Localization prompt](/images/3-BlogsTranslated/3.2-Blog2/2.png)
*Figure 2: Content Localization prompt*

The second prompt evaluates the original content and the localized content to provide an assessment for editors. To remain independent from the localization prompt, this evaluation prompt uses Amazon Nova Pro—a powerful multimodal model that provides the best combination of accuracy, speed, and cost across more than 200 languages.

![Figure 3: Content Evaluation prompt](/images/3-BlogsTranslated/3.2-Blog2/3.png)
*Figure 3: Content Evaluation prompt*

## Creating and configuring the flow
Using the Amazon Bedrock console, navigate to **Flows** under Builder Tools and create a new flow as shown in Figure 4.

![Figure 4: Amazon Bedrock Flow named "Content Localization" showing name, description, creation date, IAM role, and flow ID.](/images/3-BlogsTranslated/3.2-Blog2/4.png)
*Figure 4: Amazon Bedrock Flow named "Content Localization"*

After creation, the console will automatically open the flow builder. Otherwise, select **Edit in flow builder**.

Inside the Flow Builder, you can choose from multiple [node types](https://docs.aws.amazon.com/bedrock/latest/userguide/flows-nodes.html). Drag nodes onto the canvas and link them after defining variables or loading saved prompts.

In this example, the flow is shown in Figure 5.

![Figure 5: Content localization flow.](/images/3-BlogsTranslated/3.2-Blog2/5.png) 
*Figure 5: Content localization flow*

Details for each node:

1. **Input node** simulates content coming from a CMS and accepts a JSON object with:
   - `article`: selected article text  
   - `country`: target country  
   - `language`: target language  
   - `query`: text prompt to query the knowledge base for relevant style guides  

2. **Get_Style_Guides node** uses Cohere Command R to interpret the query and retrieve results from the knowledge base. These results supplement localized content generation.

3. **Localization Prompt node** uses the earlier prompt to localize the article.

4. **Evaluation Prompt node** evaluates the original and localized texts using the evaluation prompt.

5. **Two Output nodes** emit data produced by the respective prompt nodes.

LLMs can generate hallucinations. Amazon Bedrock Flows integrates with [Amazon Bedrock Guardrails](https://docs.aws.amazon.com/bedrock/latest/userguide/flows-guardrails.html) so you can configure safeguards to detect or block undesired responses.

## Testing the flow
Using the **Test flow** panel, you can quickly test the workflow with near real-time node outputs.

To illustrate how generative AI can adapt Spanish content across Europe and Latin America, the following examples use the same input text but change the target country.

![Figure 6: Example inputs.](/images/3-BlogsTranslated/3.2-Blog2/6.png)
*Figure 6: Example inputs*

![Figure 7: Sample localized text.](/images/3-BlogsTranslated/3.2-Blog2/7.png)
*Figure 7: Sample localized text*

Finally, the evaluation step uses a separate foundation model to independently compare original and localized content and produce a scored assessment.

![Figure 8: Example content evaluation.](/images/3-BlogsTranslated/3.2-Blog2/8.png)
*Figure 8: Example content evaluation*

## Pricing
Amazon Bedrock Flows charges per 1,000 transitions within your workflow. A transition occurs whenever data moves from one node to another (for example, from an input node to a prompt node). There is no additional charge for using Amazon Bedrock Prompt Management.

Model usage pricing depends on the model type and the number of input/output tokens. This example also uses Amazon Bedrock Knowledge Bases configured with an Amazon OpenSearch Serverless vector database and Amazon S3 as the data source.

Pricing varies by AWS Region. All resources in this walkthrough are configured in Oregon (us-west-2). Refer to pricing pages for [Amazon Bedrock](https://aws.amazon.com/bedrock/pricing/), [Amazon S3](https://aws.amazon.com/s3/pricing/), and [Amazon OpenSearch Service](https://aws.amazon.com/opensearch-service/serverless-vector-database/).

## Conclusion
We have demonstrated how media and entertainment customers can build a localized content workflow using a serverless, low-code architecture. Using Amazon Bedrock Flows and Prompt Management, content owners and editors can leverage generative AI to deliver more engaging content to new audiences.

Contact an [AWS Representative](https://pages.awscloud.com/Media-and-Entertainment-Contact-Us.html) to learn how we can help accelerate your business.

## Further reading

- Amazon Bedrock Flows User Guide:  
  [Build an end-to-end generative AI workflow with Amazon Bedrock Flows](https://docs.aws.amazon.com/bedrock/latest/userguide/flows.html)

- Amazon Bedrock Prompt Management User Guide:  
  [Construct and store reusable prompts with Prompt Management in Amazon Bedrock](https://docs.aws.amazon.com/bedrock/latest/userguide/prompt-management.html)

- [Amazon Bedrock Flows is now generally available with enhanced safety and traceability](https://aws.amazon.com/blogs/machine-learning/amazon-bedrock-flows-is-now-generally-available-with-enhanced-safety-and-traceability/)

- [Evaluating prompts at scale with Prompt Management and Prompt Flows for Amazon Bedrock](https://aws.amazon.com/blogs/machine-learning/evaluating-prompts-at-scale-with-prompt-management-and-prompt-flows-for-amazon-bedrock/)
