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
