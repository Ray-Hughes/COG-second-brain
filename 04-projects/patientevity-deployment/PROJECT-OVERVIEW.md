---
type: project-overview
project: Patientevity Deployment
slug: patientevity-deployment
created: 2026-02-06
status: active
tags: ["#project", "#overview", "#deployment", "#jenkins", "#devops"]
---

# Patientevity Deployment Pipeline

## What is this project?
Jenkins CI/CD pipeline with Ansible automation for deploying the Patientevity EHR platform to Google Cloud Platform. Handles blue/green deployments, feature flags, secrets management, and rollback procedures.

## Repository
- **Path**: `/home/decypherxc/development/patientevity-deployment`
- **Branch**: `main`
- **Parent Project**: [[04-projects/patientevity/PROJECT-OVERVIEW|Patientevity EHR]]

## Architecture

### Jenkins Pipelines
| Pipeline | File | Trigger | Purpose |
|----------|------|---------|---------|
| CI | `jenkins/Jenkinsfile.ci` | PR/Push | Tests, lint, security scan |
| CD | (main pipeline) | Manual/Push to main | Deploy to environments |
| Set-Features | `jenkins/Jenkinsfile.set-features` | Manual | Update feature flags |
| Set-Functions | `jenkins/Jenkinsfile.set-functions` | Manual | Update secrets/config |
| Rollback | `jenkins/Jenkinsfile.rollback` | Manual | Revert to previous version |

### Shared Libraries
- `vars/deployToGCP.groovy` - GCP deployment logic
- `vars/notifySlack.groovy` - Slack notifications
- `vars/healthCheck.groovy` - Health check verification
- `vars/runAnsible.groovy` - Ansible playbook execution

### Ansible Playbooks
- `base-bake.yml` - System packages, security, monitoring
- `app-bake.yml` - Ruby, Node.js, Nginx, Docker
- `build.yml` - Clone, bundle, assets, deploy
- `switch-traffic.yml` - Blue/green traffic switch
- `rollback.yml` - Rollback procedures
- `health-check.yml` - Health verification
- `setup-monitoring.yml` - Monitoring configuration

### Environments
| Environment | Trigger | Notes |
|-------------|---------|-------|
| Development | Auto on push to `develop` | Lower resources, debug logging |
| Staging | Auto on push to `staging` | Production-like, integration testing |
| Production | Manual approval | Full resources, blue/green active |

### GCP Infrastructure
- **Cloud Run** - Web service (blue/green) + Worker (SolidQueue)
- **Cloud Run Jobs** - Database migrations
- **Cloud SQL** - PostgreSQL 15 with pgvector (primary, cache, queue, cable DBs)
- **Secret Manager** - database-url, rails-master, secret-key, smtp configs
- **Artifact Registry** - Docker images
- **Cloud Storage** - Production bucket, voice bucket
- **Cloud Monitoring** - Metrics, logs, alerts, dashboards

### Deployment Strategy
Blue/green zero-downtime deployment:
1. Build Docker image and push to Artifact Registry
2. Run migrations via Cloud Run Job
3. Deploy new revision (green)
4. Health check
5. Switch traffic from blue to green
6. Old revision becomes standby for instant rollback

### Scripts
- `scripts/set-features.sh` - Feature flag management
- `scripts/set-functions.sh` - Cloud Functions config
- `scripts/import-credentials.sh` - Credential management
- `scripts/validate-deployment.sh` - Deployment validation

### Recent Commits
- Keep database running during hibernate for marketing site
- Use existing gcloud auth instead of service account key
- Add hibernate and resume jobs for cost savings
- Add developer setup guide and Jenkins job automation
- Fix migration status check race condition

## Documentation
- `docs/DEVELOPER_GUIDE.md` - Developer setup
- `docs/FEATURE_FLAGS.md` - Feature flag management
- `docs/SECRETS_MANAGEMENT.md` - Secrets handling
- `docs/runbooks/DEPLOYMENT.md` - Deployment runbook
- `docs/runbooks/ROLLBACK.md` - Rollback procedures

## Project Resources
- [[braindumps/|Deployment Braindumps]]
- [[planning/|Planning Documents]]

---

*This overview helps COG organize deployment-related thoughts and updates.*
