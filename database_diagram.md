erDiagram
    events_raw {
        UUID event_id PK
        String client_id
        DateTime64 received_at
        String event_source
        String event_type
        String payload
    }

    fact_conversions {
        UUID conversion_id PK
        String client_id
        DateTime converted_at
        String user_id
        String device_id
        Float revenue
        String currency
    }

    fact_ad_performance {
        Date date PK
        String source PK
        String campaign_id PK
        String campaign_name
        Float ad_spend
        Int clicks
        Int impressions
    }

    events_raw ||--o{ fact_conversions : "dbt model"
    events_raw ||--o{ fact_ad_performance : "Airbyte + dbt"
