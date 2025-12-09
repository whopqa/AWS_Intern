---
title: "Week 13 Worklog"
date: 2025-09-10
weight: 13
chapter: false
pre: " <b> 1.13 </b> "
---


### Week 13 Objectives:

* Finalize and optimize appointment scheduling flow with edge case handling.
* Address throttling and timeout issues in the system.
* Improve prompt engineering to increase bot accuracy.
* Optimize vector search and schema retrieval.
* Deploy, test, and fix bugs in production environment.
* Complete documentation and demo.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 1   | - Continue developing appointment scheduling flow alongside deploy testing <br> - Add Webhook Receiver to handle requests from Messenger: <br>&emsp; + Deploy SQS to avoid Lambda timeout <br>&emsp; + Prevent multiple response returns <br> - Handle throttling error when invoking Lambda (too many bot calls) <br> - Improve prompt for SQL mutation: <br>&emsp; + Fix column, table, param errors <br>&emsp; + Add annotations for enum params and user input params <br> - Optimize schema search using embedding: <br>&emsp; + Create filter function to get top closest tables <br>&emsp; + Improve similarity score by adding string annotations to table names <br> - Update permissions: <br>&emsp; + Admin for mutation SQL (DB admin secret) <br>&emsp; + Readonly for SELECT SQL | 12/01/2025 | 12/01/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 2   | - Merge 2 development branches and deploy test <br> - Handle discovered issues: <br>&emsp; + Mutation SQL prompt lacks flexibility when schema changes <br>&emsp; + Hallucination: Bot responds normally when no SQL results <br>&emsp; + Throttling still occurs <br>&emsp; + Response too long (>2000 characters) prevents Messenger processing <br> - Improve prompts: <br>&emsp; + Add prompt to respond based on SQL results (no results → respond according to context) <br>&emsp; + Adjust extraction prompt to understand final intent before extracting information <br>&emsp; + Avoid bias into context <br>&emsp; + Require output <2000 characters <br> - Test model upgrade: <br>&emsp; + Switch Claude 3 Haiku → Claude 3.5 Sonnet <br>&emsp; + Use cross-region (trade-off higher latency → timeout) | 12/03/2025 | 12/03/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 2   | - Update new appointment scheduling flow: <br>&emsp; **Create Flow:** <br>&emsp;&emsp; • Information extraction prompt starts when intent is booking create <br>&emsp;&emsp; • Switch to collecting state <br>&emsp;&emsp; • No need to call intent classification prompt in collecting state <br>&emsp;&emsp; • Call extraction prompt → check field → response ask → allow user to ask more <br>&emsp;&emsp; • Repeat until consultant name, date, time are sufficient <br>&emsp;&emsp; • Display waiting message → get available slots → cache index <br>&emsp;&emsp; • User selects slot → confirm → confirm state → mutation → notify → idle <br>&emsp; **Update Flow:** <br>&emsp;&emsp; • Intent update → selecting slots state <br>&emsp;&emsp; • Get booked appointments by customer ID → cache index → user selects <br>&emsp;&emsp; • Save old and new appointment params → switch to collecting state <br>&emsp;&emsp; • Update: Cancel old appointment + Insert new appointment <br>&emsp; **Delete Flow:** <br>&emsp;&emsp; • Get appointments by customer ID → user selects → confirm → mutation cancel | 12/03/2025 | 12/03/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Adjust model temperature to increase accuracy <br> - Fix Vietnamese comparison error: <br>&emsp; + Don't use regular ILIKE <br>&emsp; + Use unaccent in DB schema <br> - Improve ID retrieval prompt: <br>&emsp; + More flexible with soft information (consultant name) <br>&emsp; + Use SELECT OR instead of requiring full name, date, time <br> - Merge intent recognition and extraction info into one prompt (Claude 3 Sonnet) <br> - Add constraints: <br>&emsp; + Query customer information only by ID <br>&emsp; + Get consultant schedule only for current and future time | 12/05/2025 | 12/05/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Complete smarter welcome message <br> - Modifications: <br>&emsp; + Only get user appointments with "pending" status <br>&emsp; + Constraint for getting appointments: time > current_time if day = current_day <br> - Revise proposal document <br> - Write README documentation <br> - Prepare and perform system demo | 12/07/2025 | 12/07/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Week 13 Achievements:

**Handling Throttling and Timeout Issues:**
* Deployed SQS as message queue between Messenger and Lambda:
  - Webhook receiver receives requests from Messenger and pushes to SQS
  - Lambda consumer processes messages from queue
  - Prevents multiple response returns due to timeout
  - Minimizes throttling errors when too many concurrent requests
* Handled Lambda invocation throttling error during SQL mutation for appointments
* Configured database access permissions:
  - Admin secret for mutation SQL (INSERT/UPDATE/DELETE)
  - Readonly permission for SELECT SQL

**Optimizing Vector Search and Schema Retrieval:**
* Improved schema search efficiency using embedding:
  - Created filter function to get top tables with highest similarity
  - Added string annotations for each table name to improve similarity score
  - Reduced number of returned schemas from too many to only most relevant tables
* Addressed low similarity score and inaccurate results issues

**Improving Prompt Engineering:**
* Upgraded prompt for SQL mutation:
  - Fixed column, table, parameter errors
  - Added detailed guidance on enum parameters
  - Clarified which parameters users need to input
  - Increased flexibility when schema changes
* Addressed hallucination issues:
  - Bot responds based on actual SQL results
  - When no SQL results → respond according to context instead of rigid responses
  - Avoid bias into irrelevant context
* Optimized output:
  - Required response <2000 characters for Messenger processing
  - Adjusted model temperature to increase accuracy
* Improved extraction prompt:
  - Understand user's final intent before extracting information to fill fields
  - Merged intent recognition and extraction info into one prompt for Claude 3 Sonnet

**Completing Appointment Scheduling Flow:**
* **Create Flow (New appointment):**
  1. Identify intent as booking create → switch to collecting state
  2. No need to call intent classification prompt in collecting state
  3. Call information extraction prompt → check required fields
  4. Return response asking for missing information → allow user to ask more
  5. Repeat until consultant name, date, time are sufficient
  6. Display waiting message → call prompt to get available slots
  7. Cache index new appointment information (consultant id, name, date, time)
  8. User selects slot → get information as params
  9. User confirms → confirm state → mutation prompt → execute
  10. Notify success/failure → return to idle state

* **Update Flow (Update appointment):**
  1. Identify intent update → selecting slots state
  2. Automatically get booked appointments by customer ID → cache index
  3. User selects appointment to change
  4. Save time, date, consultant id of old appointment to params
  5. Save customer id, email, phone to new appointment params
  6. Switch to collecting state (similar to create)
  7. Execute: Cancel old appointment (update status) + Insert new appointment

* **Delete Flow (Cancel appointment):**
  1. Identify intent delete
  2. Automatically get booked appointments by customer ID → cache index
  3. User selects appointment to cancel
  4. Get old appointment information
  5. User confirms → mutation SQL (update status to "cancelled")

**Handling Vietnamese and Database:**
* Fixed Vietnamese comparison error:
  - Don't use regular ILIKE
  - Configure and use unaccent extension in PostgreSQL
  - Re-setup in DB schema to support Vietnamese search without diacritics
* Improved ID retrieval prompt based on soft information:
  - More flexible with information like consultant name
  - Use SELECT OR instead of requiring full consultant name, date, and time

**Model Testing and Cross-Region:**
* Upgraded from Claude 3 Haiku to Claude 3.5 Sonnet:
  - Improved response quality
  - Better context understanding
* Used cross-region inference:
  - Trade-off between model quality and latency
  - Higher latency but may cause timeout
  - Need to balance between performance and latency

**Constraints and Business Logic:**
* Added business constraints:
  - Query customer information only by customer ID
  - Get consultant schedule only for current and future time
  - Only get user appointments with "pending" status
  - Get appointments: time > current_time if day = current_day
* Completed smarter welcome message with context

**Documentation and Demo:**
* Revised and completed proposal document
* Wrote comprehensive README documentation
* Successfully prepared and performed system demo

**Lessons Learned and Insights:**
* Model temperature significantly affects information extraction accuracy
* Merging multiple prompts into one can reduce API calls and increase consistency
* Vector search needs careful fine-tuning with annotations to achieve good similarity
* Cross-region inference is a trade-off between model quality and latency
* SQS is an effective solution for throttling and timeout issues
* Vietnamese handling requires unaccent extension in PostgreSQL
* Business logic constraints are crucial to avoid invalid data
