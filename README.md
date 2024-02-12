# Death Plan

## Introduction

I was completely unprepared for my [friend](https://github.com/yhc-huichao)'s death. 

Without knowledge of his passwords or account details, we’re unsure how to access his digital assets, social
media accounts, email, enter his phone.

Therefore, I’m writing this tool to remember him, and to help myself and others handle this sad situation.

> Do not go gentle into that good night

## Process

```mermaid
flowchart LR
    subgraph "local init"
        A[file] -->|GPG encrypt| B[death-plan.md.gpg]
        B --> |upload|C[GitHub]
    end

    subgraph "workflow"
        D[tailscale] -->|status| id1{Any devices are online}
        id1 -->|yes| F0[reset cron]
        id1 -->|no| G[count++]
    end

    G -.- End[[notify]]
    H[schedule each month] --> id2{count > 3}
    id2 -->|no| D
    id2 -->|yes| F1[decrypt file to death-plan.md]
    F1 -.-> C
```

## Variables

- `secrets.WORKFLOW_TOKEN`: need workflow and repo read write access
- `secrets.TS_AUTH_KEY`: tailscale auth key
- `GPG_SIGNING_KEY`: gpg private key base64[^1]
- `GPG_PASSPHRASE`: gpg passphrase

## Projects

- [My blog](https://github.com/bxb100/bxb100.github.io/blob/main/.github/workflows/death-plan.yml)


[^1]: https://stackoverflow.com/questions/61096521/how-to-use-gpg-key-in-github-actions
