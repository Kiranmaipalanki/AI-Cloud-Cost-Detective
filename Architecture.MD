## AI Cloud Cost Detective - Architecture

```

                          ┌──────────────┐
                          │     USER     │
                          └──────┬───────┘
                                 │
                                 ▼
                       ┌───────────────────┐
                       │  REACT FRONTEND   │
                       └────────┬──────────┘
                                :
                                : Login / Signup
                                ▼
                       ┌───────────────────┐
                       │  PYTHON BACKEND   │
                       │    (FastAPI)      │
                       │                   │
                       │  · Custom JWT Auth│
                       └───┬───────┬───┬───┘
                           :       :   :
            ┌──────────────┘       :   └──────────────┐
            :                      :                  :
            ▼                      ▼                  ▼
     ┌─────────────┐     ┌──────────────┐    ┌──────────────┐
     │  AWS SDK    │     │   FASTAPI    │    │  GOOGLE AI   │
     │  (BOTO3)    │     │  WEBSOCKET   │    │   STUDIO     │
     │             │     │  (Progress)  │    │ (Gemini API) │
     │ boto3       │     └──────┬───────┘    │              │
     │ describe_*  │            :            │ Cost Analysis│
     └──────┬──────┘            :            └──────┬───────┘
            :                   : Live updates      :
            ▼                   ▼                   :
     ┌─────────────┐   ┌───────────────┐            :
     │    AWS      │   │    REACT      │            :
     │ (Account /  │   │  (Progress    │            :
     │  Region)    │   │   Tracker)    │            :
     └─────────────┘   └───────────────┘            :
                                                    ▼
                                             ┌──────────────┐
                                             │   AMAZON     │
                                             │     RDS      │
                                             │ (PostgreSQL) │
                                             │              │
                                             │ · users      │
                                             │ · analyses   │
                                             └──────┬───────┘
                                                    :
                                                    : Stored results
                                                    ▼
                                             ┌───────────────┐
                                             │    REACT      │
                                             │ (Final Report │
                                             │  + Suggestions│
                                             │  + Fixes)     │
                                             └───────────────┘

```
