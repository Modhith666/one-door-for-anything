# ONEGATE Database Design

## 1. Users

Stores information about authenticated ONEGATE users.

| Field         | Description                |
| ------------- | -------------------------- |
| `user_id`     | Unique user identifier     |
| `name`        | User's name                |
| `email`       | User's enterprise email    |
| `department`  | User's department          |
| `role`        | User's role                |
| `permissions` | User permissions           |
| `created_at`  | Account creation timestamp |

---

## 2. Requests

Stores every request submitted through ONEGATE.

| Field        | Description                       |
| ------------ | --------------------------------- |
| `request_id` | Unique request identifier         |
| `user_id`    | User who submitted the request    |
| `query`      | Original natural-language request |
| `intent`     | Detected request intent           |
| `status`     | Current request status            |
| `created_at` | Request creation timestamp        |
| `updated_at` | Last update timestamp             |

### Example

```json
{
  "request_id": "REQ-001",
  "user_id": "USER-101",
  "query": "I need three days leave next week",
  "intent": "HR",
  "status": "processing"
}
```

---

## 3. Tasks

Stores individual tasks created by the planner or agents.

| Field         | Description                    |
| ------------- | ------------------------------ |
| `task_id`     | Unique task identifier         |
| `request_id`  | Parent request                 |
| `agent`       | Agent responsible for the task |
| `description` | Task description               |
| `status`      | Current task status            |
| `result`      | Task execution result          |
| `created_at`  | Task creation timestamp        |
| `updated_at`  | Last update timestamp          |

### Example

```json
{
  "task_id": "TASK-001",
  "request_id": "REQ-001",
  "agent": "HR",
  "description": "Check employee leave balance",
  "status": "completed",
  "result": "12 days available"
}
```

---

## 4. Approvals

Stores human approval decisions for sensitive actions.

| Field         | Description                    |
| ------------- | ------------------------------ |
| `approval_id` | Unique approval identifier     |
| `request_id`  | Related request                |
| `user_id`     | User responsible for approval  |
| `status`      | Pending, approved, or rejected |
| `approved_at` | Approval timestamp             |

### Example

```json
{
  "approval_id": "APR-001",
  "request_id": "REQ-001",
  "user_id": "MANAGER-101",
  "status": "approved",
  "approved_at": "2026-09-30T12:00:00"
}
```

---

## 5. Documents

Stores metadata for enterprise documents used by the RAG system.

| Field          | Description                 |
| -------------- | --------------------------- |
| `document_id`  | Unique document identifier  |
| `name`         | Document name               |
| `department`   | Owning department           |
| `access_level` | Required access level       |
| `version`      | Document version            |
| `created_at`   | Document creation timestamp |

### Example

```json
{
  "document_id": "DOC-001",
  "name": "Leave Policy.pdf",
  "department": "HR",
  "access_level": "employee",
  "version": "2.1"
}
```

---

## 6. Audit Logs

Records important actions performed within ONEGATE.

| Field        | Description                     |
| ------------ | ------------------------------- |
| `log_id`     | Unique log identifier           |
| `request_id` | Related request                 |
| `user_id`    | User who initiated the action   |
| `action`     | Action performed                |
| `agent`      | Agent that performed the action |
| `status`     | Action status                   |
| `timestamp`  | Time of action                  |
| `metadata`   | Additional information          |

### Example

```json
{
  "log_id": "LOG-001",
  "request_id": "REQ-001",
  "user_id": "USER-101",
  "action": "leave_request_created",
  "agent": "HR",
  "status": "success",
  "timestamp": "2026-09-30T12:05:00",
  "metadata": {
    "days": 3
  }
}
```

---

## 7. Relationships

```text
USER
  │
  │ 1
  ▼
REQUEST
  │
  │ 1:N
  ▼
TASK
  │
  └──────────────► AGENT

REQUEST
  │
  ├──────────────► APPROVAL
  │
  └──────────────► AUDIT LOG

DOCUMENT
  │
  └──────────────► RAG / VECTOR DATABASE
```

### Relationship Summary

* One **User** can create many **Requests**.
* One **Request** can contain multiple **Tasks**.
* A **Task** is assigned to an **Agent**.
* A **Request** can require one or more **Approvals**.
* A **Request** can generate multiple **Audit Logs**.
* **Documents** provide knowledge for the RAG pipeline.
* Document permissions must be checked before content is retrieved.

---

## 8. Initial Database Scope

For the prototype, the minimum required entities are:

```text
Users
Requests
Tasks
Approvals
Documents
Audit Logs
```

The schema can be extended later when additional enterprise
integrations and workflows are implemented.
