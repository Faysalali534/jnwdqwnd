graph TD
    subgraph "Data Sources"
        A[eCommerce Pixel/Webhook]
        B[Meta Ads API]
        C[Google Ads API]
    end

    subgraph "Ingestion & Storage"
        D[Cloud Run Ingestion API] --> E[Pub/Sub Topic]
        E --> F[GCS Raw Data Lake]
        E --> G[ClickHouse Raw Events Table]
        H[Airbyte Connectors] --> G
        B --> H
        C --> H
    end

    subgraph "Processing"
        I[dbt]
        G -- Reads from --> I
        F -- Batch Load (Optional) --> G
        I -- Writes to --> J[ClickHouse Reporting Tables]
    end

    subgraph "Serving & Orchestration"
        J --> K[Looker Studio Dashboards]
        J --> L[Reporting API]
        M[GitHub Actions CI/CD]
        N[Cloud Scheduler]

        M -- Deploys --> D
        M -- Deploys --> I
        M -- Deploys --> H
        N -- Triggers --> H
    end

    A -- HTTP --> D

    style D fill:#4285F4,stroke:#333,stroke-width:2px,color:#fff
    style E fill:#DB4437,stroke:#333,stroke-width:2px,color:#fff
    style F fill:#F4B400,stroke:#333,stroke-width:2px,color:#fff
    style G fill:#0F9D58,stroke:#333,stroke-width:2px,color:#fff
    style H fill:#9E9E9E,stroke:#333,stroke-width:2px,color:#fff
    style I fill:#FF6D00,stroke:#333,stroke-width:2px,color:#fff
    style J fill:#0F9D58,stroke:#333,stroke-width:2px,color:#fff
    style K fill:#673AB7,stroke:#333,stroke-width:2px,color:#fff
    style L fill:#673AB7,stroke:#333,stroke-width:2px,color:#fff
    style M fill:#24292E,stroke:#333,stroke-width:2px,color:#fff
    style N fill:#4285F4,stroke:#333,stroke-width:2px,color:#fff
