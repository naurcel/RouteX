# RouteX

**Truck Profitability and Delivery Operations Management System**
Built for Redeemed Route Logistics Inc.

![Next.js](https://img.shields.io/badge/Next.js-000000?style=flat&logo=next.js&logoColor=white)
![React](https://img.shields.io/badge/React-20232A?style=flat&logo=react&logoColor=61DAFB)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat&logo=typescript&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-38B2AC?style=flat&logo=tailwind-css&logoColor=white)
![shadcn/ui](https://img.shields.io/badge/shadcn%2Fui-000000?style=flat&logo=shadcnui&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat&logo=postgresql&logoColor=white)
![Supabase](https://img.shields.io/badge/Supabase-3FCF8E?style=flat&logo=supabase&logoColor=white)
![NextAuth.js](https://img.shields.io/badge/Auth.js-000000?style=flat&logo=auth0&logoColor=white)
![Vercel](https://img.shields.io/badge/Vercel-000000?style=flat&logo=vercel&logoColor=white)

---

## What is RouteX?

Redeemed Route Logistics Inc. currently manages deliveries, truck profitability, and company expenses manually, mainly through Microsoft Excel and paper records. RouteX is a **partially automated, web-based system** intended to centralize:

- Delivery management (revenue, expenses, status, POD documents)
- Fleet / truck profitability tracking
- Company transactions not tied to a specific delivery
- Search and record retrieval across deliveries, trucks, drivers, and clients
- Operational and financial reporting
- User administration, roles, and audit trails

Users remain responsible for entering and updating information; the system automates calculations (e.g. delivery margin), search, and report generation.

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Next.js, React, TypeScript, Tailwind CSS, shadcn/ui, Lucide React |
| Backend | Next.js Server Actions + Route Handlers (same app as frontend) |
| Database | PostgreSQL via Supabase |
| File Storage | Supabase Storage |
| Auth | Auth.js (NextAuth.js) |
| Deployment | Vercel |

> RouteX is built as a **single Next.js application** — there is no separate backend service. Server Actions and Route Handlers running inside the Next.js app *are* the backend.

## Project Structure

```
routex/
├── AGENTS.md                       # AI agent workflow rules (kept identical to CLAUDE.md)
├── CLAUDE.md                       # Duplicate of AGENTS.md for tools that only load this file
├── README.md                       # You are here
├── .gitignore
├── RouteX-Knowledge-Base/          # All project documentation
│   ├── 00-Project-Core/
│   ├── 01-Requirements/
│   ├── 02-Architecture/
│   ├── 03-Design/
│   ├── 04-Development/
│   ├── 05-Testing/
│   ├── 06-Decisions/
│   ├── 07-AI-Agents/
│   ├── 08-Logs/
│   └── 09-References/
└── app/                            # The Next.js application (internal structure TBD)
```

## Status

🚧 **This repository currently contains only initial setup scaffolding.**

- ✅ Root-level config and agent-instruction files (`AGENTS.md`, `CLAUDE.md`, `README.md`, `.gitignore`)
- ✅ Placeholder folder structure for `RouteX-Knowledge-Base/` (category names and reading order only — contents not yet written)
- ✅ Placeholder folder for `app/` (the Next.js app itself — internal feature structure not yet designed)
- ❌ No application code has been written yet
- ❌ No database schema or Supabase project have been provisioned yet
- ❌ No authentication, deployment, or CI/CD configuration exists yet

This section will be updated as each of the above actually gets built — nothing above should be read as "done" until it's checked off with a corresponding change in the code.

## Getting Started

_To be written once the `app/` structure and initial dependencies are scaffolded._

## Documentation

All project documentation — requirements, architecture, design, decisions, and logs — lives in [`RouteX-Knowledge-Base/`](./RouteX-Knowledge-Base). Start with `00-Project-Core/` for current status, or `01-Requirements/` for the SRS and project plan.
