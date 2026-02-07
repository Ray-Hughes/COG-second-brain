---
type: project-overview
project: Patientevity
slug: patientevity
created: 2026-02-06
status: active
tags: ["#project", "#overview", "#ehr", "#patientevity"]
---

# Patientevity - EHR Platform

## Mission
Revolutionize behavioral health care through innovative technology that empowers healthcare providers to deliver exceptional patient care while maintaining the highest standards of security, compliance, and usability.

## What is this project?
A comprehensive, modern Electronic Health Records (EHR) system purpose-built for behavioral health practices. Multi-tenant SaaS platform serving psychiatrists, psychologists, therapists, counselors, and their clinical/administrative staff.

## Repositories

| Repo | Path | Branch | Purpose |
|------|------|--------|---------|
| **patientevity** (main) | `/home/decypherxc/development/patientevity` | `hotfix/go-live-cleanup` | Core EHR application |
| **patientevity-deployment** | `/home/decypherxc/development/patientevity-deployment` | `main` | Jenkins CI/CD + Ansible + GCP deployment |
| **patientevity-marketing** | `/home/decypherxc/development/patientevity-marketing` | `main` | Public marketing website |

## Tech Stack (Main EHR)

### Backend
- **Ruby 3.4.4** / **Rails 8.0.2**
- **PostgreSQL 15+** with pgvector, pg_trgm extensions
- **Inertia.js** (server-driven SPA - no separate API needed)
- **Solid Queue** / **Solid Cache** / **Solid Cable** (Rails 8 built-ins)
- **Karafka** for Kafka event-driven architecture
- **JWT** for API authentication, **bcrypt** for passwords
- **ActsAsTenant** for row-level multi-tenancy
- **Rack::Attack** for rate limiting
- **ROTP + rqrcode** for 2FA
- **LiveKit** for telehealth video calls
- **Prawn / WickedPDF / HexaPDF** for PDF generation
- **Stripe + Square** for payment processing
- **Google Vertex AI (Gemini)** for HIPAA-compliant AI
- **AWS Transcribe** for audio transcription
- **OpenTelemetry** for observability

### Frontend
- **React 19.1.0** with **TypeScript 5.8.3**
- **Vite** (via vite_rails) for build tooling
- **Tailwind CSS v4** + **Headless UI** + **Heroicons**
- **Inertia.js React adapter** for server-driven navigation
- **Action Cable** WebSockets for real-time features

### Testing
- **RSpec** (primary), **FactoryBot**, **Shoulda Matchers**
- **Capybara + Selenium** for system tests
- **SimpleCov** for coverage, **parallel_tests** for CI speed
- **Brakeman** for security scanning

### Database Scale
- **389 tables** in schema (as of 2026-02-06)
- Key domains: patients, providers, appointments, billing/claims, clinical notes, telehealth, organizations, accounting

## Current Status - Phase 1 Complete, Phase 2 In Progress

### Completed (Phase 1)
- Core EHR infrastructure with multi-tenant isolation
- Unified user system (patients, staff, associates)
- Permission-based authorization
- Patient management, clinical documentation, template builder
- Appointment scheduling system
- Billing with CPT codes, claims management, ERA processing
- Document management with e-signatures
- Patient portal (messaging, scheduling, insurance, records)
- Telehealth foundation (WebRTC, waiting room, AI transcription)
- Support portal with knowledge base and ticketing
- Custom Report Builder for claims/billing
- 379+ test examples

### Active Development (Phase 2)
- Telehealth video enhancements (WebRTC, screen sharing, multi-participant)
- AI-powered clinical assistant (SOAP notes, clinical flags)
- Advanced reporting & analytics
- Go-live cleanup and hotfixes

### Recent Commits
- Fix dark mode styling in Report Builder
- Custom Report Builder for Claims/Billing
- Unify Claims UI and Payers management
- Complete Appointment Scheduling System
- Go-live bug fixes

## Key Features
- **Multi-tenant** with subdomain routing and custom branding
- **Telehealth** with video calls, AI transcription, session recording
- **Claims & Billing** with ERA uploads, denial management, appeals
- **Clinical Documentation** with template builder and AI assistance
- **Patient Portal** with secure messaging, scheduling, payments
- **Support Portal** with knowledge base, ticketing, status page
- **Organization Payments** with Stripe/Square integration
- **Medical AI** for clinical suggestions (HIPAA-compliant via Vertex AI)

## Deployment Architecture
- **GCP Cloud Run** (blue/green deployment)
- **Cloud SQL** PostgreSQL 15 with pgvector
- **Jenkins** CI/CD with Ansible playbooks
- **Docker** containerized (Kamal-ready)
- **GCP Secret Manager** for credentials
- **GCP Artifact Registry** for Docker images
- 3 environments: development, staging, production

## Project Resources
- [[braindumps/|Project Braindumps]]
- [[competitive/|Competitive Intelligence]]
- [[content/|Content & Assets]]
- [[planning/|Planning Documents]]
- [[04-projects/patientevity-deployment/PROJECT-OVERVIEW|Deployment Pipeline]]
- [[04-projects/patientevity-marketing/PROJECT-OVERVIEW|Marketing Site]]

---

*This overview helps COG organize your project-related thoughts and updates.*
