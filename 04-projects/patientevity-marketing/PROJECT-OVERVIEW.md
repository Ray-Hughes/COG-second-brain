---
type: project-overview
project: Patientevity Marketing
slug: patientevity-marketing
created: 2026-02-06
status: active
tags: ["#project", "#overview", "#marketing", "#website"]
---

# Patientevity Marketing Site

## What is this project?
Public-facing marketing website for Patientevity EHR. Showcases product features, pricing, blog content, and handles lead generation through demo requests and waitlist signups.

## Repository
- **Path**: `/home/decypherxc/development/patientevity-marketing`
- **Branch**: `main`
- **Parent Project**: [[04-projects/patientevity/PROJECT-OVERVIEW|Patientevity EHR]]

## Tech Stack
- **Ruby on Rails 8.0.2** (server-rendered, NOT a SPA)
- **PostgreSQL** database
- **Tailwind CSS** for styling
- **Stimulus.js (Hotwire)** for JavaScript interactivity
- **Propshaft** asset pipeline
- **Devise** for authentication (admin + user)
- **Kamal** for deployment (Docker-based)
- **Flipper** for feature flags

## Key Pages
| Page | View | Purpose |
|------|------|---------|
| Home | `app/views/home/index.html.erb` | Hero, features, CTAs |
| About | `app/views/about/index.html.erb` | Mission, team |
| Features | `app/views/features/index.html.erb` | EHR features, AI section |
| Pricing | `app/views/pricing/index.html.erb` | 3-tier pricing, comparison table |
| Blog | `app/views/blog/index.html.erb` | Articles, search, categories |
| Contact | `app/views/contact/index.html.erb` | Contact form, offices |

## Key Features

### Blog System
- Full-text search, category/tag filtering, pagination (Kaminari)
- Admin CRUD for posts, categories, tags
- View counters, related posts, social sharing
- SEO-friendly slugs

### Pre-Launch Mode (Feature Flags)
- `pre_launch` flag: Sign Up becomes "Join Waitlist", Login hidden, Pricing shows "Coming Soon"
- Waitlist system captures name, email, company, message
- Feature flag admin at `/admin/flipper`

### Pricing
- Starter, Professional, Enterprise tiers
- Monthly/annual toggle (Stimulus controller)
- Additional providers: $29/month
- Patient limits: 250 (Starter), 1000 (Professional)

### Admin Panel
- Custom Tailwind-based dashboard at `/admin`
- Blog post management, waitlist management
- Admin login: `admin@patientevity.com`

## Deployment
- **Kamal** with Docker
- **GitHub Actions** CI/CD (`deploy-staging.yml`)
- Dockerfiles for app (`Dockerfile`) and migrations (`Dockerfile.migrate`)

### Recent Commits
- Fix 18 failing tests
- Make CD workflow dependent on CI success
- Add comprehensive test coverage with system tests and Capybara
- Fix blog controller to only show published posts

## Models
- `BlogPost` - title, slug, content, excerpt, featured status, SEO fields
- `Category` / `Tag` - Blog organization
- `Comment` - Blog comments
- `Admin` - Admin users with roles
- `Waitlist` - Pre-launch signups

## Project Resources
- [[braindumps/|Marketing Braindumps]]
- [[planning/|Planning Documents]]

---

*This overview helps COG organize marketing-related thoughts and updates.*
