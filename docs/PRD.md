Product Requirements Document (PRD) — CreditCare

1. Vision and Objectives
Name: CreditCare
Vision: Provide a responsive web application that helps users avoid late fees and optimize credit card payments through reminders, simulations, and clear payment history.
Objectives:
- Deliver a functional MVP deployed publicly.
- Cover 5 complete user flows (auth, add card, dashboard, simulate, record payment).
- Achieve >70% test coverage in financial logic.
- Document architecture and deployment in README.

2. Scope
In Scope (MVP):
- User registration/login with JWT.
- Card metadata management (issuer, last4, APR, due dates).
- Dashboard with balances and upcoming payments.
- Payment simulator.
- Payment history + CSV export.
- Email/in-app reminders.
Out of Scope (MVP):
- Real payment processing.
- Storing PAN/CVV.
- Enterprise/multi-user features.

3. Personas & User Stories
Personas:
- Student: needs simple reminders.
- Professional: manages multiple cards, wants payoff optimization.
- Parent: exports history for family budgeting.
User Stories:
- Register/login → secure account creation.
- Add card → save metadata, schedule reminders.
- Dashboard → view balances and due dates.
- Simulate payment → calculate payoff scenarios.
- Record payment → update balance and history.
- Export CSV → download history.

4. Functional Requirements
|  |  |  | 
|  |  |  | 
|  |  |  | 
|  |  |  | 
|  |  |  | 
|  |  |  | 
|  |  |  | 
|  |  |  | 



5. Non-Functional Requirements
- Security: bcrypt/Argon2 password hashing, JWT with refresh tokens, TLS in production.
- Performance: p95 < 300ms for critical endpoints.
- Availability: 99% uptime target for MVP.
- Privacy: no PAN/CVV storage.
- Testing: unit, integration, E2E; >70% coverage in financial logic.

6. Architecture & Tech Stack
- Backend: Flask (Python), SQLAlchemy, Marshmallow, Flask-JWT-Extended.
- Frontend: React + TypeScript, Vite, Tailwind CSS.
- Database: PostgreSQL.
- Workers: Celery + Redis (optional for reminders).
- CI/CD: GitHub Actions.
- Hosting: Render/Heroku (backend + DB), Vercel/Netlify (frontend).
Project Structure:
creditcare/
  backend/
    app/
      __init__.py
      models.py
      routes/
        auth.py
        cards.py
      utils/
        security.py
    migrations/
    tests/
    wsgi.py
  frontend/
  docs/
    PRD.md
  README.md
  LICENSE
  .gitignore
  .env.example



7. API Endpoints
- POST /api/auth/register → register user.
- POST /api/auth/login → login, get JWT.
- POST /api/cards → add card.
- GET /api/cards → list cards.
- POST /api/cards/:id/payments → record payment.
- GET /api/cards/:id/history → payment history.
- POST /api/simulate → simulate payoff.
- GET /api/reminders → list reminders.
- POST /api/export/:cardId → export CSV.

8. Roadmap
Phase 1: Planning + repo setup (README, LICENSE, .gitignore, .env.example).
Phase 2: Backend setup (Flask app, models, auth, migrations).
Phase 3: Frontend setup (React app, dashboard, forms).
Phase 4: Testing + CI/CD (GitHub Actions, coverage).
Phase 5: Deployment (Render/Vercel).
Phase 6: Documentation + demo video.

9. Risks & Mitigation
- Sensitive data → mitigate by not storing PAN/CVV.
- Incorrect financial calculations → mitigate with documented formulas + unit tests.
- Notification spam → mitigate with user consent + configurable frequency.
- Secrets leakage → mitigate with .gitignore, GitHub Secrets, hosting provider env vars.

10. Success Metrics
- MVP deployed and accessible.
- 5 user flows demonstrable in video.
- 70% test coverage in financial logic.
- README with architecture and deployment guide.
