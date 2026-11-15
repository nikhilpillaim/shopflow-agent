# ShopFlow Support Agent

## Problem Statement
Customers need an automated way to check their order status and determine return eligibility. If eligible, they need a frictionless way to automatically generate a Return Support Case. Additionally, the system must detect customer frustration and intelligently escalate the conversation to a human agent with a summary of the issue.

## Architecture
* **Agent:** ShopFlow Support (Agentforce)
* **Channels:** Messaging for Web / Enhanced Chat (API-ready)
* **Topics & Subagents:**
  * Case Creation (Topic)
  * Return Eligibility (Subagent)
  * Escalation (Subagent)
* **Custom Actions:** `Create_Return_Case` (linked via Asset Library)

## Flow Logic
1. **Input Collection:** The agent requests `var_Email` and `var_OrderNumber` from the user.
2. **Eligibility Check:** The agent queries the order status. If the order is not yet "Delivered", it blocks the return.
3. **Case Creation (Happy Path):** If delivered, the agent triggers the `Create Return Case` Flow.
4. **Flow Output:** The Flow creates the Case record in Salesforce and passes `var_OutputStatus` back to the agent to confirm success.
5. **Escalation Path:** If user frustration is detected via NLP, the Escalation subagent overrides standard topics and routes a summary to the human queue.

---
*Note: No passwords, API keys, or security tokens are included in this repository.*