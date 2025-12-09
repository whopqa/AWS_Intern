---
title: "Week 12 Worklog"
date: 2025-09-10
weight: 2
chapter: false
pre: " <b> 1.12. </b> "
---


### Week 12 Objectives:

* Restructure and optimize Chatbot system architecture.
* Build efficient session management and caching mechanisms.
* Develop service files following decoupling principles.
* Implement intelligent appointment scheduling flow with LLM.
* Deploy and test appointment scheduling system in production environment.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   | - Design Reset Session mechanism after 15 minutes to save costs <br> - Create confirmation state for appointment information before saving to DB <br> - Restructure code base following decoupling principles: <br>&emsp; + Session Service: manage session, LLM context, timeout, cache <br>&emsp; + Bedrock Service: specialized prompts (intent classification, SQL query, response) <br>&emsp; + Authenticator Service: user authentication <br>&emsp; + Embed Service: call embedding model and get vector <br>&emsp; + Indexer Service: create embedding table schema <br>&emsp; + Messenger Service: send messages to user <br> - Build Handler Files: <br>&emsp; + Chat Handler: handle conversation logic <br>&emsp; + Text2SQL Handler: handle query and execute SQL on Facebook <br> - Restructure data flow for Admin | 11/24/2025 | 11/24/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - Analyze appointment scheduling business questions: <br>&emsp; + "What time slots are available?" <br>&emsp; + "I'm free now, can you suggest the most suitable time?" <br> - Learn main schema in appointment scheduling system <br> - Design optimal appointment scheduling mechanism: <br>&emsp; + Hold appointments temporarily in cache (2-3 minutes) to avoid conflicts <br>&emsp; + Handle conflicts when multiple users book simultaneously <br>&emsp; + Provide confirmation token for first requester <br> - Cache available slots to increase response speed <br> - Check duplicate questions with cache to reuse previous answers <br> - Research Reflection mechanism with LLM when SQL returns incorrect results <br> - Apply Prompt-based Few-shot Learning <br> - Evaluate using SQS <br> - Design Table Cache structure: <br>&emsp; + Rolling Summary for conversations (token limit) <br>&emsp; + Cache appointment questions (SQL statement, text, response, query result, prompt, schema, column name) <br> - Setup SQS to avoid Lambda timeout | 11/25/2025 | 11/25/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Create function to get conversation context for LLM <br> - Build Context structure for main Model (Sonnet/Haiku): <br>&emsp; + System Prompt: define bot rules <br>&emsp; + Structured Summary (from Cache): summarize business state <br>&emsp; + Recent History: keep last 2-3 conversation turns <br> - Develop Bedrock Service with caching mechanism: <br>&emsp; + Compare query with previous questions using LLM <br>&emsp; + Return from cache if relevant <br>&emsp; + Save metadata for each turn <br>&emsp; + Keep last 3 turns to save tokens <br> - Complete most Service Files <br> - Build Session Table structure in DynamoDB | 11/26/2025 | 11/26/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Add jsonState to appointment field in Session Table <br> - Determine accurate intent classification method (SQL query vs RAG) <br> - Prepare context for bot to understand conversation context <br> - Code Chat Handler to orchestrate conversation logic flow <br> - Handle issue of short questions lacking context <br> - Complete preliminary conversation flow <br> - Ready to test appointment scheduling flow <br> - Notes: <br>&emsp; + Intent Classify and RAG Service not completed <br>&emsp; + Session cancel/delete time not set <br>&emsp; + JSON template for appointment not applied | 11/27/2025 | 11/27/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Deploy and test appointment scheduling flow separately <br> - Handle DynamoDB issue not saving float data for vector: <br>&emsp; + Convert vector to string when writing session <br>&emsp; + Convert back when searching cache <br> - Change region: <br>&emsp; + Singapore doesn't have embedding model <br>&emsp; + Host to Tokyo (trade-off latency) <br> - Enable Claude model in Playground <br> - Develop two specialized Prompts: <br>&emsp; + Mutation Prompt: constraints for INSERT/UPDATE SQL <br>&emsp; + Query Prompt: specialized for querying table information <br> - Implement appointment scheduling Logic flow: <br>&emsp; + Determine intent (query vs appointment) <br>&emsp; + Divide into 3 sub-flows: Schedule / Update / Cancel <br>&emsp; + Print available appointment information and index cache <br>&emsp; + Extract customer information using LLM <br>&emsp; + Confirm and execute appointment <br> - Identify limitation: Logic may print too many appointments at once | 11/28/2025 | 11/28/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Week 12 Achievements:

**System Restructuring Following Decoupling Principles:**
* Successfully built Service-based architecture with independent modules:
  * **Session Service:** Manage sessions with features:
    - Create new session with predefined fields
    - Update and delete sessions
    - Get session information and context for LLM
    - Check timeout and state
    - Save cache and search using vector search
  * **Bedrock Service:** Manage specialized prompts:
    - Intent classification
    - SQL queries
    - Generate responses
  * **Authenticator Service:** User authentication
  * **Embed Service:** Call embedding model and get vector
  * **Indexer Service:** Create embedding table schema
  * **Messenger Service:** Manage sending messages to users
* Built Handler Files:
  * **Chat Handler:** Handle conversation logic
  * **Text2SQL Handler:** Handle query and execute SQL directly on Facebook
* Restructured data flow for Admin.

**Session and Caching Mechanism Optimization:**
* Designed Reset Session mechanism after 15 minutes to save costs when appointment information is not confirmed.
* Created confirmation state to ensure template has complete information before saving to DB.
* Built Session Table structure in DynamoDB with jsonState field in appointment.
* Designed intelligent caching mechanism:
  - **Rolling Summary:** Summarize conversations with token limit via cheaper LLM
  - **Query Caching:** Store SQL statement, text, response, query result, prompt text, schema_text, column name
  - **Recent History:** Keep last 3 turns to save tokens
  - **Vector Search:** Compare query with previous questions using LLM

**Building Context for LLM:**
* Designed Context structure for main Model (Sonnet/Haiku):
  - **System Prompt:** Define bot rules
  - **Structured Summary (from Cache):** Summarize business state (e.g., "Customer A, wants appointment on day X, time not confirmed")
  - **Recent History:** Keep last 2-3 turns verbatim for bot to capture tone and immediate previous questions
* Prepare context for bot each call to understand conversation context.

**Developing Intelligent Appointment Scheduling Flow:**
* Analyzed and handled business questions:
  - "What time slots are available?"
  - "I'm free now, can you suggest the most suitable time?"
* Designed optimal appointment scheduling mechanism:
  - **Temporary hold:** Cache appointments for 2-3 minutes to avoid conflicts when multiple users book simultaneously
  - **Confirmation token:** First requester receives token to continue confirmation
  - **Wait notification:** Other cases are notified to wait for latest updates
  - **Cache available slots:** Increase response speed, update when DB changes
  - **Check duplicates:** Check if user question has same meaning as previous ones to resend old answers
* Implemented Logic flow with 3 main branches:
  1. **New appointment:** Print available appointment information → User selects → Extract information using LLM → Confirm → Execute
  2. **Update appointment:** Automatically print user's existing appointments → User selects appointment to update → Modify information → Confirm → Execute
  3. **Cancel appointment:** Automatically print user's existing appointments → User selects appointment to cancel → Confirm → Cancel appointment

**Developing Specialized Prompts:**
* **Mutation Prompt:** Contains specialized constraints for INSERT/UPDATE SQL
* **Query Prompt:** Specialized for querying table information
* Researched Reflection mechanism with LLM when SQL returns incorrect results.
* Applied Prompt-based Few-shot Learning.

**Deployment and Technical Issue Resolution:**
* Successfully deployed and tested appointment scheduling flow separately.
* Handled DynamoDB issue not saving float data:
  - Convert vector to string when writing session
  - Convert back when searching cache
* Changed region for embedding model:
  - Singapore region doesn't have embedding model
  - Host to Tokyo (trade-off latency)
* Enabled Claude model in Playground for use.
* Setup SQS to avoid Lambda timeout.

**Lessons Learned and Challenges:**
* Determined accurate intent classification method between SQL query and RAG.
* Handled issue of short questions lacking context (e.g., "What time?" → Whose time?).
* Identified limitation: Current logic may print too many appointments at once, not intelligent enough.
* Incomplete parts:
  - Intent Classify and RAG Service
  - Session cancel/delete time
  - JSON template for appointments
