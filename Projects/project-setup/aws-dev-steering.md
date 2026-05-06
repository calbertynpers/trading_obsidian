# AWS Dev — Steering File

> `.kiro/steering/aws-deployment-framework.md`
> Architecture decisions and conventions for the AWS Deployment Framework. Auto-included in all Kiro sessions for this workspace.

```markdown
---
inclusion: auto
---

# AWS Deployment Framework — Project Steering

## Purpose

This project is the shared DevOps layer for the trading platform ecosystem. It provisions AWS infrastructure and orchestrates deployments for all trading platform services using CloudFormation and CodeBuild/CodeDeploy.

## Architecture Decisions

### Single AWS Account
All services deploy to a single AWS account. No multi-account strategy. Environments separated by resource naming and tags.

### Compute Strategy
- **EC2** for Phase 1 (cheapest, simplest)
- **ECS Fargate** for Phase 3 (containerized, auto-scaling)
- Decision is per-service, documented in that service's `deploy.yml` manifest

### Database
- **RDS PostgreSQL** — standard for all services
- Shared instance (db.t4g.micro), separate databases per service
- Phase 3: Aurora Serverless v2

### Infrastructure as Code
- **CloudFormation** — all infrastructure defined as templates
- No Terraform, no CDK — keep the toolchain simple

### CI/CD
- **CodeBuild** — builds and tests
- **CodeDeploy** — deployment orchestration
- **CodePipeline** — ties build + deploy together
- Source: GitHub (webhook-triggered)

## Naming & Tagging Convention

### Resource Naming
Pattern: `trading-{service_prefix}-{resource_type}-{environment}`

### Required Tags
| Tag | Example | Purpose |
|-----|---------|---------|
| `Project` | `trading-platform` | Cost allocation |
| `Service` | `binance-position-tools` | Service identification |
| `ServicePrefix` | `BDS` | Short identifier |
| `Environment` | `prod` | Environment separation |
| `ManagedBy` | `cloudformation` | Drift detection |

## Cross-Project Ticket Model

When a service needs AWS deployment, two tickets are created:
1. In the service's ticket folder — app-side deployment readiness
2. In `Tickets/aws-deployment-framework/` — infra provisioning

Ticket prefix: **ADF**

## Service Prefixes

| Prefix | Service | Compute | Database |
|--------|---------|---------|----------|
| BDS | Binance Position Tools | EC2 → Fargate | PostgreSQL |
| TIS | Trigger Ingestion System | EC2 → Fargate | PostgreSQL |
| TMS | Telegram MCP Server | EC2 → Fargate | None |
| ALS | Alpha Scanner | EC2 → Fargate | PostgreSQL |
| IDS | Idea Discovery Service | EC2 → Fargate | TBD |

## Key Constraints

- Keep costs minimal — personal trading platform, not enterprise
- No over-engineering — simplest viable setup per service
- Security basics: Secrets Manager, no hardcoded credentials, least-privilege IAM
```

## Notes

- This steering file has `inclusion: auto` — it's loaded into every Kiro session for the aws_dev workspace
- Other projects that need AWS deployment context should reference this via the vault, not copy it locally
- The steering file evolves as the architecture matures through phases
