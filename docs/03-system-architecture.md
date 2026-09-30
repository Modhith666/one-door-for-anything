# ONEGATE System Architecture

## High-Level Architecture


                         USER
                           |
                           v
                  +----------------+
                  | ONEGATE FRONT  |
                  |     END        |
                  +-------+--------+
                          |
                          v
                  +----------------+
                  |   BACKEND API  |
                  +-------+--------+
                          |
                          v
                  +----------------+
                  | ORCHESTRATOR   |
                  +-------+--------+
                          |
             +------------+-------------+
             |            |             |
             v            v             v
        INTENT MODEL    RAG         TASK PLANNER
             |            |             |
             +------------+-------------+
                          |
                          v
                  +----------------+
                  |  AGENT ROUTER  |
                  +-------+--------+
                          |
          +---------------+---------------+
          |               |               |
          v               v               v
       HR AGENT        IT AGENT      FINANCE AGENT
          |               |               |
          +---------------+---------------+
                          |
                          v
                  ENTERPRISE TOOLS
                          |
                          v
                      APPROVAL
                          |
                          v
                      EXECUTION
                          |
                          v
                     AUDIT LOG
Major Components
##Frontend

Provides the user interface for interacting with ONEGATE.

##Backend

Provides APIs, authentication, authorization, database access,
workflow management, and integration.

##AI Layer

Provides intent detection, embeddings, retrieval, and
natural-language generation.

##RAG Layer

Retrieves relevant enterprise documents and provides grounded
responses.

##Agent Layer

Contains specialized agents for different enterprise domains.

##Orchestrator

Coordinates intent detection, retrieval, planning, agents,
approvals, and execution.

##Audit Layer

Records important actions and workflow events.
