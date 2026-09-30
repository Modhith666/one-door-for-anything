# ONEGATE Testing Strategy

## 1. Testing Objectives

The testing strategy verifies that ONEGATE:

* Understands user requests correctly
* Retrieves relevant enterprise information
* Selects the correct agent
* Creates valid task plans
* Executes authorized actions
* Protects restricted information
* Records important activities
* Provides a reliable user experience

---

## 2. AI / ML Testing

The AI components should be evaluated using a predefined test dataset.

### Metrics

* Intent classification accuracy
* Retrieval accuracy
* Source correctness
* Response relevance
* Groundedness
* Response consistency

### Example

```text
Input:
"What is our work-from-home policy?"

Expected Intent:
KNOWLEDGE

Expected:
Relevant policy document retrieved
+
Answer grounded in the document
+
Source displayed
```

---

## 3. RAG Testing

Test the complete RAG pipeline:

```text
User Query
    |
    v
Query Embedding
    |
    v
Vector Search
    |
    v
Relevant Documents
    |
    v
Context
    |
    v
LLM
    |
    v
Answer + Sources
```

### RAG Test Cases

Test whether:

* Relevant documents are retrieved
* Irrelevant documents are excluded
* Sources are correctly displayed
* Responses remain grounded in retrieved content
* Unauthorized documents are not retrieved
* No-answer cases are handled correctly

---

## 4. Intent Classification Testing

Test different categories of user requests.

| User Query                               | Expected Intent |
| ---------------------------------------- | --------------- |
| "I need three days leave."               | HR              |
| "My VPN is not working."                 | IT              |
| "Submit my client dinner expense."       | FINANCE         |
| "What is the work-from-home policy?"     | KNOWLEDGE       |
| "Prepare everything for a new employee." | ONBOARDING      |

Measure:

```text
Accuracy
Precision
Recall
F1 Score
```

---

## 5. Agent Testing

Each agent should be tested independently.

### Test

* Correct agent selection
* Correct task interpretation
* Correct tool selection
* Successful execution
* Invalid request handling
* Permission handling
* Failure handling

Example:

```text
Input:
"My VPN is not working."

Expected:

Intent → IT
Agent → IT Agent
Action → Create IT Support Request
```

---

## 6. Task Planner Testing

Test whether complex requests are correctly decomposed into tasks.

Example:

```text
User:
"Arjun is joining my team next Monday. Prepare everything."

Expected Plan:

1. Create employee onboarding request
2. Prepare HR onboarding tasks
3. Request IT account setup
4. Request required application access
5. Display plan for approval
6. Execute approved actions
7. Record results
```

---

## 7. Backend Testing

Test:

* API endpoints
* Request validation
* Authentication
* Authorization
* Database operations
* Error handling
* Audit logging
* Agent communication

Example:

```text
POST /api/chat
POST /api/intent
POST /api/rag/search
POST /api/plan
POST /api/approve
POST /api/execute
```

Each endpoint should have valid, invalid, and unauthorized test cases.

---

## 8. Frontend Testing

Test the main user journeys.

### Chat

* User enters request
* Request is submitted
* Response is displayed

### Action Plan

* Plan is displayed
* Tasks are understandable
* Status is visible

### Approval

* User can review action
* User can approve
* User can reject

### Activity

* Previous actions are displayed
* Status is correct
* Errors are understandable

---

## 9. Security Testing

Verify that:

* Unauthorized users cannot access restricted resources
* Unauthorized documents are excluded from RAG
* Unauthorized agents cannot execute restricted tools
* Approval is required for sensitive actions
* API keys are not exposed
* Audit logs are created for important actions

---

## 10. End-to-End Testing

The primary ONEGATE workflow is:

```text
User Request
    |
    v
Authentication
    |
    v
Intent Detection
    |
    v
RAG / Task Planning
    |
    v
Agent Routing
    |
    v
Action Plan
    |
    v
Human Approval
    |
    v
Tool Execution
    |
    v
Result
    |
    v
Audit Log
```

The complete workflow should be tested from the user's initial request through final execution.

---

## 11. Golden Test Cases

### Test Case 1 — HR

**Input:**

```text
I need three days leave next week.
```

**Expected:**

```text
Intent = HR
Agent = HR Agent
```

---

### Test Case 2 — IT

**Input:**

```text
My VPN is not working.
```

**Expected:**

```text
Intent = IT
Agent = IT Agent
```

---

### Test Case 3 — Finance

**Input:**

```text
I want to submit a client dinner expense.
```

**Expected:**

```text
Intent = FINANCE
Agent = Finance Agent
```

---

### Test Case 4 — Knowledge

**Input:**

```text
What is our work-from-home policy?
```

**Expected:**

```text
Intent = KNOWLEDGE
Agent / Service = RAG
Source = Relevant policy document
```

---

### Test Case 5 — Multi-Agent Onboarding

**Input:**

```text
Arjun is joining my team next Monday. Prepare everything.
```

**Expected:**

```text
Intent = ONBOARDING

Agents:
- HR Agent
- IT Agent

Expected:
Multi-step plan
+
Human approval where required
+
Workflow execution
+
Audit trail
```

---

## 12. Testing Workflow

All features should follow:

```text
Development
    |
    v
Unit Testing
    |
    v
Integration Testing
    |
    v
Security Testing
    |
    v
End-to-End Testing
    |
    v
Demo Validation
```

Testing should happen continuously during development rather than only at the end of the project.
