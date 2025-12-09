---
title: "Blog 3"
date: 2025-09-10
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---


# Innovating at Speed: BMW's Generative AI Solution for Cloud Incident Analysis
by Johann Wildgruber, Dr. Jens Kohl, Thilo Bindel, Luisa-Sophie Gloger, Aishwarya Lakshmi Krishnan, Huong Vu, Kim Robins, Otto Kruse, Satyam Saxena, and Tanrajbir Takher | March 05, 2025 | in [Advanced (300)](https://aws.amazon.com/blogs/machine-learning/category/learning-levels/advanced-300/), [Amazon Bedrock](https://aws.amazon.com/blogs/machine-learning/category/artificial-intelligence/amazon-machine-learning/amazon-bedrock/), [Amazon Bedrock Agents](https://aws.amazon.com/blogs/machine-learning/category/artificial-intelligence/amazon-machine-learning/amazon-bedrock/amazon-bedrock-agents/), [Amazon CloudWatch](https://aws.amazon.com/blogs/machine-learning/category/management-tools/amazon-cloudwatch/), [Artificial Intelligence](https://aws.amazon.com/blogs/machine-learning/category/artificial-intelligence/), [AWS CloudTrail](https://aws.amazon.com/blogs/machine-learning/category/management-tools/aws-cloudtrail/), [Customer Enablement](https://aws.amazon.com/blogs/machine-learning/category/customer-enablement/), [Customer Solutions](https://aws.amazon.com/blogs/machine-learning/category/post-types/customer-solutions/) | [Permalink](https://aws.amazon.com/blogs/machine-learning/innovating-at-speed-bmws-generative-ai-solution-for-cloud-incident-analysis/) | [Comments](https://aws.amazon.com/blogs/machine-learning/innovating-at-speed-bmws-generative-ai-solution-for-cloud-incident-analysis/#Comments) | [Share](https://aws.amazon.com/blogs/machine-learning/innovating-at-speed-bmws-generative-ai-solution-for-cloud-incident-analysis/)

<i>This post was co-authored with Johann Wildgruber, Dr. Jens Kohl, Thilo Bindel, and Luisa-Sophie Gloger from BMW Group.</i>

The [BMW Group](https://www.bmwgroup.com/) — headquartered in Munich, Germany — employs over 154,000 people and operates 30 manufacturing and assembly plants worldwide, along with R&D centers in 17 countries. Today, BMW Group (BMW) is a global leader in premium automobiles and motorcycles, also offering high-end financial and mobility services.

[BMW Connected Company](https://www.bmwusa.com/explore/connecteddrive.html) is a division within BMW responsible for developing and operating premium digital services for BMW’s connected fleet, which currently numbers more than 23 million vehicles worldwide. These digital services are used by many BMW vehicle owners daily; for example, to lock or open car doors remotely using an app on their phone, to start window defrost remotely, to buy navigation map updates from the car’s menu, or to listen to music streamed over the internet in their car.

In this post, we explain how BMW uses generative AI technology on AWS to help run these digital services with high availability. Specifically, BMW uses [Amazon Bedrock Agents](https://aws.amazon.com/bedrock/agents/) to make remediating (partial) service outages quicker by speeding up the otherwise cumbersome and time-consuming process of root cause analysis (RCA). The fully automated RCA agent correctly identifies the right root cause for most cases (measured at 85%), and helps engineers in terms of system understanding and real-time insights in their cases. This performance was further validated during the proof of concept, where employing the RCA agent on representative use cases clearly demonstrates the benefits of this solution, allowing BMW to achieve significantly lower diagnosis times.


## Challenges in Root Cause Analysis for Cloud Incidents
Digital services are often implemented by chaining multiple software components together; components that might be built and run by different teams. For example, consider the service of remotely opening and locking vehicle doors. There might be a development team building and running the iOS app, another team for the Android app, a team building and running the backend-for-frontend used by both the iOS and Android app, and so on. Moreover, these teams might be geographically dispersed and run their workloads in different locations and regions; many hosted on AWS, some elsewhere.

Now consider a (fictitious) scenario where reports come in from car owners complaining that remotely locking doors with the app no longer works. Is the iOS app responsible for the outage, or the backend-for-frontend? Did a firewall rule change somewhere? Did an internal TLS certificate expire? Is the MQTT system experiencing delays? Was there an inadvertent breaking change in recent API changes? When did they actually deploy that? Or was the database password for the central subscription service rotated again?

It can be difficult to determine the root cause of issues in situations like this. It requires checking many systems and teams, many of which might be failing, because they’re interdependent. Developers need to reason about the system architecture, form hypotheses, and follow the chain of components until they have located the one that is the culprit. They often have to backtrack and reassess their hypotheses, and pursue the investigation in another chain of components.

Understanding the challenges in such complex systems highlights the need for a robust and efficient approach to root cause analysis. With this context in mind, let’s explore how BMW and AWS collaborated to develop a solution using Amazon Bedrock Agents to streamline and enhance the RCA process.

## Solution Overview
At a high level, the solution uses an Amazon Bedrock agent to do automated RCA. This agent has several custom-built tools at its disposal to do its job. These tools, implemented by [AWS Lambda](https://aws.amazon.com/lambda/) functions, use services like [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/) and [AWS CloudTrail](https://aws.amazon.com/cloudtrail/) to analyze system logs and metrics. The following diagram illustrates the solution architecture.


![Architecture of the Amazon Bedrock Agent solution for automated RCA.](/images/3-BlogsTranslated/3.3-Blog3/1.png)

When an incident occurs, an on-call engineer gives a description of the issue at hand to the Amazon Bedrock agent. The agent will then start investigating for the root cause of the issue, using its tools to do tasks that the on-call engineer would otherwise do manually, such as searching through logs. Based on the clues it uncovers, the agent proposes several likely hypotheses to the on-call engineer. The engineer can then resolve the issue, or give pointers to the agent to direct the investigation further. In the following section, we take a closer look at the tools the agent uses.

## Amazon Bedrock agent tools
The Amazon Bedrock agent’s effectiveness in performing RCA lies in its ability to seamlessly integrate with custom tools. These tools, designed as Lambda functions, use AWS services like CloudWatch and CloudTrail to automate tasks that are typically manual and time-intensive for engineers. By organizing its capabilities into specialized tools, the Amazon Bedrock agent makes sure that RCA is both efficient and precise.

**Architecture Tool**
The Architecture Tool uses [C4 diagrams](https://c4model.com/) to provide a comprehensive view of the system’s architecture. These diagrams, enhanced through [Structurizr](https://structurizr.com/), give the agent a hierarchical understanding of component relationships, dependencies, and workflows. This allows the agent to target the most relevant areas during its RCA process, effectively narrowing down potential causes of failure based on how different systems interact.

For instance, if an issue affects a specific service, the Architecture Tool can identify upstream or downstream dependencies and suggest hypotheses focused on those systems. This accelerates diagnostics by enabling the agent to reason contextually about the architecture instead of blindly searching through logs or metrics.

**Logs Tool**
The Logs Tool uses CloudWatch Logs Insights to analyze log data in real time. By searching for patterns, errors, or anomalies, as well as comparing the trend to the previous period, it helps the agent pinpoint issues related to specific events, such as failed authentications or system crashes.

For example, in a scenario involving database access failures, the Logs Tool might identify a new spike in the number of error messages such as “FATAL: password authentication failed” compared to the previous hour. This insight allows the agent to quickly associate the failure with potential root causes, such as an improperly rotated database password.

**Metrics Tool**
The Metrics Tool provides the agent with real-time insights into the system’s health by monitoring key metrics through CloudWatch. This tool identifies statistical anomalies in critical performance indicators such as latency, error rates, resource utilization, or unusual spikes in usage patterns, which can often signal potential issues or deviations from normal behavior.

For instance, in a Kubernetes memory overload scenario, the Metrics Tool might detect a sharp increase in memory consumption or unusual resource allocation prior to the failure. By surfacing CloudWatch metric alarms for such anomalies, the tool enables the agent to prioritize hypotheses related to resource mismanagement, misconfigured thresholds, or unexpected system load, guiding the investigation more effectively toward resolving the issue.

**Infrastructure Tool**
The Infrastructure Tool uses CloudTrail data to analyze critical control-plane events, such as configuration changes, security group updates, or API calls. This tool is particularly effective in identifying misconfigurations or breaking changes that might trigger cascading failures.

Consider a case where a security group ingress rule is inadvertently removed, causing connectivity issues between services. The Infrastructure Tool can detect and correlate this event with the reported incident, providing the agent with actionable insights to guide its RCA process.

By combining these tools, the Amazon Bedrock agent mimics the step-by-step reasoning of an experienced engineer while executing tasks at machine speed. The modular nature of the tools allows for flexibility and customization, making sure that RCA is tailored to the unique needs of BMW’s complex, multi-regional cloud infrastructure.

In the next section, we discuss how these tools work together within the agent’s workflow.

## Amazon Bedrock Agents: ReAct Framework in Action
At the heart of BMW’s rapid RCA lies the [ReAct](https://arxiv.org/abs/2210.03629) (Reasoning and Action) agent framework, an innovative approach that dynamically combines logical reasoning with task execution. By integrating ReAct with Amazon Bedrock, BMW gains a flexible solution for diagnosing and resolving complex cloud-based incidents. Unlike traditional methods, which rely on predefined workflows, ReAct agents use real-time inputs and iterative decision-making to adapt to the specific circumstances of an incident.

The ReAct agent in BMW’s RCA solution uses a structured yet adaptive workflow to diagnose and resolve issues. First, it interprets the textual description of an incident (for example, “Vehicle doors cannot be locked via the app”) to identify which parts of the system are most likely impacted. Guided by the ReAct framework’s iterative reasoning, the agent then gathers evidence by calling specialized tools, using data centrally aggregated in a [cross-account observability setup](https://aws.amazon.com/blogs/aws/new-amazon-cloudwatch-cross-account-observability/). By continuously reevaluating the results of each tool invocation, the agent zeros in on potential causes—whether an expired certificate, a revoked firewall rule, or a spike in traffic—until it isolates the root cause. The following diagram illustrates this workflow.

<video width="100%" controls>
  <source src="/images/3-BlogsTranslated/3.3-Blog3/react-flow.mp4" type="video/mp4">
</video>

The ReAct framework offers the following benefits:
- **Dynamic & adaptive**: The ReAct agent tailors its approach to the specific incident, rather than a one-size-fits-all methodology. This adaptability is especially critical in BMW’s multi-regional, multi-service architecture.
- **Efficient tool utilization**: By reasoning about which tools to invoke and when, the ReAct agent minimizes redundant queries, providing faster diagnostics without overloading AWS services like CloudWatch or CloudTrail.
- **Human-like reasoning**: The ReAct agent mimics the logical thought process of a seasoned engineer, iteratively exploring hypotheses until it identifies the root cause. This capability bridges the gap between automation and human expertise.

## Case study: Root cause analysis “Unlocking vehicles via the iOS app”
To illustrate the power of Amazon Bedrock agents in action, let us explore a possible real-world scenario involving the interplay between BMW’s connected fleet and the digital services running in the cloud backend.

We deliberately change the security group for the central networking account in a test environment. This has the effect that requests from the fleet are (correctly) blocked by the changed security group and do not reach the services hosted in the backend. Hence, a test user cannot lock or unlock her vehicle door remotely.

**Incident Details**

BMW engineers received a report from a tester indicating the remote lock/unlock functionality on the mobile app does not work.

This report raised immediate questions: was the issue in the app itself, the backend-for-frontend service, or deeper within the system, such as in the MQTT connectivity or authentication mechanisms?

**How the ReAct agent addresses the problem**
1. The agent begins by understanding the overall system architecture, calling the Architecture Tool. The outputs of the architecture tool reveal that the iOS app, like the Android app, is connected to a backend-for-frontend API, and that the backend-for-frontend API itself is connected to several other internal APIs, such as the Remote Vehicle Management API. The Remote Vehicle Management API is responsible for sending commands to cars by using MQTT messaging.
2. The agent uses the other tools at its disposal in a targeted way: it scans the logs, metrics, and control plane activities of only those components that are involved in remotely unlocking car doors: iOS app remote logs, backend-for-frontend API logs, and so on. The agent finds several clues:

      a. Anomalous logs that indicate connectivity issues (network timeouts).

      b. A sharp decrease in the number of successful invocations of the Remote Vehicle Management API.

      c. Control plane activities: several security groups in the central networking account hosted on the testing environment were changed.
3. Based on those findings, the agent infers and defines several hypotheses and presents these to the user, ordered by their likelihood. In this case, the first hypothesis is the actual root cause: a security group was inadvertently changed in the central networking account, which meant that network traffic between the backend-for-frontend and the Remote Vehicle Management API was now blocked. The agent correctly correlated logs (“fetch timeout error”), metrics (decrease in invocations) and control plane changes (security group ingress rule removed) to come to this conclusion.
4. If the on-call engineer wants further information, they can now ask follow-up questions to the agent, or instruct the agent to investigate elsewhere as well.

The entire process—from incident detection to resolution—took minutes, compared to the hours it could have taken with traditional RCA methods. The ReAct agent’s ability to dynamically reason, access cross-account observability data, and iterate on its hypotheses alleviated the need for tedious manual investigations.

<video width="100%" controls>
  <source src="/images/3-BlogsTranslated/3.3-Blog3/ios+issue+BMW-truncated.mp4" type="video/mp4">
</video>

The entire diagnosis took minutes instead of hours.

## Conclusion
By using Amazon Bedrock ReAct agents, BMW has shown how to improve its approach to root cause analysis, turning a complex and manual process into an efficient, automated workflow. The tools integrated within the ReAct framework significantly narrow down potential reasoning space, and enable dynamic hypotheses generation and targeted diagnostics, mimicking the reasoning process of seasoned engineers while operating at machine speed. This innovation has reduced the time required to identify and resolve service disruptions, further enhancing the reliability of BMW’s connected services and improving the experience for millions of customers worldwide.

The solution has demonstrated measurable success, with the agent identifying root causes in 85% of test cases and providing detailed insights in the remainder, greatly expediting engineers’ investigations. By lowering the barrier to entry for junior engineers, it has enabled less-experienced team members to diagnose issues effectively, maintaining reliability and scalability across BMW’s operations.

Incorporating generative AI into RCA processes showcases the transformative potential of AI in modern cloud-based operations. The ability to adapt dynamically, reason contextually, and handle complex, multi-regional infrastructures makes Amazon Bedrock Agents a game changer for organizations aiming to maintain high availability in their digital services.

As BMW continues to expand its connected fleet and digital offerings, the adoption of generative AI-driven solutions like Amazon Bedrock will play an important role in maintaining operational excellence and delivering seamless experiences to customers. By following BMW’s example, your organization can also benefit from Amazon Bedrock Agents for root cause analysis to enhance service reliability.

Get started by exploring [Amazon Bedrock Agents](https://aws.amazon.com/bedrock/agents/) to optimize your incident diagnostics or use [CloudWatch Logs Insights](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/AnalyzingLogData.html) to identify anomalies in your system logs. If you want a hands-on introduction to creating your own Amazon Bedrock agents—complete with code examples and best practices—check out the following [GitHub repository](https://github.com/awslabs/amazon-bedrock-agent-samples/). These tools are setting a new industry standard for efficient RCA and operational excellence.