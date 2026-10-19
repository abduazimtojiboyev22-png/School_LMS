# Maktab LMS backend scope

Audit date: 2026-10-19  
Source: `Maktab_LMS_plan.txt` and the repository state available in this workspace.

## Purpose

Build a backend-only LMS for one school in small, reviewable steps. This document records the agreed boundary for the 15-lesson prompt sequence; it is not a statement that the backend is already implemented or production-ready.

The referenced `Maktab_LMS_Arxitektura_15_Dars.pdf` was not present in the workspace during this audit. Alignment with that PDF is therefore unverified; the boundary below follows the supplied TXT plan.

## Product boundary

- One school; business user roles are `pupil` and `teacher`.
- `manage_accounts` and `manage_academics` are teacher capabilities, not additional business roles. A Django superuser is a technical administration account.
- Backend APIs and operational support are in scope. Frontend, mobile clients, public registration, parent role, multi-tenant SaaS, GraphQL, microservices, Kubernetes, and automatic timetable solving are out of scope.
- The planned core includes academic catalogs and enrollments, course topics and private resources, assignments/submissions, grading, timetable and attendance, in-app notifications, exams, dashboards, deployment support, and an optional teacher-reviewed AI draft workflow.
- AI, antivirus, broker, cache, and object storage integrations are added only at their designated prompts. A mock or local adapter must not be reported as a real external integration.

## Architecture and teaching constraints

- Adapt the current repository; do not generate a second project or discard existing work.
- Use Django session authentication with CSRF protection. JWT, wildcard CORS, and public signup are not part of this plan.
- Keep database datetimes timezone-aware and UTC-based; school schedule wall-clock values use `Asia/Tashkent`. The final API serialization and frontend display contract must be made explicit in the designated contract prompts.
- PostgreSQL is authoritative for persisted business data and concurrency rules. Redis is not the only copy of grades or answers.
- Keep pupil data scoped to the current pupil/course permissions. Private files are unavailable until a real scan marks them clean.
- Preserve published content, submitted revisions, grading history, and enrollment history. Use transactions and idempotency for important workflows.
- Work one prompt at a time in the listed order. Verify its acceptance criteria before starting the next prompt. The sequence is P000, P001–P023, P023-A–F, P024–P080, P081, P081-A, P081-B, P082–P090.
- P000 is a governing prompt and is not counted among the 98 implementation prompts. Study mode does not change repository files or mark a prompt verified.

## Repository baseline

- The existing Django project is `root/`, with an installed `apps` application. Preserve this layout unless a later prompt gives a concrete reason to adapt it.
- `requirements.txt` currently pins Django 5.2.18, Django REST Framework 3.18.3, drf-spectacular 0.30.0, Pillow 12.3.0, psycopg 3.3.6, and python-dotenv 1.2.4. Django, DRF, PostgreSQL settings, session authentication, global `IsAuthenticated`, and drf-spectacular are already present.
- There is no custom user model and no generated app migration beyond `apps/migrations/__init__.py`. `db.sqlite3` is empty; settings point to PostgreSQL. Preserve migration history and do not reset a database.
- `.env.example` and `.gitignore` already exist. No `docs/` directory, `AGENTS.md`, Git metadata, or architecture PDF was found. This workspace is a project directory but is not currently a Git checkout.
- The requirements file pins direct dependencies but is not a complete transitive lock. P002 must choose and document a reproducible lock approach without needlessly replacing compatible packages.
- Known configuration item: `root/settings.py` contains Django 6.1 email documentation and a `MAILERS` setting while the pinned runtime is Django 5.2. Resolve or document this before relying on configured email; email delivery itself is outside the current core scope.

## Technology direction

For the initial implementation, retain the repository's Python 3.12 target, Django 5.2 LTS line, and compatible DRF. The versions already pinned in `requirements.txt` are the baseline to inspect, not a request to reinstall or upgrade them. Confirm runtime/package compatibility and the dependency lock strategy when P002 is reached. Add only the dependency needed by the current prompt.

## Next prompt

P002 is next after P001 is verified. It should adapt the existing project configuration, preserve the current secret/environment conventions, and avoid the first database migration until P003 installs the custom user model.
