# Death Plan

## Introduction

I was completely unprepared for my friend’s death, and his family and I are at a loss on how to manage his digital
assets. Without knowledge of his passwords or account details, we’re unsure how to access his digital assets, social
media accounts, email, bank, insurance, and investment accounts.
Therefore, I’m writing this to my family and friends to provide guidance on how to handle these matters in the event of
my death.

## Process

```mermaid
flowchart LR
    subgraph "local init"
        A[file] -->|GPG encrypt| B[GitHub]
        B --> C[encrypt file]
    end

    subgraph "workflow"
        D[tailscale] -->|status| id1{Any devices are online}
        id1 -->|yes| F0[reset cron]
        id1 -->|no| G[count++ and update cron]
    end

    G -.- End[notify]
    H[action trigger] --> id2{count > 3}
    id2 -->|no| D
    id2 -->|yes| F1[decrypt file]
    F1 -.-> C
```
