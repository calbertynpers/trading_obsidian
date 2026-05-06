# AWS Dev — CLAUDE.md

> `CLAUDE.md` in the `aws_dev` workspace root
> Agent instructions for the AWS Deployment Framework project. Auto-loaded by Claude Code on every session.

```markdown
# Project: AWS Deployment Framework — Trading Platform

> **Agent instructions.** This file is auto-loaded on every session. Read it before doing anything.

---

## 1. What this project is

This is the **shared DevOps layer** for the trading platform ecosystem. It provisions AWS infrastructure and orchestrates deployments for all trading platform services using CloudFormation, setup scripts, and CI/CD pipelines.

**It is NOT an application project.** It contains infrastructure templates, deployment scripts, and automation — not application code.

### Services this project deploys

| Prefix | Service | Repo | Status |
|--------|---------|------|--------|
| BDS | Binance Data Collector / Position Tools | `binance_data_collector` | First deployment target |
| TIS | Trigger Ingestion System | `trigger_ingestion_system` | Future |
| TMS | Telegram MCP Server | `telegram-mcp-server` | Future |
| ALS | Alpha Scanner | `alpha_scanner` | Future |
| IDS | Idea Discovery Service | `idea_discovery_service` | Future |

---

## 2. Source of truth

- **Steering doc:** `.kiro/steering/aws-deployment-framework.md`
- **Tickets:** Obsidian vault at `Tickets/aws-deployment-framework/` (ADF-001 through ADF-007)
- **Ticket Index:** `Tickets/Ticket Index.md` in the vault
- **Service docs:** `Projects/binance-data-collector/Overview.md` in the vault

### Before starting any task

1. Read the relevant ADF ticket in the vault.
2. Read `.kiro/steering/aws-deployment-framework.md` for conventions.
3. Check existing scripts/templates for patterns — match them.
4. If the task touches a service (BDS, TIS, etc.), read that service's Overview doc in the vault.

---

## 3. AWS environment

| Property | Value |
|----------|-------|
| **Account ID** | `950858585111` |
| **Primary region** | `eu-north-1` (Stockholm) |
| **EC2 instance** | `i-0d3a293742aa3ad5c` (t3.small, AL2023, running) |
| **EC2 Elastic IP** | `13.53.240.97` (static) |
| **EC2 key pair** | `clint_dev_personal` |
| **EC2 security group** | `trading-sg-prod` (`sg-0375487fef0e42eb8`) |
| **IAM instance profile** | `trading-ec2-profile-prod` |
| **VPC** | `vpc-0e4c57f7f8d13d847` (default VPC eu-north-1) |
| **EC2 service dir** | `/opt/trading/bds/{data,config,logs,scripts}` |
| **Python on EC2** | 3.14.4 (via uv) |

### SSH access

ssh -i credentials/clint_dev_personal.pem ec2-user@13.53.240.97

---

## 4. Naming & tagging convention

Pattern: `trading-{service_prefix}-{resource_type}-{environment}`

Required tags: Project, Service, ServicePrefix, Environment, ManagedBy

---

## 5. Things to never do

- Never commit secrets, API keys, or PEM files to git
- Never run destructive AWS commands without explicit confirmation
- Never use `us-east-1` for resource operations — infra is in `eu-north-1`
- Never create resources without proper tags
- Never expose ports to `0.0.0.0/0` except HTTPS outbound

---

## 6. Phased architecture

Phase 1 (current):  EC2 + RDS PostgreSQL + Secrets Manager (~$35/month)
Phase 2 (next):     Add more services (TIS, TMS) to same EC2 + RDS
Phase 3 (future):   Containerize → Fargate + Aurora Serverless v2
```

## Notes

- This is a condensed version. The full CLAUDE.md in the repo has additional sections on ticket status, workflow, and repository layout.
- Update this vault copy when significant changes are made to the live CLAUDE.md.
