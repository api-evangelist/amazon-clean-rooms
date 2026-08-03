# Amazon Clean Rooms (amazon-clean-rooms)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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
