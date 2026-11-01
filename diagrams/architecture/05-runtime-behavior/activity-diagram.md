# Activity Diagram (UML)

Mermaid type: `flowchart` (Close fit). Source: Modeling-Diagraming.md, section "Runtime Behavior, Interactions & State".

Shows control flow, decisions, concurrent activities, and object flows, answering which steps run, which branches exist, and what work can happen in parallel.

## Example 1: Simple - Customer onboarding with parallel checks
```mermaid
flowchart TD
    S([Application received]) --> C[Collect customer data]
    C --> F{{Fork}}
    F --> K[Run KYC screening]
    F --> B[Run credit check]
    K --> J{{Join}}
    B --> J
    J --> D{"Both checks passed?"}
    D -- Yes --> O[Open account]
    D -- No --> R[Refer to analyst]
    O --> E([Onboarding complete])
    R --> E
```

## Example 2: Realistic - Card dispute handling
```mermaid
flowchart TD
    A([Dispute raised]) --> B{"Amount above 500 EUR?"}
    B -- Yes --> C[Assign to senior analyst]
    B -- No --> D[Assign to standard queue]
    C --> F{{Fork}}
    D --> F
    F --> E[Request merchant evidence]
    F --> G[Post provisional credit]
    E --> H{{Join}}
    G --> H
    H --> I{"Evidence accepted?"}
    I -- Yes --> J[Close in favor of customer]
    I -- No --> K[Debit provisional credit]
    J --> L([Dispute closed])
    K --> L
```
