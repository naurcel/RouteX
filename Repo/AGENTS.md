> ⚠️ **This file and `CLAUDE.md` must always be edited together and kept word-for-word identical.**
> Some AI coding tools only auto-load `CLAUDE.md`; others only load `AGENTS.md`. If they ever diverge, agents will behave inconsistently depending on which tool is running. Whenever you change one, copy the same change into the other in the same commit.

# AGENTS.md — RouteX

This is the entry point for any AI coding agent (Claude, Copilot, Cursor, etc.) working in the RouteX repository. Read this file in full before doing anything else in this repo.

## 0. What RouteX is (one-line context)

RouteX is a partially automated, web-based truck profitability and delivery operations management system for Redeemed Route Logistics Inc., built as a single Next.js application (frontend UI + Server Actions/Route Handlers as the backend, PostgreSQL via Supabase, Auth.js, Supabase Storage, deployed on Vercel).

---

## 1. Source-of-Truth Hierarchy

When two documents disagree, resolve the conflict using this order — **higher wins**:

1. **Direct, explicit instructions from the human in the current conversation/task.**
2. **`AGENTS.md` / `CLAUDE.md`** (this file) — repo-wide process rules.
3. **`RouteX-Knowledge-Base/06-Decisions/`** — recorded architectural/product decisions (most recent decision on a topic wins over an older one).
4. **`RouteX-Knowledge-Base/01-Requirements/` and `02-Architecture/`** — SRS, project plan, technical documentation.
5. **`RouteX-Knowledge-Base/03-Design/` and `04-Development/`** — design specs, coding conventions, dev guides.
6. **Code comments and existing code patterns** — lowest priority; code can be outdated or wrong, and must never override a written decision or requirement above it.

If a conflict is found between levels, the agent must:
- Follow the higher-priority source for the current task.
- Flag the conflict in its log entry (see §3) so a human can reconcile the lower-priority document.
- Never silently "fix" a requirements or decision document to match the code without human sign-off.

---

## 2. Workflow: Before / During / After

### Before starting any task
- Read this file (`AGENTS.md`) in full, even if you've read it before in this session — it may have changed.
- Read `RouteX-Knowledge-Base/00-Project-Core/` for current project status and active priorities.
- Read any files in `RouteX-Knowledge-Base/06-Decisions/` relevant to the area you're touching.
- Read the relevant subfolder(s) of `01-Requirements/` and `02-Architecture/` for the feature/module in scope.
- Check `08-Logs/` for the most recent entries touching the same area, to avoid duplicating or contradicting recent work.
- If something is ambiguous or contradicted across documents, resolve it using the hierarchy in §1, and log the ambiguity.

### While working
- Follow the modular, feature-based folder convention inside `app/` (one folder per feature/module — do not dump unrelated logic into shared/flat folders).
- Keep the frontend and backend concerns separated *within* a feature folder (e.g. UI components vs. Server Actions vs. types), even though both live in the same Next.js app.
- Write code consistent with the confirmed stack: Next.js, React, TypeScript, Tailwind CSS, shadcn/ui, Lucide React, PostgreSQL (Supabase), Auth.js (NextAuth.js), Supabase Storage.
- Do not introduce a new library, framework, or architectural pattern not already listed in `02-Architecture/` without recording the decision in `06-Decisions/` first.
- Do not invent scope. If a feature isn't described in `01-Requirements/`, stop and flag it rather than guessing.
- Keep commits/changes scoped to the task at hand.

### After finishing a task
- Update any `RouteX-Knowledge-Base/` document whose content is now stale (e.g. requirements clarified, architecture changed, a decision made).
- Add a dated entry to `RouteX-Knowledge-Base/08-Logs/` describing what was done, what was decided, and what (if anything) is left open — see §3 for the mandatory timestamp rule.
- If a new architectural or product decision was made during the task, record it in `06-Decisions/`.
- Never leave the knowledge base describing a state of the system that no longer matches the code.

---

## 3. Timestamp Rule (mandatory, no exceptions)

Every log entry, decision record, or dated note an agent writes **must carry a real day-of-week, date, and time pulled from the agent's own system clock at the moment of writing.**

- ✅ Correct: run the system's actual clock/date command (or equivalent real-time source available to the agent) and use that literal output.
- ❌ Never estimate, guess, infer from context, or reuse a date mentioned earlier in the conversation as if it were "now."
- ❌ Never leave a timestamp blank or as a placeholder (e.g. `[DATE]`) in a committed log entry — resolve it to a real value before writing the file.
- Format: `YYYY-MM-DD HH:MM (Weekday), <timezone if known>` — e.g. `2026-09-28 14:32 (Monday)`.
- If the agent has no access to a real system clock at all, it must say so explicitly in the entry (e.g. `"timestamp unavailable — no system clock access"`) instead of fabricating one.

This rule exists because the knowledge base and logs are used to reconstruct project history. A guessed timestamp is worse than a missing one — it corrupts the record silently.

---

## 4. Knowledge Base Reference

All project documentation lives in **`RouteX-Knowledge-Base/`** (exact name, always — not "docs" or "wiki"). Its immediate structure:

| Folder | Purpose |
|---|---|
| `00-Project-Core/` | High-level project status, goals, current priorities |
| `01-Requirements/` | SRS, project plan, functional/non-functional requirements |
| `02-Architecture/` | System architecture, module breakdowns, tech stack rationale |
| `03-Design/` | UI/UX design references, style guides |
| `04-Development/` | Coding conventions, setup guides, dev workflows |
| `05-Testing/` | Test plans, QA notes |
| `06-Decisions/` | Recorded architectural/product decisions (source of truth over requirements when more recent) |
| `07-AI-Agents/` | Agent-specific operating notes beyond this file |
| `08-Logs/` | Dated work logs (see §3 for timestamp rule) |
| `09-References/` | External references, comparisons, research |

The internal file contents of each subfolder are defined separately as the project progresses — this file only fixes the folder names and reading order, which are treated as stable paths that other documents will reference.

---

## 5. Escalation

If an agent cannot resolve a conflict using §1, cannot find information it needs in the knowledge base, or is asked to do something that contradicts a recorded decision — **stop and ask a human**, rather than guessing or proceeding on an assumption that could be wrong. Log the question in `08-Logs/` with a real timestamp either way.
