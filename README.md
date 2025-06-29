# AdTech Real-Time Event Tracking Pipeline

This project implements a scalable, production-grade, real-time event tracking pipeline on Google Cloud Platform. It is designed to handle high-volume event ingestion, processing, and analytics for AdTech applications.

## 🚀 Project Overview

This pipeline is designed to address the challenges of tracking and analyzing millions of daily events from various sources, such as website pixels, server-side webhooks, and third-party advertising platforms like Meta and Google Ads.

### Key Features:
- **Cloud-Native & Serverless:** Built entirely on GCP, leveraging serverless components like Cloud Run and Cloud Functions for scalability and cost-efficiency.
- **Real-Time Processing:** Events are processed and made available for analytics in near real-time.
- **Scalable & Decoupled:** The architecture is designed to handle high throughput and is decoupled using Pub/Sub to ensure reliability.
- **Infrastructure as Code:** All infrastructure is managed using Terraform for reproducibility and version control.
- **CI/CD Automation:** Deployment is fully automated with GitHub Actions.
- **Modular Data Modeling:** Data transformations are managed with dbt for maintainability and data quality.

## 📐 System Architecture

A detailed diagram of the system architecture can be found in [`architecture_diagram.md`](./architecture_diagram.md).

The pipeline consists of several layers, each with a specific responsibility:

1.  **Ingestion:** A containerized Node.js API on Cloud Run receives events and publishes them to a Pub/Sub topic.
2.  **Storage:** Raw events are stored in a Google Cloud Storage data lake for auditing and replay, while the analytical data is stored in a high-performance ClickHouse database.
3.  **Processing:** A Cloud Function loads data from Pub/Sub into ClickHouse in micro-batches. Airbyte is used to sync third-party API data, and dbt is used to transform and model the data for reporting.
4.  **Serving:** A lightweight reporting API on Cloud Run exposes analytical endpoints, and the data is ready to be connected to a BI tool like Looker Studio.
5.  **Orchestration & CI/CD:** GitHub Actions automates the entire deployment process, and Cloud Scheduler can be used for scheduling tasks.

## 💾 Database Design

A detailed diagram of the database schema can be found in [`database_diagram.md`](./database_diagram.md).

The analytical database schema in ClickHouse is designed for high-performance time-series analysis.

## 🛠️ Getting Started

To deploy this project, you will need:
- A Google Cloud Platform project with billing enabled.
- A service account with appropriate permissions (`roles/owner` for simplicity, or more granular permissions for production).
- A GitHub repository with secrets configured for `GCP_PROJECT_ID` and `GCP_SA_KEY`.
- A ClickHouse Cloud account and API credentials.

Once the prerequisites are met, pushing to the `main` branch will trigger the GitHub Actions workflow and deploy the entire pipeline.
