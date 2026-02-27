# Product Requirements Document (PRD) — CreditCare

---

## 1. Vision and Objectives
**Name**: CreditCare  
**Vision**: Provide a responsive web application that helps users avoid late fees and optimize credit card payments through reminders, simulations, and clear payment history.  
**Objectives**:
- Deliver a functional MVP deployed publicly.
- Cover 5 complete user flows (auth, add card, dashboard, simulate, record payment).
- Achieve >70% test coverage in financial logic.
- Document architecture and deployment in README.

---

## 2. Scope
**In Scope (MVP)**:
- User registration/login with JWT.
- Card metadata management (issuer, last4, APR, due dates).
- Dashboard with balances and upcoming payments.
- Payment simulator.
- Payment history + CSV export.
- Email/in-app reminders.

**Out of Scope (MVP)**:
- Real payment processing.
- Storing PAN/CVV.
- Enterprise/multi-user features.

---

## 3. Personas & User Stories
**Personas**:
- Student: needs simple reminders.
- Professional: manages multiple cards, wants payoff optimization.
- Parent: exports history for family budgeting.

**User Stories**:
1. Register/login → secure account creation.
2. Add card → save metadata, schedule reminders.
3. Dashboard → view balances and due dates.
4. Simulate payment → calculate payoff scenarios.
5. Record payment → update balance and history.
6. Export CSV → download history.

---

## 4. Functional Requirements
| ID | Requirement | Priority |
|----|-------------|----------|
| RF-01 | User registration/login with JWT | High |
| RF-02 | Add card metadata | High |
| RF-03 | Dashboard summary | High |
| RF-04 | Reminders (email/in-app) | High |
| RF-05 | Payment simulator | Medium |
| RF-06 | Record payments | Medium |
| RF-07 | Export CSV | Low |

---

## 5. Non-Functional Requirements
- **Security**: bcrypt/Argon2 password hashing, JWT with refresh tokens, TLS in production.
- **Performance**: p95 < 300ms for critical endpoints.
- **Availability**: 99% uptime target for MVP.
- **Privacy**: no PAN/CVV storage.
- **Testing**: unit, integration, E2E; >70% coverage in financial logic.

---

## 6. Architecture & Tech Stack
- **Backend**: Flask (Python), SQLAlchemy, Marshmallow, Flask-JWT-Extended.
- **Frontend**: React + TypeScript, Vite, Tailwind CSS.
- **Database**: PostgreSQL.
- **Workers**: Celery + Redis (optional for reminders).
- **CI/CD**: GitHub Actions.
- **Hosting**: Render/Heroku (backend + DB), Vercel/Netlify (frontend).

**Project Structure**: