# k8s-resource-optimizer

> **Most Kubernetes clusters waste 50–70% of their resources — or crash under load because they're under-provisioned.**
> Existing autoscalers react to single metrics. They don't forecast, don't optimize across trade-offs, and don't protect against unsafe changes.
> We built something different.

---

## What Makes This Different

| Existing tools | This project |
|---|---|
| React to current metrics | **Forecast** future demand (Holt-Winters, trend decomposition) |
| Optimize for one objective | **Pareto-optimal** recommendations — cost vs. performance vs. reliability |
| No safety guarantees | **Circuit breakers, SLA monitoring, automatic rollback** built in |
| Suggest or scale | **Generate GitOps PRs** — auditable, reviewable, automated |

---

## How It Works

```mermaid
flowchart LR
    subgraph K8S["☸ Kubernetes Cluster"]
        W1[Workload A]
        W2[Workload B]
        W3[Workload C]
    end

    subgraph OPT["🧠 Optimizer Controller"]
        direction TB
        SA["📈 Statistical Analysis\nHolt-Winters · Trend · Forecast"]
        PO["⚖️ Pareto Optimization\nCost · Performance · Reliability"]
        SL["🛡️ Safety Layer\nCircuit Breaker · Rollback · SLA"]
        PE["📋 Policy Engine"]

        SA --> PO --> SL --> PE
    end

    subgraph OUT["📦 Output"]
        GIT["GitOps PR\nKustomize / Helm patch"]
        MON["Grafana Dashboard\nPrometheus Metrics"]
    end

    K8S -- "metrics" --> SA
    PE -- "recommendations" --> GIT
    OPT -- "observability" --> MON
    GIT -- "applies" --> K8S

    style K8S fill:#dbeafe,stroke:#3b82f6,color:#1e3a5f
    style OPT fill:#f0fdf4,stroke:#22c55e,color:#14532d
    style OUT fill:#fefce8,stroke:#eab308,color:#713f12
```

---

## Stack

`Go` · `Kubernetes controller-runtime` · `Prometheus` · `Grafana` · `Kustomize` · `Helm` · `kind`

---

## Repositories

| | |
|---|---|
| [`intelligent-cluster-optimizer`](https://github.com/k8s-resource-optimizer/intelligent-cluster-optimizer) | Controller, optimizer engine, safety layer, GitOps integration, monitoring |
| [`optimizer-test`](https://github.com/k8s-resource-optimizer/optimizer-test) | 600+ unit, integration, and E2E tests |

---

**[Azra Karakaya](https://github.com/azrakarakaya1) · [Erva Şengül](https://github.com/ervasengul)**
Istanbul Medipol University · Computer Engineering · 2024–2025
