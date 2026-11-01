# Data Flow Volumes

Mermaid type: `sankey-beta` (beta). Shows transaction volumes flowing from channels to reporting.

```mermaid
sankey-beta

Mobile app,Payment API,500
Online banking,Payment API,300
Branch,Payment API,200
Payment API,Fraud check,1000
Fraud check,Core ledger,930
Fraud check,Manual review,70
Core ledger,Data warehouse,930
Manual review,Data warehouse,70
```
