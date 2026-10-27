


<!-- [Diagram] -->

## State

```mermaid
stateDiagram-v2
    [*] --> Recieved
    Recieved --> Accepted
    Accepted --> Pending
    Accepted --> Rejected
    Pending --> Completed
    Pending --> Failed
    Completed --> [*]
    Rejected --> [*]
    Failed --> [*]
```
    click Recieved href "./recieved.md" "Open the Received document"
