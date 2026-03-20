# Proofline – Agent Instructions

## 1. Project Overview

Proofline is a private, single-user web application designed to help the user:

- achieve goals
- develop execution discipline
- build a strong, reality-based mindset

This is NOT a public product.

This app is:

- single-user only
- private
- execution-focused
- dashboard-first (not chat-first)

The system combines:

- structured user input (goals, logs, actions)
- AI analysis (behavior + execution)
- memory from past behavior

---

## 2. Core Product Principles

### Focus

This app is about:

- execution
- behavior
- reality-based feedback

NOT about:

- motivation
- inspiration
- therapy
- social features

---

## 3. MVP Scope (Strict)

### Included

- authentication (magic link only)
- allowlisted email access
- onboarding
- goal creation
- journaling
- daily check-ins
- proof actions
- AI behavior analysis
- dashboard
- chat (context-aware)
- weekly reviews

### Explicitly Excluded

- PDFs
- vector databases / embeddings
- multi-user support
- payments
- public signup
- OAuth flows
- mobile app
- voice features
- external integrations
- agent frameworks (LangChain, LangGraph, etc.)
- unnecessary abstractions

Do NOT add features outside this scope.

---

## 4. Tech Stack

Use exactly:

- Next.js (App Router)
- React
- TypeScript (strict)
- Tailwind CSS
- shadcn/ui
- Supabase (Auth + Postgres)
- OpenAI Node SDK
- zod (for schema validation)
- pnpm

Do NOT introduce:

- Prisma
- Drizzle
- MongoDB
- external state managers unless necessary

Keep it simple and stable.

---

## 5. Authentication Rules

- Magic link login only
- No password auth
- No public signup

Allowlisted email:

- comes from env: `ALLOWED_EMAIL`

Behavior:

- reject all non-allowlisted emails
- protect all routes except `/login`
- create profile on first login
- redirect to onboarding if not completed

---

## 6. Data Model (Core Entities)

The system must include:

- profiles
- goals
- journal_entries
- daily_checkins
- proof_actions
- ai_assessments
- weekly_reviews

Rules:

- all data belongs to one user
- enforce row-level security
- never trust client-provided user IDs
- derive user from session

---

## 7. AI System Definition

### Roles

Primary:

- Execution Architect

Secondary:

- Behavioral Analyst

---

### AI Behavior

Tone:

- direct
- blunt
- realistic
- unsentimental
- truth-first

The AI should:

- evaluate behavior honestly
- identify what matters vs what does not
- detect avoidance, drift, inconsistency
- convert reflection into action
- prescribe next steps
- use past app data as context

The AI should NEVER:

- flatter the user
- provide fake encouragement
- hallucinate memory
- give generic advice
- act like a therapist

---

### Default Output Structure

For analysis tasks, the AI should produce:

1. assessment
2. meaning
3. problem
4. next step
5. stop doing

---

## 8. AI Reliability Rules

- Always validate outputs with zod
- Never write invalid data to the database
- If parsing fails:
  - do NOT write partial results
  - fallback gracefully
- Do not let AI directly mutate critical state without validation

---

## 9. Context Strategy

Do NOT use embeddings or vector search.

Context must be constructed from:

- active goal
- target identity
- blockers
- recent journal entries
- recent check-ins
- open proof actions
- latest AI assessments
- recent weekly reviews

Keep context:

- small
- relevant
- structured

Do NOT dump large raw history.

---

## 10. UI / UX Rules

Style:

- minimal
- black theme
- orange accent
- sharp edges (not rounded)
- high contrast
- panel-based layout

Design tokens:

- background: #0A0A0A
- panel: #111111
- border: #262626
- accent: #F97316
- text primary: #F5F5F5
- text secondary: #A3A3A3
- radius: 4px

UI must feel like:

- a control panel
- a serious execution system
- not playful
- not soft

---

## 11. Core Pages

Implement:

- /login
- /onboarding
- /dashboard
- /journal
- /actions
- /reviews
- /chat
- /settings

---

## 12. Dashboard Requirements

Must show:

- active goal
- target identity
- today’s proof actions
- latest AI assessment
- quick journal input
- quick check-in input

---

## 13. Error Handling

The app must never crash due to:

- missing data
- empty states
- failed AI calls
- incomplete onboarding

Implement:

- loading states
- empty states
- fallback UI

---

## 14. Security Rules

- no secrets in repo
- use env variables only
- restrict to allowlisted email
- protect all routes
- do not expose OpenAI key to client
- enforce RLS

---

## 15. Environment Variables

Expected:
