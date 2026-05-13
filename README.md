# Telecom CX Analytics Accelerator

## Overview

A comprehensive **Customer Experience Analytics** solution for telecommunications companies, built natively on Snowflake. This accelerator correlates network performance, service quality, and customer interactions to measure satisfaction, reduce churn, and optimize complaint resolution.

## Key Features

- **NPS Deep Dive** — Score distribution, segment analysis, promoter/detractor trends
- **Complaint Intelligence** — Category analysis, resolution time tracking, channel performance
- **Network & Root Cause** — Latency/speed analysis, outage correlation, region-level heatmaps
- **Churn & Retention** — Risk scoring, save-candidate identification, upsell opportunities
- **AI Summary & Chatbot** — Cortex-powered executive summaries and natural language Q&A

## Architecture

The app queries your source tables directly via Snowflake references — no intermediate materialization required:

```
Your Tables (via References) → Real-time Analytics → Interactive Dashboard
```

- **Zero data movement** — all queries run against your existing tables in-place
- **CX Health Score** computed at query time (NPS 25% + Complaints 25% + Latency 25% + Recency 25%)
- **Churn Risk Classification** — High/Medium/Low/Healthy based on composite signals
- **AI-powered insights** via Snowflake Cortex (Mistral Large 2)

## Data Requirements

The app requires 4 source tables mapped via references:

| Reference | Required Columns | Optional Columns | Description |
|-----------|-----------------|------------------|-------------|
| CUSTOMER | CUSTOMER_ID, PLAN_TYPE, REGION, CUSTOMER_SEGMENT, CHURN_FLAG | CUSTOMER_NAME, ACCOUNT_START_DATE, PHONE, CHURN_DATE | Customer master |
| NPS_SURVEY | CUSTOMER_ID, SURVEY_DATE, NPS_SCORE | SURVEY_ID, VERBATIM_COMMENT, SURVEY_CHANNEL | NPS responses |
| SERVICE_COMPLAINT | COMPLAINT_ID, CUSTOMER_ID, COMPLAINT_DATE, STATUS, COMPLAINT_CATEGORY, RESOLUTION_TIME_HOURS, CHANNEL | RESOLVED_DATE | Complaint records |
| NETWORK_PERFORMANCE | CUSTOMER_ID, EVENT_TIMESTAMP, DOWNLOAD_SPEED_MBPS, UPLOAD_SPEED_MBPS, LATENCY_MS, OUTAGE_FLAG | RECORD_ID, PACKET_LOSS_PCT | Network telemetry |

## Installation

1. Install the app from Snowflake Marketplace
2. Grant references to your source tables via the setup dialog (4 tables)
3. Grant the `SNOWFLAKE.CORTEX_USER` database role for AI features
4. Open the dashboard — it's immediately operational

