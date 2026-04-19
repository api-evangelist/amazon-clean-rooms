# Amazon Clean Rooms (amazon-clean-rooms)
Amazon Clean Rooms enables organizations to collaborate and analyze shared datasets without exposing underlying raw data to partners. Create secure data clean rooms in minutes and collaborate with any company while maintaining data privacy through differential privacy, cryptographic computing, and flexible analytics.

**URL:** [Visit APIs.json URL](https://raw.githubusercontent.com/api-evangelist/amazon-clean-rooms/refs/heads/main/apis.yml)

**Run:** [Capabilities Using Naftiko](https://github.com/naftiko/fleet?utm_source=api-evangelist&utm_medium=readme&utm_campaign=company-api-evangelist&utm_content=repo)

## Tags:

 - AWS, Clean Rooms, Data Collaboration, Privacy, Analytics, Marketing

## Timestamps

- **Created:** 2026-03-16
- **Modified:** 2026-04-19

## APIs

### Amazon Clean Rooms API
API for creating and managing secure collaboration workspaces, memberships, configured tables, analysis templates, and executing privacy-preserving protected queries and jobs.

**Human URL:** [https://aws.amazon.com/clean-rooms/](https://aws.amazon.com/clean-rooms/)

#### Tags:

 - AWS, Clean Rooms, Data Collaboration, Privacy, Analytics

#### Properties

- [Documentation](https://docs.aws.amazon.com/clean-rooms/latest/apireference/)
- [OpenAPI](openapi/amazon-clean-rooms-openapi.yml)
- [GettingStarted](https://aws.amazon.com/clean-rooms/getting-started/)
- [Pricing](https://aws.amazon.com/clean-rooms/pricing/)
- [FAQ](https://aws.amazon.com/clean-rooms/faqs/)
- [APIReference](https://docs.aws.amazon.com/clean-rooms/latest/apireference/)
- [CLI](https://docs.aws.amazon.com/cli/latest/reference/cleanrooms/)
- [JSONSchema](json-schema/clean-rooms-collaboration-schema.json)
- [JSONLD](json-ld/amazon-clean-rooms-context.jsonld)

## Common Properties

- [Portal](https://aws.amazon.com/)
- [Website](https://aws.amazon.com/clean-rooms/)
- [SpectralRules](rules/amazon-clean-rooms-spectral-rules.yml)
- [Vocabulary](vocabulary/amazon-clean-rooms-vocabulary.yaml)
- [NaftikoCapability](capabilities/secure-data-collaboration.yaml)

## Features

| Name | Description |
|------|-------------|
| Privacy-Preserving Analytics | Analyze shared datasets without exposing underlying raw data using differential privacy and cryptographic computing. |
| Zero-ETL Integration | Collaborate with Snowflake and AWS datasets without data movement or ETL pipelines. |
| Protected Queries | Execute SQL, PySpark, or ML model queries on partner data with configurable privacy controls. |

## Use Cases

| Name | Description |
|------|-------------|
| Marketing Measurement | Measure campaign effectiveness by combining advertiser and publisher data in a privacy-safe environment. |
| Customer Insights | Build comprehensive customer views by combining data from multiple channels and partners. |

## Integrations

| Name | Description |
|------|-------------|
| Amazon S3 | Store and retrieve collaboration data and query results in S3. |
| Snowflake | Zero-ETL integration with Snowflake datasets for cross-platform collaboration. |
| AWS Glue | Configure Glue tables as data sources for Clean Rooms configured tables. |

## Artifacts

### OpenAPI

- [Amazon Clean Rooms API](openapi/amazon-clean-rooms-openapi.yml)

### JSON Schema

- [Collaboration](json-schema/clean-rooms-collaboration-schema.json)
- [Membership](json-schema/clean-rooms-membership-schema.json)
- [Protected Query](json-schema/clean-rooms-protected-query-schema.json)
- [Configured Table](json-schema/clean-rooms-configured-table-schema.json)

### JSON-LD

- [Amazon Clean Rooms Context](json-ld/amazon-clean-rooms-context.jsonld)

## Capabilities

### Shared Per-API Definitions

- [Amazon Clean Rooms](capabilities/shared/clean-rooms.yaml) — 10 operations for secure data collaboration management

### Workflow Capabilities

| Workflow | APIs Combined | Tools | Persona |
|----------|--------------|-------|---------|
| [Secure Data Collaboration](capabilities/secure-data-collaboration.yaml) | Clean Rooms | 9 | Data Analyst, Marketing Analyst |

## Vocabulary

- [Amazon Clean Rooms Vocabulary](vocabulary/amazon-clean-rooms-vocabulary.yaml) — Unified taxonomy mapping 4 resources, 5 actions, 1 workflow, and 2 personas

## Rules

- [Amazon Clean Rooms Spectral Rules](rules/amazon-clean-rooms-spectral-rules.yml) — 27 rules across 10 categories enforcing Amazon Clean Rooms API conventions

## Maintainers

**FN:** Kin Lane

**Email:** kin@apievangelist.com
